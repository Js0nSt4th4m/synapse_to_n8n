# synapse_to_n8n

Based on [matrix-bot-sdk](https://github.com/turt2live/matrix-bot-sdk-bot-template), synapse_to_n8n allow you to connect synapse to n8n, you will be able to make a command bot.

Here is the data modele of n8n input :

  {
	  "Room_ID": roomId,
	  "Sender": event.sender,
	  "Args": args
  }

# Running / Building

After clicking the 'use this template' button and cloning the repo, you'll need to install the dependencies to get started. This assumes you have at least NodeJS 14 or higher.

    Replace this README with something useful.
    Update your project's details in package.json.
    Run npm install to get the dependencies.

To build it: npm run build.

To run it: npm run start:dev

To check the lint: npm run lint

To build the Docker image: docker build -t your-bot:latest .

To run the Docker image (after building): docker run --rm -it -v $(pwd)/config:/bot/config your-bot:latest Note that this will require a config/production.yaml file to exist as the Docker container runs in production mode.

# Configuration

This template uses a package called config to manage configuration. The default configuration is offered as config/default.yaml. Copy/paste this to config/development.yaml and config/production.yaml and edit them accordingly for your environment.
