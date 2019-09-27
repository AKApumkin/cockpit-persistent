# Cockpit docker-compose
This repo contains the docker-compose build of Cockpit with persistent data from the storage folder that will be mapped locally. 

This image also has 2 addons from the community:
1. https://github.com/agentejo/CloudStorage -> This addon provides access to AWS, Azure or Google Cloud storage for assets. The config files are located on the git repo, to add them, once you have logged into the cockpit control panel after installation go to the settings and add the necessary lines to the config.yaml file.

2. https://github.com/pauloamgomes/CockpitCMS-Moderation -> This adds draft mode to your collections, watch the video at the bottom of the repo for a full explanation. no need for any configuration. 


## Start
`docker-compose up -d` 

## Run the installation for Cockpit 
http://localhost:8080/install 

## Enjoy 
As a note the storage folder holds the object information that is also required during a migration. 


