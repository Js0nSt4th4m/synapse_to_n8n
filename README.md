# Synapse_to_n8n

Based on [matrix-bot-sdk](https://github.com/turt2live/matrix-bot-sdk-bot-template), synapse_to_n8n allow you to connect synapse to n8n, you will be able to make a command bot.

Here is the data modele of n8n input :

  {
	  "Room_ID": roomId,
	  "Sender": event.sender,
	  "Args": args
  }

# Running / Building

After clicking the 'use this template' button and cloning the repo, you'll need to install the dependencies to get started. This assumes you have at least NodeJS 14 or higher.

    Run npm install 

to get the dependencies.

To build it: 

 	npm run build

To run it: 

	npm run start:dev

To check the lint: 

	npm run lint

To build the Docker image: 

	docker build -t your-bot:latest

To run the Docker image (after building): 

	docker run --rm -it -v $(pwd)/config:/bot/config your-bot:latest 
 
 Note that this will require a config/production.yaml file to exist as the Docker container runs in production mode.

# Configuration

This template uses a package called config to manage configuration. The default configuration is offered as config/default.yaml. Copy/paste this to config/development.yaml and config/production.yaml and edit them accordingly for your environment.

Example :

	//Where the homeserver's Client-Server API is located. Typically this
	// is where clients would be connecting to in order to send messages.
	homeserverUrl: "https://matrix.org"
	
	// An access token for the bot to use. Learn how to get an access token
	// at https://t2bot.io/docs/access_tokens
	accessToken: "YOUR_TOKEN_HERE"
	
	// Whether or not to autojoin rooms when invited.
	autoJoin: true
	
	// Location on disk for where to store various bot information.
	dataPath: "storage"
	
	// Set to false to disable encryption support. Encrypted data will be
	// stored under dataPath.
	encryption: true
	
	// Ajouter l'url de votre webhook n8n
	n8n_webhook_url: ""

 # N8N Minimal WorkFlow

 ![image](https://github.com/user-attachments/assets/b85f41a2-b014-45f6-900f-19cdbc5e0720)

 Entry Point : WebHook node, it's where you will get the "n8n_webhook_url".

 Edit Fields node : It's where you will parse the webhook body.

 ![image](https://github.com/user-attachments/assets/943711f9-6b96-48ec-8ec6-3387260d3f44)

 Exit Point : Matrix node, it's will be used to send the response to the synapse server

# Get your access token 

To retrieve your access token by Login :

	import { MatrixAuth } from "matrix-bot-sdk";
	
	// This will be the URL where clients can reach your homeserver. Note that this might be different
	// from where the web/chat interface is hosted. The server must support password registration without
	// captcha or terms of service (public servers typically won't work).
	const homeserverUrl = "https://example.org";
	
	const auth = new MatrixAuth(homeserverUrl);
	const client = await auth.passwordLogin("username", "password");
	
	console.log("Copy this access token to your bot's config: ", client.accessToken);

 To retrieve your access token by Registration :

	 import { MatrixAuth } from "matrix-bot-sdk";
	
	// This will be the URL where clients can reach your homeserver. Note that this might be different
	// from where the web/chat interface is hosted. The server must support password registration without
	// captcha or terms of service (public servers typically won't work).
	const homeserverUrl = "https://example.org";
	
	const auth = new MatrixAuth(homeserverUrl);
	const client = await auth.passwordRegister("username", "password");
	
	console.log("Copy this access token to your bot's config: ", client.accessToken);

 Regarding the [matrix_bot_sdk](https://turt2live.github.io/matrix-bot-sdk/tutorial-bot.html)
