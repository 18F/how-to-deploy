## How to deploy Sentry to Cloud Foundry

### What is Sentry?

Sentry is a real-time crash reporting tool that can work with multiple frameworks.

Learn more: [https://www.getsentry.com/welcome/]()  
Github link: [https://github.com/getsentry/sentry]()

### Getting Started

Sentry is releases as a Python pip package. We will use the Python buildpack,
the pip package and add some configuration files to deploy the app.

There is an open source project to deploy Sentry to Heroku here:
[https://github.com/fastmonkeys/sentry-on-heroku](). That project was forked to
create [https://github.com/dlapiduz/sentry-on-cf]().

### Steps

1. Target the space in Cloud Foundry that you want to deploy your app to:  
For example: `cf target -o sentry -s sentry`
1. Clone the `sentry-on-cf` repo:  
`git clone https://github.com/dlapiduz/sentry-on-cf`
1. Edit the `manifest.yml` file to match your desired `host` and `domain`.
1. Push the application without starting it to create the environment:  
  `cf push --no-start`
1. Create a postgres database service instance and bind it:  
  For example: `cf create-service rds shared-psql sentrydb`  
  `cf bind-service sentry sentrydb`
1. Create a redis service instance and bind it:  
  For example: `cf create-service redis28-swarm standard sentryredis`  
  `cf bind-service sentry sentryredis`
1. Add the services to your `manifest.yml` file:  

  ```
  ...
  services:
  - sentrydb
  - sentryredis
  ...
  ```
1. Get the Redis URL from the app environment and take note of it:
  `cf env sentry`
1. Set required environment variables in your `manifes.yml` file:  
  (use the Redis settings from the previous step to set REDIS_URL)  

  ```
  env:
    SENTRY_URL_PREFIX: my-sentry.apps.com
    REDIS_URL: redis://dummy:password@1.1.1.1:12345
    SECRET_KEY: secretkeyshhh
    SENTRY_ADMIN_EMAIL: myemail@email.com
    SERVER_EMAIL: theserver@email.com
    MANDRILL_USERNAME:  
    MANDRILL_APIKEY:  
  ```
1. Run `cf-ssh` to ssh into a container to run admin tasks (this might take a while)
1. Once in the container terminal run:  

  ```
  # Fill in the DB
  sentry --config=sentry.conf.py upgrade --noinput
  # Create an account (say yes to superuser)
  sentry --config=sentry.conf.py createuser
  ```
1. Do one more `cf push` to make sure all the apps are up and running

And you should have a working Sentry installation!
