## Covid-19 chatbot - Neural Search - Jina AI

## Welcome to a new fancy "Neural Search" project!

We will make a Covid-19 chatbot using neural search, will be using **Jina AI** open-source framework!

- ***What will we cover:***
   - **What is Jina AI?**
   - **What is neural search?**
   - **Coding the bot**

Without waiting such more time, let's start!

## What is Jina AI?

**Jina AI** is a *Cloud-Native Neural Search Framework for **any kind of data!***

### Why Jina AI?

- ⏱️ **Save time** - *The* design pattern of neural search systems, which quickly builds solutions for indexing, querying, understanding multi/cross modal data such as: 
   - **Video**,
   - **Image**,
   - **Text**,
   - **Audio**,
   - **Source code**,
   - **PDF** 

- ☁️ **Local and cloud friendly** - **Distributed** **architecture**, **scalable**, and **cloud-native**. Same developer experience is also experienced on *local*:

   -   [Docker Compose](https://docs.jina.ai/how-to/docker-compose/), 
   -   [Kubernetes](https://docs.jina.ai/how-to/kubernetes/)

- 🚀 **Serve, scale & share** - *Serve* a local project with:
   - **HTTP**,
   - **WebSockets**,
   - **gRPC**

- 🍱 **Own your stack** - *Keep* end-to-end stack ownership of your solution. Avoid integration pitfalls you get with fragmented, multi-vendor, generic legacy tools. Enjoy the integration with the neural search ecosystem including [DocArray](https://docarray.jina.ai), [Hub](https://hub.jina.ai) and [Finetuner](https://finetuner.jina.ai).

## What is neural search?

> In short, neural search is a new approach to retrieving information. Instead of telling a machine a set of rules to understand what data is what, neural search does the same thing with a pre-trained neural network. This means developers don’t have to write every little rule, saving them time and headaches, and the system trains itself to get better as it goes along.

> **Source:** [What is Neural Search? | Written on Medium by Jina AI](https://medium.com/jina-ai/what-is-jina-and-neural-search-7a9e166608ab)

## Coding the bot

First, let's install Jina.

### Installing Jina

Open your terminal, and enter the following command: `pip install jina`

More install options for **Docker**, **Windows**, and **Conda** can be found [here](https://docs.jina.ai/get-started/install/).

But in our project, we need extra dependencies, so use `pip install "jina[demo]"`

Now after installation, enter `jina` into the terminal to confirm the installation was successful or not.

### Coding the bot

First, we will start coding `app.py`.

```py
import os
import urllib.request
import webbrowser
from pathlib import Path

from jina import Flow, Document
from jina.importer import ImportExtensions
from jina.logging import default_logger
from jina.logging.profile import ProgressBar
from jina.parsers.helloworld import set_hw_chatbot_parser

if __name__ == '__main__':
    from executors import MyTransformer, MyIndexer
else:
    from .executors import MyTransformer, MyIndexer
```

Here we imported all the libraries we need for the friendly Covid-19 QA bot.

```py
def hello_world(args):
    """
    Execute the chatbot example.
    :param args: arguments passed from CLI
    """
    Path(args.workdir).mkdir(parents=True, exist_ok=True)

    with ImportExtensions(
        required=True,
        help_text='this demo requires Pytorch and Transformers to be installed, '
        'if you haven\'t, please do `pip install jina[torch,transformers]`',
    ):
        import transformers, torch

        assert [torch, transformers]  #: prevent pycharm auto remove the above line

    targets = {
        'covid-csv': {
            'url': args.index_data_url,
            'filename': os.path.join(args.workdir, 'dataset.csv'),
        }
    }

    # download the data
    download_data(targets, args.download_proxy, task_name='download csv data')

    # now comes the real work
    # load index flow from a YAML file

    f = (
        Flow()
        .add(uses=MyTransformer, parallel=args.parallel)
        .add(uses=MyIndexer, workspace=args.workdir)
    )

    # index it!
    with f, open(targets['covid-csv']['filename']) as fp:
        f.index(Document.from_csv(fp, field_resolver={'question': 'text'}))

    # switch to REST gateway
    url_html_path = 'file://' + os.path.abspath(
        os.path.join(os.path.dirname(os.path.realpath(__file__)), 'static/index.html')
    )
    f.use_rest_gateway(args.port_expose)
    with f:
        try:
            webbrowser.open(url_html_path, new=2)
        except:
            pass  # intentional pass, browser support isn't cross-platform
        finally:
            default_logger.success(
                f'You should see a demo page opened in your browser, '
                f'if not, you may open {url_html_path} manually'
            )
        if not args.unblock_query_flow:
            f.block()
```

Here, we made a function to execute our bot.

```py
def download_data(targets, download_proxy=None, task_name='download fashion-mnist'):
    """
    Download data.
    :param targets: target path for data.
    :param download_proxy: download proxy (e.g. 'http', 'https')
    :param task_name: name of the task
    """
    opener = urllib.request.build_opener()
    opener.addheaders = [('User-agent', 'Mozilla/5.0')]
    if download_proxy:
        proxy = urllib.request.ProxyHandler(
            {'http': download_proxy, 'https': download_proxy}
        )
        opener.add_handler(proxy)
    urllib.request.install_opener(opener)
    with ProgressBar(task_name=task_name, batch_unit='') as t:
        for k, v in targets.items():
            if not os.path.exists(v['filename']):
                urllib.request.urlretrieve(
                    v['url'], v['filename'], reporthook=lambda *x: t.update_tick(0.01)
                )


if __name__ == '__main__':
    args = set_hw_chatbot_parser().parse_args()
    hello_world(args)
```

Here, we made a function to download Covid-19 stats when needed by user in addition to use `if __name__ == '__main__'` to run the script/bot.

We are done of `app.py` now we start with `my_executors.py`.

```py
import os
from pathlib import Path
from typing import Optional, Dict, Tuple

import numpy as np
import torch
from transformers import AutoModel, AutoTokenizer

from jina import Executor, DocumentArray, requests, Document
```

Here, we imported the need libraries for the executor.

```py
class MyTransformer(Executor):
    """Transformer executor class """

    def __init__(
        self,
        pretrained_model_name_or_path: str = 'sentence-transformers/distilbert-base-nli-stsb-mean-tokens',
        base_tokenizer_model: Optional[str] = None,
        pooling_strategy: str = 'mean',
        layer_index: int = -1,
        max_length: Optional[int] = None,
        acceleration: Optional[str] = None,
        embedding_fn_name: str = '__call__',
        *args,
        **kwargs,
    ):
        super().__init__(*args, **kwargs)
        self.pretrained_model_name_or_path = pretrained_model_name_or_path
        self.base_tokenizer_model = (
            base_tokenizer_model or pretrained_model_name_or_path
        )
        self.pooling_strategy = pooling_strategy
        self.layer_index = layer_index
        self.max_length = max_length
        self.acceleration = acceleration
        self.embedding_fn_name = embedding_fn_name
        self.tokenizer = AutoTokenizer.from_pretrained(self.base_tokenizer_model)
        self.model = AutoModel.from_pretrained(
            self.pretrained_model_name_or_path, output_hidden_states=True
        )
        self.model.to(torch.device('cpu'))

    def _compute_embedding(self, hidden_states: 'torch.Tensor', input_tokens: Dict):
        import torch

        fill_vals = {'cls': 0.0, 'mean': 0.0, 'max': -np.inf, 'min': np.inf}
        fill_val = torch.tensor(
            fill_vals[self.pooling_strategy], device=torch.device('cpu')
        )

        layer = hidden_states[self.layer_index]
        attn_mask = input_tokens['attention_mask'].unsqueeze(-1).expand_as(layer)
        layer = torch.where(attn_mask.bool(), layer, fill_val)

        embeddings = layer.sum(dim=1) / attn_mask.sum(dim=1)
        return embeddings.cpu().numpy()

    @requests
    def encode(self, docs: 'DocumentArray', *args, **kwargs):
        import torch

        with torch.no_grad():

            if not self.tokenizer.pad_token:
                self.tokenizer.add_special_tokens({'pad_token': '[PAD]'})
                self.model.resize_token_embeddings(len(self.tokenizer.vocab))

            input_tokens = self.tokenizer(
                docs.get_attributes('content'),
                max_length=self.max_length,
                padding='longest',
                truncation=True,
                return_tensors='pt',
            )
            input_tokens = {
                k: v.to(torch.device('cpu')) for k, v in input_tokens.items()
            }

            outputs = getattr(self.model, self.embedding_fn_name)(**input_tokens)
            if isinstance(outputs, torch.Tensor):
                return outputs.cpu().numpy()
            hidden_states = outputs.hidden_states

            embeds = self._compute_embedding(hidden_states, input_tokens)
            for doc, embed in zip(docs, embeds):
                doc.embedding = embed


class MyIndexer(Executor):
    """Simple indexer class """

    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self._docs = DocumentArray()
        Path(self.workspace).mkdir(parents=True, exist_ok=True)
        self.filename = os.path.join(self.workspace, 'chatbot.ndjson')
        if os.path.exists(self.filename):
            self._docs = DocumentArray.load(self.filename)

    def close(self) -> None:
        self._docs.save(self.filename)

    @requests(on='/index')
    def index(self, docs: 'DocumentArray', **kwargs):
        self._docs.extend(docs)

    @requests(on='/search')
    def search(self, docs: 'DocumentArray', **kwargs):
        a = np.stack(docs.get_attributes('embedding'))
        b = np.stack(self._docs.get_attributes('embedding'))
        q_emb = _ext_A(_norm(a))
        d_emb = _ext_B(_norm(b))
        dists = _cosine(q_emb, d_emb)
        idx, dist = self._get_sorted_top_k(dists, 1)
        for _q, _ids, _dists in zip(docs, idx, dist):
            for _id, _dist in zip(_ids, _dists):
                d = Document(self._docs[int(_id)], copy=True)
                d.score.value = 1 - _dist
                _q.matches.append(d)

    @staticmethod
    def _get_sorted_top_k(
        dist: 'np.array', top_k: int
    ) -> Tuple['np.ndarray', 'np.ndarray']:
        if top_k >= dist.shape[1]:
            idx = dist.argsort(axis=1)[:, :top_k]
            dist = np.take_along_axis(dist, idx, axis=1)
        else:
            idx_ps = dist.argpartition(kth=top_k, axis=1)[:, :top_k]
            dist = np.take_along_axis(dist, idx_ps, axis=1)
            idx_fs = dist.argsort(axis=1)
            idx = np.take_along_axis(idx_ps, idx_fs, axis=1)
            dist = np.take_along_axis(dist, idx_fs, axis=1)

        return idx, dist


def _get_ones(x, y):
    return np.ones((x, y))


def _ext_A(A):
    nA, dim = A.shape
    A_ext = _get_ones(nA, dim * 3)
    A_ext[:, dim : 2 * dim] = A
    A_ext[:, 2 * dim :] = A ** 2
    return A_ext


def _ext_B(B):
    nB, dim = B.shape
    B_ext = _get_ones(dim * 3, nB)
    B_ext[:dim] = (B ** 2).T
    B_ext[dim : 2 * dim] = -2.0 * B.T
    del B
    return B_ext


def _euclidean(A_ext, B_ext):
    sqdist = A_ext.dot(B_ext).clip(min=0)
    return np.sqrt(sqdist)


def _norm(A):
    return A / np.linalg.norm(A, ord=2, axis=1, keepdims=True)


def _cosine(A_norm_ext, B_norm_ext):
    return A_norm_ext.dot(B_norm_ext).clip(min=0) / 2
```

Here, we ended the `my_executors.py` file, in this snippet, we made all the rest of the code to analyze the data and such on.

Next, make an empty file called `__init.py__`, that's it!

Make a folder called `static` which can be found in the GitHub Repo at the end of this article, copy the data which is in that folder in **GitHub Repo**...

## Outro

Thanks for reading the article!

Important links:

- [**GitHub Repo**](https://github.com/OmarDev100/covid19-bot-jina-ai)
- [**Jina AI**](https://www.jina.ai)
- [**Jina Docs**](https://docs.jina.ai/)
- [**Jina AI GitHub**](https://github.com/jina-ai)
- [**Jina Community (Slack)**](https://slack.jina.ai/)
- [**Jina AI on YouTube**](https://www.youtube.com/c/JinaAI/)
- [**Jina AI on LinkedIn**](https://www.linkedin.com/company/jinaai/)
- [**Jina AI on Twitter**](https://twitter.com/jinaAI_/)
- [**Jina AI on Meetup**](https://meetup.com/jina-community-meetup/)
- [**Jina AI Blog on Medium**](https://medium.com/jina-ai)
- [**Jina AI Blog (Outdated)**](https://jina.ai/blog/)