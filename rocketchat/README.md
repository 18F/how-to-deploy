# How to deploy [RocketChat](https://github.com/RocketChat/Rocket.Chat) to Cloud Foundry

## Steps:
- Run `git clone https://github.com/RocketChat/Rocket.Chat`
- cd into `Rocket.Chat`
- cf push <YOUR APP NAME> -b https://github.com/cloudfoundry-community/cf-meteor-buildpack.git --no-start
- cf marketplace
- Get the name of your MONGO_DB service name
- `cf create-service <YOUR MONGO DB SERVICE NAME> <YOUR SERVICE NAME PLAN> <THE MONGODB NAME YOU CHOOSE>`
- `cf bind-service <YOUR APP NAME> <THE MONGODB NAME YOU CHOOSE>`
- `cf start <YOUR APP NAME>`
