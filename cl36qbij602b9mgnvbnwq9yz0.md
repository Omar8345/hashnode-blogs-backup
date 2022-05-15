## Introducing Supabase: The new open-source Firebase alternative

**Supabase?** The open-source **Firebase** alternative?!

This is an **Extra Ordinary Claim because it requires Extra Ordinary Evidence**

"Supabase VS Firebase"

## Supabase VS Firebase

### 1. Features

| Supabase | Firebase |
| -------- | -------- |
| Database | Database |
| Authentication | Authentication |
| Storage | Storage |
| Functions | Functions |
|      | Hosting |
| | Analytics |
| | Crashlytics |
| | ML |
| | Push notifications |
| | Remote config |

This isn't completely a fair comparison because **Supabase** is still new, but **Firebase** has been here for a long time!

There is one **great** fact which is about **Supabase**. What's it?

**Supabase** uses open-source technologies for it's platform, what does it mean?

It means that you can **run Supabase with Docker, and you can *host your own Firebase alternative on AWS (recommended) or any other cloud platform.***

### 2. Policies

When you use **Firebase**, you are locked in with **Google**, as you are signing a contract with the **Alphabet** cooperation by giving them the power to destroy your business at any moment if they decide that's what should happen. Proof as in the following picture:


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652526710954/NwYSWMEFl.png align="left")

Source: [**Firebase Paid Services Terms of Service**](https://firebase.google.com/terms/billing)

Let's look now to **S**upabase features to see how they stack-up in front of **F**irebase...

### User Authentication

Before we start, **S**upabase isn't a 1-to-1 mapping of **F**irebase. It just provides the tools which approximately do the same thing. I have made a demo using **S**upabase and I would like to tell you that the developer experience is similar to **F**irebase. The only thing **S**upabase is missing is phone authentication. Now, in the actual code, you can get a user logged in with one or two lines of code like **F**irebase, I do like that **S**upabase returns an error as an object, because in **F**irebase you should wrap it in a try catch block to catch errors.

### Security

One thing cool that **S**upabase does but **F**irebase doesn't is that automatically create a database record for the user.

### Database

We haven't talked about database yet. In **F**irebase we have 2 different database options but we'll be focusing on **F**irestore which is very similar to **MongoDB** and it is a **NoSQL** document database. It is very easy to work with scales automatically and it automatically handles relational data fairly well. However, it's not ideal for graphs and full-text search.

**S**upabase uses **PostgreSQL** as it's database, a relational SQL database that has been around forever. But SQL databases are expensive, hard to use, and difficult to scale. **S**upabase offers you handling the scaling for you automatically and also by providing a dashboard and SDK to make working with the database much easier.

### Realtime

If you are building a realtime app, you can do so with one line of code with very little configuration with **F**irebase. The client-side SDKs are very sophisticated and do thing like optimistic updates where it updates the UI before the actual changes is committed to the back-end. It also supports offline mode.

In **S**upabase you can subscribe to real time updates that's pretty much it. Another issue that security policies will not work with real time data.

## Pricing

Both products has a free tier:

| **Supabase** | **Firebase** |
|---|---|
| 10K users | Unlimited users |
| 500 MB data | 1 GB data |
| FREE | FREE |

| **Supabase** | **Firebase** |
|---|---|
| **$25** per month for 7 | **$0.18** per GB |
| ***Unlimited API calls?!*** | **$0.06** per 100K reads |
| | **$0.18** per 100K writes |


| **Supabase** | **Firebase** |
|---|---|
| **$25** per month | **$0.18** per GB |
| **$0.125** per GB (*over 8 GB*) |

### The end 🎉

Hope the comparison was useful for you! Good bye!
