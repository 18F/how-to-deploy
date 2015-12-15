# How to deploy Hubot to Cloud Foundry for Slack

### WIP

These instructions come from the instructions for [hubot for slack](https://github.com/slackhq/hubot-slack)

## Getting Started

#### Creating a new bot

- `npm install -g hubot coffee-script yo generator-hubot`
- `mkdir -p /path/to/hubot`
- `cd /path/to/hubot`
- `yo hubot`
- `npm install hubot-slack --save`
- Initialize git and make your initial commit
- Check out the [hubot docs](https://github.com/github/hubot/tree/master/docs) for further guidance on how to build your bot

#### Testing your bot locally

- `HUBOT_SLACK_TOKEN=xoxb-1234-5678-91011-00e4dd ./bin/hubot --adapter slack`

#### Deploying to Cloud Foundry

- `cf push <YOUR_APPNAME>
- `cf set-env <YOUR_APPNAME> HUBOT_SLACK_TOKEN <TOKEN>`
- `cf restage <YOUR_APPNAME>

