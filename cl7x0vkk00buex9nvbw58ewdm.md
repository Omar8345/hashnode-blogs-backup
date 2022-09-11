## Convert Figma components to React (Next.js) components

Hallo! Wie geht's? ("Hello, how are you?" in German)

Hoping you are having a fruitful day, today we'll convert **[Figma](https://figma.com)** components to *React* (**Next.js**) components! Which is a super time-saver ✨.

Let's go!

## 1 - Creating an Amplify project

Go to the [**AWS Amplify** page](https://aws.amazon.com/pm/amplify/) and click on **Build an app with AWS Amplify**. If required, sign in/sign up for an **AWS** account, after that, set the app name to your preferred name and click **Confirm Deployment**.

## 2 - Creating our Figma

Open the [**Figma Community Site**](https://figma.com/community) and search for *AWS Amplify UI Kit* and use the original one made by **AWS Amplify**, or use this direct link:

[AWS Amplify UI Kit - On Figma](https://www.figma.com/community/file/1047600760128127424)

Click the **Duplicate** button and edit the sample components as your needs.

## 3 - Import Figma components to AWS Amplify Studio

On the sidebar in the studio, click **UI Library** and click on **Get Started** and paste the **Figma file you duplicated** and continue.

Then you will get all the components, where you can accept/reject every component alone, or only accept all.

## 4 - Setup Next.js with the Amplify dependencies

In your terminal, run:

```bash
npx create-next-app figma-to-next
```

Now, just to make sure the app is working, run:

```bash
npm run dev
```

And check `localhost:3000`, now, the app is working, let's install a few things before importing the components from Amplify:

```bash
npm i aws-amplify @aws-amplify/ui-react
```

Now, also a requirement, be sure that you got Amplify CLI installed on your system, to verify that, run:

```bash
amplify -v
```

## 5 - Import the components from Amplify to Next.js

Open the studio and click **Local Setup Instructions** and copy the command, and run it in your Next.js project's root folder, now let's check if the components have been imported by running the following simple command:

```bash
ls -la ui-components
```

Now, you're all done! You can now use your components which are made using Figma in React/Next.js! 

Have a nice day ✨! See you!