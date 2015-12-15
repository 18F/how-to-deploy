## How to deploy it to Cloud Foundry

This is a repository of guides on how to deploy popular open source projects
to Cloud Foundry.

## Common pre-requisites

1. A Cloud Foundry account.
1. The [CF cli](https://github.com/cloudfoundry/cli#downloads).
1. Access to services for persistence.

## Ideas on how to get started

1. Search online first to see if there is a guide for "how to deploy x to Cloud Foundry"
1. Search the same but use "heroku" instead of "Cloud Foundry" most of the time
the deployment is similar


## How to contribute

There are multiple CF flavors and not all installations are exactly the same so
when sending a pull request please try to keep it as agnostic as possible.

1. Create a directory with the name of the project you want to deploy.
1. Add a `README.md` file with the main instructions for deployment.
1. If there are any files required, please create a `files` sub-directory with them.
