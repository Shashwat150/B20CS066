# Shashwat Singh(B20CS066)  -- Author

Overview: 
          
    -> Creating a simple web application

	  -> Testing the application locally.
        
	  -> Packaging the locally made application into its own docker image.

=> Simple Web Application
--------------------------
- I have a created a basic Node.js application using the Express.js framework to create a simple web server that listens on port 4000 and prints "Hello World" when we access the root path in our browser.
- In the code of index.js,I have imported the Express.js framework and created an instance of the Express application.
- The constant port is set to 4000, on which the server will listen.
- Defined a route handler for the root path("/"). When a GET request is made to the root path, the server responds with "Hello World".


=> Testing the application locally.
------------------------------------
- Just run the "index.js" file and the application will start listening.
- When we access the root path in our browser (e.g., http://localhost:4000), it will respond with "Hello World".


=> Packaging the locally made application into its own docker image.
---------------------------------------------------------------------

```
FROM node:20-alpine
WORKDIR /app
ADD package*.json ./
RUN npm install
ADD index.js ./
CMD [ "node", "index.js"]
```

- I have created a Dockerfile, which is a blueprint to create our own docker images.
- `FROM node:20-alpine`: This sets the base image for your Docker container. It uses the node:20-alpine image as the starting point, which is based on Alpine Linux and includes Node.js version 20.
- `WORKDIR /app`: This instruction sets the working directory within the container to /app.
- `ADD package*.json ./`: This copies the package.json and package-lock.json from your local machine to the /app directory in the container. These files are needed for installing the application's 
  dependencies.
- `RUN npm install`: This runs the npm install command inside the container, which installs the Node.js dependencies listed in our package.json file. This step is essential to set up our application.
- `ADD index.js ./`: This adds our index file to the working directory.
- `CMD ["node", "index.js"]` :used to define the command that will be executed when the container starts. It allows you to specify the default command that should be run.
- ["node", "index.js"] : is an array that represents the command and its arguments. In this case, it tells Docker to run the node command with index.js as an argument. Essentially, it instructs Docker to start 
  our Node.js application by running the index.js file when the container is launched.

  So, when we create a container from the Docker image built using this Dockerfile, it will automatically execute our Node.js application by running node index.js as its main process.

Creating Docker Image:
-----------------------
- First I installed Docker Desktop application to have the docker daemon running in the background.
- We could see the docker containers running using the command:
  
  `docker ps -a`
- We can run an already exixting docker image using the command:
  
  `docker run <image_name>:<version>`
- We can see the running docker images using the command:

  `docker images`
- In order to create our own docker image we use the command:

  `docker build -t shashwat:1.0 .`
  
  (. signifies the directory in which all the application files are present)
- Image hash generated : ac69e4cdbbe1
- For running the above created docker image, we run the command:

  `docker run --name my-app -d -p 4000:4000 shashwat:1.0`

    --name: to give a name to our running container
    -d: to run in detached mode
    -p: port binding
    -shashwat:1.0 : name of the image and version.

Image Layers:
--------------

	shashwat:1.0
		   |
	Node:20-alpine
	 	   |
	alpine:3.18


