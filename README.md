## How to deploy it to Cloud Foundry

This is a repository of guides on how to deploy popular open source projects
to Cloud Foundry.

## Common pre-requisites

1. A Cloud Foundry account.
1. The (CF cli)[https://github.com/cloudfoundry/cli#downloads].
1. Access to services for persistence.

## How to contribute

There are multiple CF flavors and not all installations are exactly the same so
when sending a pull request please try to keep it as agnostic as possible.

1. Create a directory with the name of the project you want to deploy.
1. Add a `guide.md` file with the main instructions for deployment.
1. If there are any files required, please create a `files` sub-directory with them.
