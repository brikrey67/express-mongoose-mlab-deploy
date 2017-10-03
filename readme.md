# Deploying Node-Express-Mongo Apps to Heroku

Deploying our Node-Express-Mongoose application (our APIs) consists of 2 sets of steps. First, we'll set up a Mongo database that our Node-Express-Mongoose back-end can connect to, and then configure our Node-Express-Mongoose applications (our APIs) to connect to this new cloud-hosted database.

## [Set Up Your Cloud-Based Mongo Database](./mongodb.md)

Clicking the link in the header above will take you to a set of instructions for setting up a cloud-hosted (via AWS) Mongo database you can use in your deployed Heroku application.

## First Steps with Heroku

Following Heroku's **[Getting Started with Node.js](https://devcenter.heroku.com/articles/getting-started-with-nodejs)** guide takes care of many deployment issues most of you will encounter, and give you a sense of how to use Heroku's deployment environment and features. Take particular note of...

* [Define a Procfile](https://devcenter.heroku.com/articles/getting-started-with-nodejs#define-a-procfile).
* [Provision a database](https://devcenter.heroku.com/articles/getting-started-with-nodejs#provision-a-database).
* If you've been storing API keys as environment variables locally, [define config vars](https://devcenter.heroku.com/articles/getting-started-with-nodejs#define-config-vars).

Speaking of config vars, [using `dotenv` to store sensitive information in the environment](https://github.com/motdotla/dotenv) is a fantastic practice, and accords with 12-factor principles.
    > After reading documentation, make sure you add `.env` to your `.gitignore` file, since `.env` will contain the sensitive data you **don't want under version control***.

## Google Is Your Best Friend

More often that not, solving deployment issues requires a good deal of Googling. Don't expect to find a silver bullet -- often we must go through many different issues other users may have encountered to understand our own.

What should you Google?
* If you aren't able to deploy, Google the error that shows up in your terminal after trying to push your app.
* If you are able to deploy but your app doesn't load/function propertly, see what shows up after running `$ heroku logs` in the Terminal.

## Help Each Other Out

If you notice somebody running into the same problem as you, try working together on debugging it!
