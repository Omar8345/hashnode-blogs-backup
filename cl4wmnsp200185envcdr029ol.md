## My review for the Craft Conference 2022

## My review for the Craft Conference 2022

I am Omar. A certified software developer and a designer.  I have taken many programming courses and I am experienced in many popular programming languages including **Python, Java, and JavaScript**.

Craft Conference 2022 was one of the conferences I enjoyed where I learned many things, one of my favourite talks was from Debbie O'Brien, who works [at] Microsoft as a Senior Program Manager where she talked about Testing Web Applications with Playwright and how to make automatic easy tests in no time without making it hard on you, taking a long time even to learn how and build, and so much on, so that's Playwright.



## Testing Web Applications with Playwright - Debbie O'Brien, Microsoft

Debbie O'Brien from Microsoft spoke about Java, Dot Net and Python. Testing is hard, testing takes time to learn and to write, and time is money. As developers, we want to test. We know we should but we don't have time. So how can we get more developers to do testing? We can create better tools. Let me introduce you to Playwright - Reliable end-to-end cross-browser testing for modern web apps, by Microsoft and fully open source. Playwright's Codegen generates tests for you in JavaScript, TypeScript, Dot Net, Java or Python. Now you have no excuses. It's time to use Playwright.

I didn't know anything about Playwright. I learned that it's okay not to test your application because it's hard, takes time to build and learn, and takes a long time. So that's why Playwright is the solution to test the web applications. It's easy with Playwright to test web applications, it is an end-to-end testing tool and it runs on almost all browsers, Chromium, and more.

I learned Playwright it's better because it works with any browser, any platform, one API, fast execution and more.

How I can get started with Playwright is simple is just as follows:

```bash
# Run from your project's root directory
npm init playwright@latest
# Or create a new project
npm init playwright@latest new-project
```

Also, the thing that I liked is that there is a **VS Code** extension for Playwright which has a UI so it would be easy to use 😎. 

I will be also writing a summary of how to make your first test. After the installation in your browser, just by clicking `F1`, you will get a `package.json`, `playwright.config.ts`, and `Tests` folder with an example test file. If you don't have an existing project, you can use the To-Do template!

What's also great is Codegen which generates tests by recording your actions. You can run it using `npx playwright codegen` which then will open 2 windows with a browser window and the tests, also the tests support multiple languages, including Java, JavaScript, Python, and C#.

What about running tests? You can run all tests, a set of tests, or a single test. Or you can even make tests run in parallel and it's super fast 🚀! 

You can run tests in **Headless** or **Headed**:

```bash
# headless
npx playwright test
# headed
npx playwright test --headed
```

What about breaking tests? It's recommended to break tests to check if they are working. As an example, I was using a **locator** in a t-shirt online store, there is (Women, Men, and Children) if you try to locate `Men`, Playwright isn't sure what you want to exactly approach, because also the word `Men` is in `Women` because it's so strict, so we need to mention **exactly `Men`, no any letter missing and no any letter is extra**!

Locators are a way to find element(s) on the page at any moment with built-in auto-waiting and retry-ability, they are like the pins on a map. Here is how to make/use a locator:


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656055107266/FJV95_mQL.png align="left")

Running debug mode:

~~~bash
npx playwright test --debug
~~~

If you would like to have better errors details, this is for the terminal, if you are using the extension in **VS Code, it's as follows**:

Just make a breakpoint where you want to stop your code and click on the green check mark and click **Debug Test**.

We can show reports using the command:

```bash
npx playwright show-report
```

This is an report example in **Chromium**:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656055687150/7YOyhCrIh.png align="left")

Let's talk about tracing files, if you want to record a trace for each test, normally it's on if it's a broken test, but you can manually turn it on by mentioning the following:

~~~js
trace: 'on'
~~~

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656055817258/kL2saIRQX.png align="left")

What it does is if you go to your report, at the bottom you will get an image, a trace `.zip` file.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656055889978/w6pLzAFtG.png align="left")

Or you can just click and it'll open it up.

## My review's summary

To pack up, **Playwright** is an amazing way to test your applications in no time seamlessly as it supports many programming languages including **Java, JavaScript, Python, and C#**. Also, there is a **Visual Studio Code extension for Playwright!** You can make a breakpoint and run your test in **debug mode**.

I also tried to use it with **[CodeGuard](https://omardevblog.toolsandapps4us.site/codeguard)** which is my submission for the **Hashnode X Linode Hackathon** and I found some bugs, errors, etc. which I fixed in **release version 1.1** which has been just released yesterday, and announced today on the submission article. Since then, my project **CodeGuard** for the Hashnode X Linode Hackathon got better because I used **Playwright** to test my application/project **CodeGuard** and find errors which sometimes are "**behind the scenes**" which is called the back-end!


I also benefited a lot from breaking my tests by making breakpoints and running in debug mode. And I had been using **Playwright** since then in all my projects, even if it's a personal one, but why not if it's all automated 🚀😎. You can use **Playwright** with any browser which is great and even get a trace in a `.zip` file!



I learned a lot and it was really useful I hope to continue using **Playwright**!

## Special thanks 🚀

Special thanks to Craft Conf for providing me with this complimentary ticket to attend the conference, I learned a lot!

Also thanks to you @[Miki Szeles](@mszeles) for providing me with this awesome opportunity!