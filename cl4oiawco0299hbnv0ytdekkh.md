## Introducing CodeGuard: The open-source tool to obfuscate your JavaScript or Python code

**P**robably most of us know that **copying and pasting from GitHub, Stackoverflow, etc.** *doesn't* make you a **programmer**.

Also, **it's not great for** *someone to steal your code* and **use it pretending that he made that code/script**, right?

**Here CodeGuard comes!** *The open-source tool to obfuscate your JavaScript or Python code in no time!*

## How I got this inspiration?

%[https://giphy.com/gifs/sesamestreet-Zd5ZVGn3ZvYKl7U6MW]

**Once upon a time**, I was creating an **project which does really great thing including making meetings, etc.** and this idea came in my mind:

***Why would I allow someone steal my code pretending that he wrote that script/code?***

So, I though why don't I make a code obfuscator to make my code hard to read and nearly impossible to understand? So, that's the beginning of **[CodeGuard](https://codeguard.tech)**.

## How did I make it? (Project workflow)

**Once a user provides a link to the file, we recommend using [*GitHub Gist*](https://gist.github.com) because the project was made to be used with Gist, but it will work also if you give a direct link to the file like `https://example.com/myproject/main.py`**

**The user will be selecting either Python or JavaScript:**

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655798332965/e4aP95m-u.png align="left")

Upon the user selection, it will call the API located in `api.codeguard.tech` providing 2 parameters, the code link in `link` and the programming language in `lang`, of course you would like to try to use the **API** yourself, we will leave a guide below!

As soon as the **API has been called**, it will start getting the file and obfuscating it, as soon as the **obfuscated file is ready, it will be automatically downloaded at the user side**.

Note: **For Python code, change the obfuscated code extension to `.pyo` and use `python -O <file-name>.pyo` to run the file!**

## What problems did I experience

- **Making the back-end**

As **I need to use JS/PY** to obfuscate, although they run at the client side, I am unable to run the script to obfuscate from client-side

- **How will I host and make the API**

With the help of Flask, I can make a API with pretty good functionalities which can help me in the project, and with the existence of Linode, I can host my API on a Linux server in the cloud!

## The tech-stack I used + Why did I use it?

- **[Next.js](https://nextjs.org/)** - *Making the front-end design of the website*

- **HTML/CSS** - *Making front-end*

- **[JavaScript](https://javascript.com)** - *Back-end, for e.g. modal (alert) and link validation*

- **[Linux](https://linux.org) [Ubuntu](https://ubuntu.com) ([Linode](https://linode.com))** - *Host the API*

- **[Vercel](https://vercel.com)** - *Host the website*

- **[Python](https://python.org) ([Flask](https://flask.palletsprojects.com/))** - *Used to make the API*

## API

### Use the API (hosted by us)

It's really simple to use our API, in JavaScript, it only requires one line of code!

```js
window.location = "https://api.codeguard.tech/?link=<code link here>&lang=<js or py>
```

For example:

```js
window.location = "https://api.codeguard.tech/?link=https://gist.githubusercontent.com/Omar8345/1038a82e7db5f81d0722a4f2ab701924/raw/b213490f419b1d67de6a6a1647557934b97fc1ef/nicecode.js&lang=js
```

### Hosting the API on your machine

- Clone the repository on your local machine:

`git clone https://github.com/Omar8345/CodeGuard`

- Next, head into `CodeGuard/API` and open your favorite IDE, if you use **Visual Studio Code**, just enter:

`code .`

- And it will open up **VSC** in the folder, just run in the terminal the following command:

`$env:FLASK_APP="__init__.py && flask run"`

You should see a local link, head into it or [http://127.0.0.1:5000/](http://127.0.0.1:5000/) and you should find some kind of error, just simply ignore it, now add the `link` and `lang` parameters value and you should be good to go!

**Made using [Vercel](https://vercel.com) and [Linode](https://linode.com) for the [Hashnode](https://hashnode.com) X [Linode](https://linode.com) *Hackathon*!**

## My quote

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655800348645/6a-GYYsTT.png align="left")

> **Take your time - But don't mess up!**

**Take your time** in studying, even **study like 72 hours**, but ***take the full mark!***

## Important Links 🔗 - Try CodeGuard!

- **[GitHub Repo](https://github.com/Omar8345/CodeGuard)**

- **[Next.js](https://nextjs.org)**

- **[CodeGuard](https://codeguard.tech)**

### Special thanks to Vedant Singhal

**Vedant** a developer in high school from **India**! **Vedant** hopefully helped me a lot in this project, so I would like to thank him here!

**Thank you Vedant!**

Check out Vedant on Social Media:

- **[GitHub - Ved235](https://github.com/Ved235)**
- **[Buymeacoffee - Ved235](https://www.buymeacoffee.com/ved235)**
- **[Vedant's Blog](https://learnwithved.hashnode.dev/)**

### We would like to hear your feedback and suggestions in the comments below!