# Getting started with docker-compose, using python/flask & redis

Compose is a tool for defining and running multi-container Docker applications. You use a Compose file to configure your application’s services. Then using a single command, you create and start all the services.

In this repo, there is a basic python flask web app in `app.py`, a Dockerfile for the specs of the container for that app (which is based off a python image), a requirements file for Docker installation additional requirements for the app (flask, redis), and a docker-compose file for the specification of the composed containers which includes the flask and redis containers. I created this in conjunction with reading this docker-compose tutorial, so you can use it to get more information on what these files do, https://docs.docker.com/compose/gettingstarted/

To get the app running in Two container on Differrent ports with redis in another, try these steps:

1. Create the files locally. See if you can tell what each one does. Check the above link to learn more.

1. Run `docker-compose build' to build the containers specified in the docker-compose file.

1. Run `docker-compose up` to start the containers (add -d to run them in the background. Then run `docker-compose stop` when done.)  

1. Browse to http://localhost:5000 or http://localhost:5001 to see the response from the web app. 


# STEPS TO DEPLOY MY FLASK APP ON AWS ECS USING CLOUDFORMATION

1. First Created private repository under ECR with the name of "webapp-ecr-repo"

2. Log in to AWS ECR locally from your machine where aws-cli already configured with running following commands

		a) aws ecr get-login --no-include-email --region ap-south-1
		
		b) If you are using the AWS CLI, run the login command from the output of step a.
		
		c) Build your Docker image

		d) After the build completes, tag your image so you can push the image to this repository:

				docker tag webapp-ecr-repo:latest 451686571853.dkr.ecr.ap-south-1.amazonaws.com/webapp-ecr-repo:latest

		e) Run the following command to push this image to your newly created AWS repository:

				docker push 451686571853.dkr.ecr.ap-south-1.amazonaws.com/webapp-ecr-repo:latest

3. Go to Cloudformation service, click on create stack and upload json file "aws_ecs_app.json". Click on button Next

4. On Next page, Give Name stack of your choice and click on Next button.

5. Within few minutes stack going to deploy.

6. Once stack deployed, copy paste public IP of EC2 Instance on the browser and appliction will run.
