## Build a to-do Node.js CLI with Prisma and Next.js

Yo! What's up? Remember the last article where we used Prisma with Next.js and made a CLI and added an authentication feature? I noticed many of you learned a lot! So here?! You will learn even more, including making a to-do list app as a CLI with Prisma and Next.js API powering the application to give it the best functionality!

Hold on, Omar? **Why** do we need Prisma/Next.js? The reason why buddy is because this application allows you to sync your tasks from anywhere in the world!

Without further time wasting, let's get started.

## Creating our API

First of all, we need a database, so let's use PlanetScale for this! Head over to [planetscale.com](https://planetscale.com) and click **Get Started**, create your database, and wait for it to get ready for work!

![PlanetScale Database Creation](https://cdn.hashnode.com/res/hashnode/image/upload/v1662274213691/vBI6L8cM7.png?auto=compress)

Now, launch your terminal and start a new **Next.js** project using `npx` after that change directory:

```bash
npx create-next-app
cd to-do-list-app
```

Now after we created our project, let's add Prisma and get it ready so run the following command in the terminal:

```bash
yarn add prisma @prisma/client
yarn prisma init
```

After that we will get a `schema.prisma` file in the `prisma` folder, replace the file with the following:

```prisma
generator client {
  provider = "prisma-client-js"
  previewFeatures = ["referentialIntegrity"]
}

datasource db {
  provider = "mysql"
  url = env("DATABASE_URL")
  referentialIntegrity = "prisma"
}
```

So, what we just most importantly changed the database provider to `mysql` because we are using a **MySQL** database.

Now on the **PlanetScale** dashboard, click on *Connect* and choose **Prisma** as the option to connect with, copy the `.env` file provided and create a `.env` file in your project and paste what you just copied.

Now we will make 2 models, a `User` and a `Task`, so add these 2 models to your Prisma schema file:

```prisma
model User {
  id Int @id @default(autoincrement())
  username String @unique
  password String
  token String @unique
}

model Task {
  id Int @id @default(autoincrement())
  title String
  userToken String
}
```

Now, your schema file should look like this:

```prisma
generator client {
  provider = "prisma-client-js"
  previewFeatures = ["referentialIntegrity"]
}

datasource db {
  provider = "mysql"
  url = env("DATABASE_URL")
  referentialIntegrity = "prisma"
}

model User {
  id Int @id @default(autoincrement())
  username String @unique
  password String
  token String @unique
}

model Task {
  id Int @id @default(autoincrement())
  title String
  userToken String
}
```

Now run `yarn prisma db push` to sync your **MySQL PlanetScale Database**.

We have to now create our API files, first remove `pages/api/hello.js` file and create a file called `register.js` in `pages/api` folder and paste the following code:

```js
import { PrismaClient } from '@prisma/client';

export default function handler(req, res) {
    const prisma = new PrismaClient();
    const { username, password, token } = req.body;
    if (!username || !password || !token) {
        res.status(400).json({
            message: 'Missing username, password or token'
        });
        return;
    }
    prisma.user.findUnique({
        where: {
            username: username
        }
    }).then(user => {
        if (user) {
            res.status(400).json({
                message: 'Username already taken'
            });
        } else {
            prisma.user.findUnique({
                where: {
                    token: token
                }
            }).then(user => {
                if (user) {
                    res.status(400).json({
                        message: 'Token already taken'
                    });
                } else {
                    prisma.user.create({
                        data: {
                            username: username,
                            password: password,
                            token: token
                        }
                    }).then(user => {
                        res.json({
                            message: "User created successfully",
                            user: user
                        });
                    });
                }
            }
            );
        }
    });

}
```

What we are doing here is defining a **Prisma** client and making variables for `username`, `password`, and `token`. If one of the parameters isn't provided, we return an error:

```js
const prisma = new PrismaClient();
    const { username, password, token } = req.body;
    if (!username || !password || !token) {
        res.status(400).json({
            message: 'Missing username, password or token'
        });
        return;
    }
```

And for registration we first check if username is used, if yes, we return an error, if not, we check if the token is used, if yes, returns an error as usual, if not, we will proceed to registration:

```js
    prisma.user.findUnique({
        where: {
            username: username
        }
    }).then(user => {
        if (user) {
            res.status(400).json({
                message: 'Username already taken'
            });
        } else {
            prisma.user.findUnique({
                where: {
                    token: token
                }
            }).then(user => {
                if (user) {
                    res.status(400).json({
                        message: 'Token already taken'
                    });
                } else {
                    prisma.user.create({
                        data: {
                            username: username,
                            password: password,
                            token: token
                        }
                    }).then(user => {
                        res.json({
                            message: "User created successfully",
                            user: user
                        });
                    });
                }
            }
            );
        }
    });
```

Now, we have the user to be able to authenticate/login, create `login.js` file and paste the following:

```js
import { PrismaClient } from '@prisma/client';

export default function handler(req, res) {
    const prisma = new PrismaClient();
    const { username, password } = req.body;
    if (!username || !password) {
        res.status(400).json({
            message: 'Missing username or password'
        });
        return;
    }
    prisma.user.findUnique({
        where: {
            username: username
        }
    }).then(user => {
        if (user) {
            if (user.password === password) {
                res.json({
                    message: 'User authenticated successfully',
                    userToken: user.token,
                    user: username
                });
            } else {
                res.status(400).json({
                    message: 'Incorrect password'
                });
            }
        } else {
            res.status(400).json({
                message: 'No user found'
            });
        }
    }
    );

}
```

So as always we are defining the *Prisma* client and checking if one of the parameters (`username` or `password`) are missing, and if so, we will return an error:

```js
    const prisma = new PrismaClient();
    const { username, password } = req.body;
    if (!username || !password) {
        res.status(400).json({
            message: 'Missing username or password'
        });
        return;
    }
```

Then we use the `findUnique` feature to use the `username` which is unique to find a record/user in the table, so if we haven't found a user, we return a error, if we found one with the matching username, we check if the password provided matches along with the username, if the password is correct, we return a token which is something like a random piece of characters & numbers which is hard to guess which allows you to do anything including with the API itself (when sending requests manually), if not, we return an error that the password is incorrect:

```js
prisma.user.findUnique({
        where: {
            username: username
        }
    }).then(user => {
        if (user) {
            if (user.password === password) {
                res.json({
                    message: 'User authenticated successfully',
                    userToken: user.token,
                    user: username
                });
            } else {
                res.status(400).json({
                    message: 'Incorrect password'
                });
            }
        } else {
            res.status(400).json({
                message: 'No user found'
            });
        }
    }
    );
```

Now, let's make the fun..... start! Create a new file called `create.js` which will allow the user to create new tasks! Paste the following code into the file:

```js
import { PrismaClient } from '@prisma/client';

export default function handler(req, res) {
    const prisma = new PrismaClient();
    const { token, taskTitle } = req.body;
    if (!token || !taskTitle) {
        res.status(400).json({
            message: 'Missing token or task title'
        });
        return;
    }
    prisma.user.findUnique({
        where: {
            token: token
        }
    }).then(user => {
        if (user) {
            prisma.task.create({
                data: {
                    title: taskTitle,
                    userToken: token
                }
            }).then(task => {
                res.json({
                    message: 'Task created successfully',
                });
            });
        } else {
            res.status(400).json({
                message: 'No user found'
            });
        }
    }
    );
}
```

Simply skipping defining the ***Prisma client***, so we use `findUnique` to check the user token if valid or not, if it's not, we pass an error saying that there is no such user, if the user exists, we create a task with the title given and with that token, and then we return a success message:

```js
    prisma.user.findUnique({
        where: {
            token: token
        }
    }).then(user => {
        if (user) {
            prisma.task.create({
                data: {
                    title: taskTitle,
                    userToken: token
                }
            }).then(task => {
                res.json({
                    message: 'Task created successfully',
                });
            });
        } else {
            res.status(400).json({
                message: 'No user found'
            });
        }
    }
    );
```

Now if we assume someone wants to delete a task? Create `delete.js` and paste the following:

```js
import { PrismaClient } from '@prisma/client';

export default function handler(req, res) {
    const prisma = new PrismaClient();
    const { token, taskId } = req.body;
    if (!token || !taskId) {
        res.status(400).json({
            message: 'Missing token or task id'
        });
        return;
    }
    prisma.user.findUnique({
        where: {
            token: token
        }
    }).then(user => {
        if (user) {
            prisma.task.findUnique({
                where: {
                    id: taskId
                }
            }).then(task => {
                if (task.userToken === token) {
                    prisma.task.delete({
                        where: {
                            id: taskId
                        }
                    }).then(task => {
                        res.json({
                            message: 'Task deleted successfully',
                        });
                    });
                } else {
                    res.status(400).json({
                        message: 'Task does not belong to the user'
                    });
                }
            }
            );
        } else {
            res.status(400).json({
                message: 'No user found'
            });
        }
    }
    );
}
```

So what we do is find the user using the token, if we didn't find the user, we return an error, if we found the user, we find the task using the ID, we check if the owner is matching, if so we delete it, if not, we return an error:

```js
    prisma.user.findUnique({
        where: {
            token: token
        }
    }).then(user => {
        if (user) {
            prisma.task.findUnique({
                where: {
                    id: taskId
                }
            }).then(task => {
                if (task.userToken === token) {
                    prisma.task.delete({
                        where: {
                            id: taskId
                        }
                    }).then(task => {
                        res.json({
                            message: 'Task deleted successfully',
                        });
                    });
                } else {
                    res.status(400).json({
                        message: 'Task does not belong to the user'
                    });
                }
            }
            );
        } else {
            res.status(400).json({
                message: 'No user found'
            });
        }
    }
    );
```

Last but not least the `view.js` file which allows the user to view the tasks:

```js
import { PrismaClient } from '@prisma/client';

export default function handler(req, res) {
    const prisma = new PrismaClient();
    const { token } = req.body;
    if (!token) {
        res.status(400).json({
            message: 'Missing token'
        });
        return;
    }
    prisma.user.findUnique({
        where: {
            token: token
        }
    }).then(user => {
        if (user) {
            prisma.task.findMany({
                where: {
                    userToken: token
                }
            }).then(tasks => {
                res.json({
                    message: 'Tasks retrieved successfully',
                    tasks: tasks
                });
            });
        } else {
            res.status(400).json({
                message: 'No user found'
            });
        }
    }
    );
}
```

So what we do here is find the user, if not found, we return an error, if we found the user, we return all the tasks corresponding to the user:

```js
    prisma.user.findUnique({
        where: {
            token: token
        }
    }).then(user => {
        if (user) {
            prisma.task.findMany({
                where: {
                    userToken: token
                }
            }).then(tasks => {
                res.json({
                    message: 'Tasks retrieved successfully',
                    tasks: tasks
                });
            });
        } else {
            res.status(400).json({
                message: 'No user found'
            });
        }
    }
    );
```

Now, we got our **API** ready after hard work 🥳!

## Creating our CLI

Run the following commands to get started:

```bash
mkdir todocli
cd todocli
npm init -y
```

Now create a `index.js` file and paste the following:

```js
#!/usr/bin/env node

var args = process.argv.slice(2);
var fs = require('fs');
var request = require('request');
command = args[0];

if (command == 'login') {
    options = {
        url: 'http://localhost:3000/api/login',
        method: 'POST',
        json: {
            username: args[1],
            password: args[2]
        }
    };
    request(options, function (error, response, body) {
        if (!error && response.statusCode == 200) {
            console.log(body.message);
            fs.writeFile('./token.txt', body.userToken, function (err) {
                if (err) {
                    return console.log(err);
                }
                console.log("Token saved successfully!");
            }
            );
        } else {
            console.log(body.message);
        }
    });
} else if (command == 'register') {
    options = {
        url: 'http://localhost:3000/api/register',
        method: 'POST',
        json: {
            username: args[1],
            password: args[2],
            token: Math.random().toString(36).substring(2, 15) + Math.random().toString(36).substring(2, 15)
        }
    };
    request(options, function (error, response, body) {
        if (!error && response.statusCode == 200) {
            console.log(body.message);
            // save token
            fs.writeFile('./token.txt', body.user.token, function (err) {
                if (err) {
                    return console.log(err);
                }
                console.log("Token saved successfully!");
            }
            );
        } else if (body.message=="Token already taken") {
            console.log("Please try registering again!")
        } else {
            console.log(body.message);
        }
    });
} else if (command == 'create') {
    options = {
        url: 'http://localhost:3000/api/create',
        method: 'POST',
        json: {
            taskTitle: args.slice(1).join(' '),
            token: fs.readFileSync('./token.txt', 'utf8')
        }
    };
    request(options, function (error, response, body) {
        if (!error && response.statusCode == 200) {
            console.log(body.message);
        } else {
            console.log(body.message);
        }
    });
} else if (command == 'view') {
    options = {
        url: 'http://localhost:3000/api/view',
        method: 'POST',
        json: {
            token: fs.readFileSync('./token.txt', 'utf8')
        }
    };
    request(options, function (error, response, body) {
        if (!error && response.statusCode == 200) {
            // save the title and id of each task in an array
            var tasks = [];
            for (var i = 0; i < body.tasks.length; i++) {
                tasks.push({
                    id: body.tasks[i].id,
                    title: body.tasks[i].title
                });
            }
            // print the tasks along with their ids
            console.log("Your tasks are:");
            for (var i = 0; i < tasks.length; i++) {
                console.log(tasks[i].id + ": " + tasks[i].title);
            }

        } else {
            console.log(body.message);
        }
    });
} else if (command == 'delete') {
    options = {
        url: 'http://localhost:3000/api/delete',
        method: 'POST',
        json: {
            taskId: args[1],
            token: fs.readFileSync('./token.txt', 'utf8')
        }
    };
    request(options, function (error, response, body) {
        if (!error && response.statusCode == 200) {
            console.log(body.message);
        } else {
            console.log(body.message);
        }
    });
} else if (command == 'help') {
    console.log("Usage: todocli <command> <arguments>");
    console.log("Commands:");
    console.log("login <username> <password>");
    console.log("register <username> <password>");
    console.log("create <task title>");
    console.log("view");
    console.log("delete <task id>");
    console.log("help");
}
```

Simply what we are mainly doing is getting the parameters and depending on the API, and the token is saved into a `txt` file locally. 

Now install a required package using `npm install request`

Now edit your `package.json` and replace your `scripts`, paste the following:

```json
  "scripts": {
    "start": "node index.js"
  },
  "bin": {
    "todocli": "index.js"
  }
```

Your `package.json` should now look like this:

```json
{
  "name": "todocli",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "bin": {
    "todocli": "index.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "request": "^2.88.2"
  }
}
```

Now we are done, do `npm install . -g` and start using the app!

## Test it out - No setup needed

Just install `to-do-cli-prisma` with the command:

```bash
npm i to-do-cli-prisma
```

And check how to use it with the command: `todocli help`

## Important links 🔗

- **GitHub Repo** - [Omar8345/to-do-list-app-cli](https://github.com/Omar8345/to-do-list-app-cli)
- **npm Package** - [to-do-cli-prisma](https://www.npmjs.com/package/to-do-cli-prisma)

Thanks for reading this article and hope you learned something useful!