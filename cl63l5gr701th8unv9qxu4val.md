## Introducing PollnVote - create polls and get votes from the public your team

## Introducing PollnVote

Are you a newbie developer? Or do you work in teams? Don't you know what programming language to learn? Or do you want to make a poll in your team? You are in the perfect right place, it's **PollnVote**!

## Why PollnVote?

**PollnVote** is open-source, which means if you want to host it only to be used for your team, it's possible, you just need a machine and database to get it up and running! **PollnVote** also allow you to make public votes where anyone from the community can vote.

## What was my tech-stack?

For making the actual big backend, I used the *MySQL database provided by **PlanetScale*** and used **Prisma** with **Next.js** to interact with the database. Well, here is the full tech-stack:

- **Next.js** - Creating the website
- **TypeScript & JavaScript** - Used with *Next.js* to make the website
- **Prisma** - Interact with the database to create polls, etc.
- **MySQL** - I used a *MySQL* database provided by **Prisma** to save polls, etc.
- **TailwindCSS** - Used to make a better *UI* (*user interface*) for the application

## Role of PlanetScale and my feedback

**PlanetScale** is a *server-less* MySQL database provider. To be honest, it's the first time using *Prisma* and also, **PlanetScale**. The use of the database was to save *polls* & *votes*.

If you would like to check the *database object*, check `prisma/schema.prisma` file.

## Deploy/Test it yourself

Start by cloning the repo:

```bash
git clone https://github.com/Omar8345/PollnVote
```

Change the directory and install the required packages:

```bash
cd PollnVote
npm install
```

Now, get your enviroment variables ready:

```bash
mv .env.example .env
```

Open your favorite IDE and set `DATABASE_URL` in `.env`, done? Sync your database and start the app:

```bash
npx prisma db push
npm run dev
```

Now, you are running **PollnVote** on your local machine 🎉

## Important Links 🔗

- **GitHub Repo** - [*Omar8345/PollnVote*](https://github.com/Omar8345/pollnvote)

- **Live Demo** - [*pollnvote.vercel.app*](https://pollnvote.vercel.app)

## The end

Thanks for reading, please provide any feedback if possible :)
