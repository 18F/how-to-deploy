## How to deploy Mozaik to Cloud Foundry

### What is Mozaik?

Mozaik is a dashboarding tool. That lets you generate visual representations
for multiple data sources.

Learn more: [https://mozaik.rocks]()  
Github link: [https://github.com/plouc/mozaik]()

### Getting Started
We are going to deploy the demo for Mozaik. Once you deploy the demo you can change the config.json file to create your own dashboards.

### Steps

1. Download mozaik-demo:  
`git clone https://github.com/plouc/mozaik-demo && cd mozaik-demo`
1. Edit `package.json`, find `mozaik` in the `dependencies` section. Change the version to point to `git://github.com/arowla/mozaik.git`.
1. Edit `config.json` in the root directory and add the following to the `config` object:

  ```
  useWssConnection: true,
  wsPort: 4443, // This might be required depending on your Cloud Foundry setup
  ```

1. Npm install:  
`npm install`
1. Gulp build:  
`gulp build`
1. (Optionally) Ignore your `node_modules` in `.cfignore`:
`echo "node_modules" > .cfignore`
1. Push it to CF:
`cf push mozaik-demo`

Open `mozaik-demo.your_domain.com` and find your brand new mozaik!
