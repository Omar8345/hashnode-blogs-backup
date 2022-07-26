## Introducing OnePass - The encrypted safe password manager!

Worried about memorizing many passwords? And instead using the same password for all your accounts? We have got the solution, introducing **OnePass**, the encrypted safe password manager!

### How does it work?

**OnePass** uses **NextAuth.js** to authenticate users *like you*. As soon as you add a password, it will be **encrypted** by a *secret key*, and once you try to view the password, it's *decrypted*.

For making sure who owns the **email/password** object, we link it to a user account on *OnePass*.

![](https://media4.giphy.com/media/yl9M9EtQ81pQJMBhT0/giphy.gif?cid=790b76112730b0e0a06f30c87918d4ed2d93135c543bc734&rid=giphy.gif&ct=g)

### What is my tech-stack?

For this project, I used:

- **Next.js** - Building the website
- **TypeScript** - Used with *Next.js* to give functionality to the website
- **TailwindCSS** - Used to give styling
- **Prisma** - To interact with the database (*PlanetScale*)
- **tRPC** - For making the *TypeScript **API***
- **NextAuth** - For authenticating users

### How PlanetScale was helpful

**PlanetScale** provided me a free **database** where I can store 2 important things with the help of *Prisma*, which are the **user** object (*credentials used to sign in to OnePass*) and the **external credentials** object (*where a username/email and password is saved for an external website like Google*), where it's the first time using **Prisma**, I learned a lot about *MySQL* 💖.

### Important Links 🔗

- **GitHub** - *[Omar8345/OnePass](https://github.com/Omar8345/OnePass)*
- **Live Demo** - *[one-pass.vercel.app](https://one-pass.vercel.app/)*

### Thanks for reading!

Special thanks to **PlanetScale** and **Hashnode** for organizing this *awesome* Hackathon!