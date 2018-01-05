# Deployment Node-Express-Mongoose

## Learning Objectives

- Define 'deployment'
- Describe the difference between development, test, and production environments
- Deploy a Node App using Heroku
- Set up a Mongoose database using MLab
- Describe the major points of a 12-factor application
- Use environmental variables to keep sensitive data out of code

## Framing

Deployment is the act of putting an app up on one or more internet-connected servers that allow users to access and use the app.

## About Deployment

> What is deployment? What changes in an application when it is deployed?

### Requirements for Deploying

There are generally a few things we need for an app to be properly deployed:

- **server** - the server(s) must be on and connected to the internet
- **services** - the server must be running the correct services (web, database, email, ect.)
- **dependencies** - the server(s) must have the proper dependencies installed
- **executable code** - we must get our code onto the server and be able to run it
- **configuration** - we must configure our running app with respect to its deployment environment

### Deployment Approaches

There are lots of ways to do each of these steps. For example, we can get our code onto a server by...

- Using FTP to transfer the files onto the server
- Adding a git remote and using git push to transmit files (like with GH pages)
- Putting the files on a flash drive, fastening it to a homing pigeon's leg, then having an operator receive the pigeon and copy the files over to the server

### Heroku

Today, we'll be using a service called Heroku to deploy our apps, because it makes all the above steps easy. For example, Heroku automatically does the following...

- starts up a new server when we run heroku create, and installs all the necessary services
- adds a new remote to our git repo, so we can just run git push heroku master to copy our code over
- detects our database
- detects the language our program is written in and chooses a buildpack
- automatically installs our app's dependancies, and starts our app
- easily change configuration information using heroku config

## Environments and Environmental Variables

### [You Do: Read about Environments](about-environments.md)

> 15 minutes

> Start by reading about environments. We've been using the `development` environment by default, now we'll look at other environments, particularly `production`.

### Environmental Variables

Node manages application environments using 'environmental variables'. Environmental variables store configuration information that is defined outside of your codebase. Storing this information separately protects sensitive information like API keys and passwords because it is not visible from your project directory.

This is accomplished using `process` a global object that comes with all node projects. `process` has property called `env` where we store environmental variables.

We can view a projects environmental variables using the node repl in our terminal.

```bash
$ cd <your-node-project>
$ node
> console.log(process.env)
```

You can create a new environmental variable in the terminal too!

```bash
$ export <YOUR-ENVIRONMENTAL_VARIABLE_NAME>=<variableValue>
```

> Environment variables tend to be ALL_CAPS_SNAKE_CASE by convention.

Try logging process.env.<YOUR-ENVIRONMENTAL_VARIABLE_NAME> from the node repl to test.

#### **Bonus: dotenv**

[dotenv](https://github.com/motdotla/dotenv) is a node package used to store sensitive information in the environment. It's a handy tool but not strictly necessary for this deployment. It is a fantastic practice, and accords with [12-factor principles](https://12factor.net/).
  > After reading documentation, make sure you add `.env` to your `.gitignore` file, since `.env` will contain the sensitive data you **don't want under version control***.

## Deploying Node-Express-Mongoose Apps

Deploying our Node-Express-Mongoose application (our APIs) consists of 2 sets of steps. First, we'll deploy our application to Heroku. Then we'll set up a Mongo database that our app can connect to. Finally, we'll configure our Node-Express-Mongoose applications (our APIs) to connect to this new cloud-hosted database.

## You Do: Deploy

> We'll use Heroku to deploy our app, since it has a "free" pricing tier, and a ton of nice features that simplify and expedite deployment.

1. Sign up for a free [Heroku](https://www.heroku.com/) account.

2. Follow the instructions [here](https://devcenter.heroku.com/articles/heroku-cli) to download the Heroku CLI.

3. [Set Up Your Cloud-Based Mongo Database](./mongodb.md)

> Clicking the link in the header above will take you to a set of instructions for setting up a cloud-hosted (via AWS) Mongo database you can use in your deployed Heroku application.

4. **Before** deploying to heroku you will need to make a minor change to `index.js`. When Heroku starts your app it will automatically assign a port to `process.env.PORT` (an environmental variable!) to be used in production. We can modify `app.listen` to accomodate Heroku's production port and our own local development port.

```js
  app.set('port', process.env.PORT || 3001)

  app.listen(app.get('port'), () => {
    console.log(`✅ PORT: ${app.get('port')} 🌟`)
  })
```

5. Follow Heroku's [Getting Started with Node.js](https://devcenter.heroku.com/articles/getting-started-with-nodejs) to deploy **When President** (if you don't have a working lab, use the 'express-mongoose-solution' branch). **Do not use the sample application provided by Heroku**

> Follow the deployment tutorial but **stop** after the 'Define a Procfile' step. Once you've deployed, read through the remaining steps to learn more about using Heroku and its features.

## Google Is Your Best Friend

More often that not, solving deployment issues requires a good deal of Googling. Don't expect to find a silver bullet -- often we must go through many different issues other users may have encountered to understand our own.

What should you Google?

- If you aren't able to deploy, Google the error that shows up in your terminal after trying to push your app.
- If you are able to deploy but your app doesn't load/function properly, see what shows up after running `$ heroku logs` in the Terminal.

## Help Each Other Out

If you notice somebody running into the same problem as you, try working together on debugging it!
