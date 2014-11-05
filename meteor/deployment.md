# Deployment for Meteor

### Requirements
* Virtual Servers for Cloud (EC2 Instance)
* Meteor Apllication
* Meteor Up  
* Nginx
* kadira

#### Virtual Servers for Cloud (EC2 Instance)

###### Create Instance
* Login in your Amazon Account @ https://aws.amazon.com/ .
* Click `EC2 icon` in the Amazon Web Services dashboard.
* Click `Launch Instance` under the Create Instance topic.
* Click select `Ubuntu Server 14.04 LTS (HVM), SSD Volume Type` to select our server(instance in ec2).
* Click the disired `Instance Type`. I prefered `t2.micro type`.
* Review `Configure Instance Details` if you think the instance detail is good then procced to review and lunch. 
* Review `Review Instance Launch` then click `Launch` then a pop up will appear `Select an existing key pair or create a new key pair`.
  Under the `Choose an existing key pair` choose `create a new key pair`.
* Create a new `Key pair name`.
* Download the `Key pair`. Dont loose this key pair you will use it to connect your server.

#### Meteor Up

###### Installation
	```
	npm install -g mup
	```
###### Creating a Meteor Up Project
	```
	mkdir ~/my-meteor-deployment
	cd ~/my-meteor-deployment
	mup init
	```

###### Setup your Deployment script
In your `my-meteor-deployment` directory edit the `mup.json` to this format below
```
{
  // Server authentication info
  "servers": [
    {
      "host": "hostname",
      "username": "root",
      "password": "password"
      // or pem file (ssh based authentication)
      // WARNING: Keys protected by a passphrase are not supported
      //"pem": "~/.ssh/id_rsa"
      // Also, for non-standard ssh port use this
      //"sshOptions": { "Port" : 49154 }
    }
  ],

  // Install MongoDB on the server. Does not destroy the local MongoDB on future setups
  "setupMongo": true,

  // WARNING: Node.js is required! Only skip if you already have Node.js installed on server.
  "setupNode": true,

  // WARNING: nodeVersion defaults to 0.10.31 if omitted. Do not use v, just the version number.
  "nodeVersion": "0.10.31",

  // Install PhantomJS on the server
  "setupPhantom": true,

  // Application name (no spaces).
  "appName": "meteor",

  // Location of app (local directory). This can reference '~' as the users home directory.
  // i.e., "app": "~/Meteor/my-app",
  // This is the same as the line below.
  "app": "/Your/meteor/app/directory",

  // Configure environment
  "env": {
    "PORT": 80,
    "ROOT_URL": "http://myapp.com",
    "Mongo_URL": "mongodb://localhost:27017/mixlinDB"
    "MAIL_URL": "smtp://postmaster%40myapp.mailgun.org:adj87sjhd7s@smtp.mailgun.org:587/"
  },

  // Meteor Up checks if the app comes online just after the deployment.
  // Before mup checks that, it will wait for the number of seconds configured below.
  "deployCheckWaitTime": 15
}
```

###### Setting Up a Server
	This will setup the server for the mup deployments.
	```
	mup setup
	```

###### Deploying an App
	This will bundle the Meteor project and deploy it to the server.
	```
	mup deploy

	```