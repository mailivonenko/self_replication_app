# Installation document containing instructions on how to launch the application and get a working URL that replicates the repository.

This  instruction is designed for a case when the app is hosted on heroku cloud platform.

# Sign up for Heroku
First go to the [https://www.heroku.com](https://www.heroku.com) and create an account.

## Download the Heroku CLI
Heroku has a command-line interface that is used to simplify our communication with the Heroku servers.
You can install it by next link: [https://devcenter.heroku.com/articles/heroku-cli](https://devcenter.heroku.com/articles/heroku-cli)

## Authenticate with Heroku with `heroku login`
Installing the Heroku CLI will give you access to the `heroku` command which has several subcommands for interacting with the Heroku service. 

The first command you need to run is `heroku login`, which will ask you to enter your login credentials so that every subsequent `heroku` command knows who you are:

~~~sh
$ heroku login
~~~

# Let's get the Flaks app code
To clone the application so that you have a local version of the code that you can then deploy to Heroku, execute the following commands in your local command shell or terminal:

~~~sh
git clone https://github.com/DanyloAntsybor/self_replication_app.git
cd self_replication_app
~~~

You now have a functioning git repository that contains an application code. Double check a runtime.txt and a requirements.txt, which is used by Python’s dependency manager, Pip.

# Deploy the app to heroku

In this step you will deploy the app to Heroku.

Create an app on Heroku, which prepares Heroku to receive your source code:
~~~sh
heroku create
~~~

When you create an app, a git remote (called heroku) is also created and associated with your local git repository.

Heroku generates a random name for your app (you also can pass a parameter to specify your own app name).
Copy this app name so it is then can be used with OAuth App on the Github


Now deploy your code:
~~~sh
git push heroku master
~~~

The application is now deployed. Ensure that at least one instance of the app is running:
~~~sh
heroku ps:scale web=1
~~~

#Create OAuth App on the Github
To launch the application by your own you need to go to the Github developers settings and create a New OAuth App:
https://github.com/settings/developers

Put some meaningful name.
For Homepage URL put the application url generate by heroku: your_heroku_app_url
For Authorization callback URL put: your_heroku_app_url/login/authorized

Once Github OAuth App is created you will see __Cliend ID__ and __Client Secret__ that we will to app to execute.

#Add Heroku environmnetal variables for application
To launch the application you need to set next environmnetal variables: `SESSION_SECRET_KEY`, `GITHUB_CLIENT_SECRET`, `GITHUB_CLIENT_ID`

Where the `SESSION_SECRET_KEY` is a secret key for a session. You can use some random generator to put this.
Example: python -c 'import os; print(os.urandom(16))'

`GITHUB_CLIENT_SECRET`, `GITHUB_CLIENT_ID` should be coppied from the previous point after Github OAuth App creation.

~~~sh
heroku config:set SESSION_SECRET_KEY=your_generated_secret_key
heroku config:set GITHUB_CLIENT_SECRET=your_github_app_client_secret
heroku config:set GITHUB_CLIENT_ID=your_github_app_client_id
~~~

Now the application is ready so you can check it by going the app link in your browser.

## logs checks
In case of any issues you can view heroku logs using above command
~~~sh
heroku logs --tail
~~~



 