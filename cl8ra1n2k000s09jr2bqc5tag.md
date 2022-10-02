## Connect MetaMask Wallet with Flask and Discord.py

## Introduction

Today we will build a `Discord.py` and use `Flask` to allow to integrate the Ethereum wallet addresses with the wallet, you use the `Flask` frontend to connect the wallet while it's logged in the `Flask` system and when you want to check if synced, the `Discord.py` bot sends a `JSON POST` request to read.

**SO LET'S GOOOOO 🔥🔥🔥**

## Setup the Flask Page

Start by creating a new directory, and in that directory, create a folder for the Flask page:

```bash
mkdir metamask-flask-discord
cd metamask-flask-discord
mkdir flask
cd flask
```

Now, create an `app.py` file and a `log.txt` and paste this into the `app.py`:

```py
from flask import Flask, render_template, Response, request
app = Flask(__name__)

@app.route('/<discord_id>')
def index(discord_id):
    return render_template('index.html', discordId = discord_id)

@app.route('/sync', methods=['POST'])
def sync():
    discord_id = request.json['discordId']
    wallet_address = request.json['walletAddress']
    with open('log.txt', 'r+') as f:
        file = f.read()
        if discord_id in file:
            if wallet_address in file:
                Pass
            else:
                f.write(' ' + wallet_address)
        else:
            f.write('\n' + discord_id + ' ' + wallet_address)
    f.close()

@app.route('/read', methods=['POST'])
def read():
    discord_id = request.json['discordId']
    with open('log.txt', 'r') as f:
        file = f.read()
        if discord_id in file:
            wallet_addresses = file.split(discord_id)[1].split(' ')
            wallet_addresses.pop(0)
            return Response(str(wallet_addresses), mimetype='application/json')
        else:
            return Response('No wallet address found', mimetype='application/json')
```

This is our main `flask` file, what we are doing here, we are setting `3` routes:

 - `/` (main)
 - `sync` (to sync with the logs which also syncs with the bot)
 - `read` (provides wallet addresses for a specific user)

And for `sync` and `read` we will receive a `JSON POST` request, `POST` is more safer, that's why I personally prefer it. 

Also, in both `sync` and `read` we open up the `log.txt` either to read wallet addresses for a specific user, or write new wallet addresses for a new user.

Now, let's create the landing page where you can connect your `MetaMask` wallet:

```bash
mkdir templates
touch index.html
```

Now in your `index.html`, paste this:

```html
<!DOCTYPE html>
<html>
    <head>
        <title>MetaMask Connection</title>
    </head>
    <body>
        <center>
        <h1>Connect Your MetaMask Wallet Here To Connect With Discord!</h1>
        <button id="connectWallet" onclick="">Connect Wallet</button>
        <button id="syncDiscord" onclick="">Sync Discord</button>

        <p id="walletAddress"></p>

        <script type="text/javascript">
            var discordId = "{{ discordId }}";
            window.walletAddress = null
            const syncDiscord = document.getElementById('syncDiscord');
            const connectWallet = document.getElementById('connectWallet')
            const walletAddress = document.getElementById('walletAddress')


            function checkInstalled() {
                if (typeof window.ethereum == 'undefined') {
                    walletAddress.innerText = 'Please install MetaMask to continue.'
                    return false
                }
                connectWallet.addEventListener('click', connectWalletwithMetaMask)
            }

            async function connectWalletwithMetaMask() {
                const accounts = await window.ethereum.request({ method: 'eth_requestAccounts' })
                .catch((e) => {
                    console.error(e.message)
                    return
                })
                if (!accounts) { return }

                window.walletAddress = accounts[0]
                walletAddress.innerText = window.walletAddress
                

                connectWallet.innerText = 'Sign Out'
                connectWallet.removeEventListener('click', connectWalletwithMetaMask)
                setTimeout(() => {
                    connectWallet.addEventListener('click', signOutOfMetaMask)
                    syncDiscord.addEventListener('click', syncDiscordWithWallet)
                }, 200 )
            }

            function signOutOfMetaMask() {
                window.walletAddress = null
                walletAddress.innerText = ''
                connectWallet.innerText = 'Connect Wallet'
                
                connectWallet.removeEventListener('click', signOutOfMetaMask)
                syncDiscord.removeEventListener('click', syncDiscordWithWallet)

                setTimeout(() => {
                    connectWallet.addEventListener('click', connectWalletwithMetaMask)
                }, 200 )
            }

            window.addEventListener('DOMContentLoaded', () => {
                checkInstalled()
            })

            async function syncDiscordWithWallet() {
                alert("If the wallet is already in the system, nothing would happen, if not, it would add it to the bot system.")
                const response = await fetch('/sync', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({
                        walletAddress: window.walletAddress,
                        discordId: discordId
                    })
                })
            }

        </script>
        </center>   
    </body>
</html>
```

So here we make few buttons, and make a few event listeners which run certain functions, and for example, when the wallet is connected, we replace the event listener to listen to the sign out function, why would the user sign in again if he is already signed in, hahah!

And for syncing here, we send a `JSON POST` request with `walletAddress` and `discordId` to `/sync` to save it!

## Working on our Discord.py bot

Start by creating a directory and creating a `.env` & `bot.py`:

```bash
mkdir discordbot
cd discordbot
touch .env
touch bot.py
```

Now, open up your `.env` file where you save your token just like this:

```env
TOKEN=<your-discord-bot-token-here>
```
Let's work on the actual bot now:

```py
import discord
from discord.ext import commands
import requests
import os
from dotenv import load_dotenv
load_dotenv()
token = os.getenv('TOKEN')


intents = discord.Intents.all()
bot = commands.Bot(command_prefix='$', intents=intents)

@bot.event
async def on_ready():
    print("Bot is ready")
    print("Username: {}".format(bot.user.name))
    print("ID: {}".format(bot.user.id))
    print("Discord.py Version: {}".format(discord.__version__))
    print("------")

@bot.command()
async def linkwallet(ctx):
    await ctx.author.send("Click on this link to connect your MetaMask Wallet")
    await ctx.author.send("Link your wallet here: http://127.0.0.1:5000/{}".format(ctx.author.id))

@bot.command()
async def readuser(ctx, userid: str):
    r = requests.post('http://127.0.0.1:5000/read', json={'discordId': userid})
    await ctx.send(r.text)




bot.run(token)
```

So what we are doing is simple, first `linkwallet` command which actually sending a DM with a link like this to connect: `http://127.0.0.1:5000/<discord-id>`

And `readuser` gets a `userid` and send a JSON request to read and returns the `JSON` response back to the user!

## Try it out!

Let's run the `flask` app:

```bash
cd flask
flask run
```

And let's run the bot:

```bash
cd discordbot
python bot.py
```

## Video Demo:

%[https://www.youtube.com/watch?v=3NBCYG2rbjc]

## Important Links 🔗

 - [GitHub Repo](https://github.com/Omar8345/metamask-discord)

## Thanks for reading!!!

Thanks for reading this article 🚀

Hope you learned something **useful !!!**