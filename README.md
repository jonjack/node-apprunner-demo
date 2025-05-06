# Node app - App Runner - Amazon Q

I was struggling to get a Node app running in a Docker container on APP Runner so i asked Amazon Q for step by step instrucitons on how to build and deploy a Hello World app.

I would like to create a Node.js application that runs in a Docker container on AWS App Runner. Can you help me create the project files?

Certainly! I'd be happy to help you create a Node.js application that runs in a Docker container on AWS App Runner. Here's a step-by-step guide to create the project files: [1]

Create a new directory for your project and navigate to it:

```sh
mkdir node-apprunner-demo
cd node-apprunner-demo
```

Initialize a new Node.js project:

```sh
npm init -y
```

Install Express.js (a popular web framework for Node.js): [2]

```sh
npm install express
```

Create a file named app.js with the following content:

```sh
const express = require('express');
const app = express();
const port = process.env.PORT || 3000;

app.get('/', (req, res) =&gt; {
  res.send('Hello from AWS App Runner!');
});

app.listen(port, () =&gt; {
  console.log(`App listening at http://localhost:${port}`);
});
```

Create a Dockerfile in the project root:

```sh
FROM node:14

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD [ "node", "app.js" ]
```

Create an apprunner.yaml file in the project root:

```sh
version: 1.0
runtime: nodejs14
build:
  commands:
    - npm install
run:
  command: node app.js
  network:
    port: 3000
```

Create a .gitignore file:

```sh
node_modules/
```

Initialize a Git repository:

```sh
git init
git add .
git commit -m "Initial commit"
```

These files set up a basic Node.js application that can be deployed to AWS App Runner. The app.js file contains a simple Express.js server, the Dockerfile defines how to build the container image, and the apprunner.yaml file provides configuration for App Runner.

To deploy this application:

Push your code to a Git repository (e.g., GitHub, CodeCommit).
In the AWS Console, navigate to App Runner and create a new service.
Choose your source repository and branch.
Select "Auto-detect" for the runtime, which will use the apprunner.yaml file.
Configure any additional settings as needed.
Deploy the application.
App Runner will build the container image using your Dockerfile, deploy it, and provide you with a URL where your application is accessible.

Remember to follow AWS security best practices, such as using least privilege permissions for your App Runner service and enabling HTTPS for your application. Also, consider setting up monitoring and logging using Amazon CloudWatch to keep track of your application's performance and any potential issues.
