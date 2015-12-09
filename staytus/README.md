# [Staytus](http://staytus.co/)

Staytus is an open source status page. You can see the general [install instructions](https://github.com/adamcooke/staytus#installation-from-source), but the Cloud Foundry-specific instructions are:

1. Clone the repository:

    ```bash
    git clone https://github.com/adamcooke/staytus.git
    cd staytus
    ```

1. [Add the `rails_12factor` gem](https://github.com/heroku/rails_12factor#install) for better logging.
1. Create a MySQL database instance. On [cloud.gov](https://cloud.gov), this would look like:

    ```bash
    # create the MySQL service for ourselves
    cf create-service mysql56 free staytus-mysql

    # push the app but don't start it
    cf push staytus --no-start

    # bind the service to the app
    cf bind-service staytus staytus-mysql

    # start the app
    cf start staytus
    ```

1. Set up the database tables:

    ```bash
    # watch the logs
    cf logs staytus
    # in a separate terminal, set up the database
    cf push staytus -c "bundle exec rake db:migrate"
    ```

1. When the migration finishes (as seen in the logs), press `CONTROL-c` to stop `cf push` from waiting for the server to start.
1. Start the server:

    ```bash
    cf push staytus -c null
    ```

1. Open the site, and you should see the Staytus homepage.
1. Log in to the admin interface (`/admin`) with username `admin@example.com` and password `password`. <!-- per https://github.com/adamcooke/staytus/blob/master/db/seeds.rb -->

## Configure SMTP

To send notifications to "subscribers", you will need to set up an SMTP service. You will need to set the environment variables:

```bash
cf set-env staytus STAYTUS_SMTP_HOSTNAME <HOST>
cf set-env staytus STAYTUS_SMTP_USERNAME <USER>
cf set-env staytus STAYTUS_SMTP_PASSWORD <PASS>
cf restage staytus
```

or modify [`config/initializers/smtp.rb`](https://github.com/adamcooke/staytus/blob/master/config/initializers/smtp.rb) if you need [additional settings](http://guides.rubyonrails.org/configuring.html#configuring-action-mailer).
