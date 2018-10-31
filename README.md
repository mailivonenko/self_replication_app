# Self-replicating app
Self-replicating app creates a `self_replication_app` repository in user's GitHub account with its own code.

<b>instructions.md</b> contains instructions on how to launch the application and get a working URL that replicates the repository.


Flask is used for web app logic implementation

Github OAuth APP is used for Github API authorization

PyGithub lib is used as a github api wrapper

Heroku is used to host the web app

App flow:
- Login: user is redirected to the Github auth page for login
- After login user can see a welcome page with the link for replicating the self_replication_app to his own Github account
- Once replicated the lis of files with statuses can be viewed

