# Docker-Tutorial

Docker is a platform for developing, shipping, and running applications in containers. Containers are lightweight, portable, and isolated environments that include an application and all its dependencies. Docker simplifies the deployment process, ensures consistency across different environments, and enables easy scaling of applications. It has gained popularity in the software development and DevOps communities for its ability to streamline the application lifecycle.

**1. Install Docker:**

Before you begin, you need to install Docker on your system. You can download the Docker Desktop for Windows or macOS or Docker Engine for Linux from the [official Docker website](https://www.docker.com/get-started).

**2. Verify Installation:**

After installation, open a terminal or command prompt and run the following command to verify that Docker is installed and working:

```bash
docker --version
```

**3. Hello World:**

Let's start with a simple example of running a Docker container that prints "Hello, World!" to the console.

```bash
docker run hello-world
```

This command will download the "hello-world" image from the Docker Hub registry and run it in a container.

**4. Run Your Own Container:**

Now, let's create and run a basic Docker container with a custom command. In this example, we'll run an interactive Ubuntu container.

```bash
docker run -it ubuntu
```

This command will start an interactive shell within an Ubuntu container. You can execute Ubuntu commands from the terminal. To exit the container, type `exit`.

**5. Build and Run Your Custom Image:**

To create a custom Docker image, you'll need to write a Dockerfile that defines the image's configuration. Here's a simple example using an Nginx web server:

Create a new directory for your Docker project and navigate to it.

Inside the project directory, create a file named `Dockerfile` (with no file extension) and add the following contents:

```Dockerfile
# Use an official Nginx runtime as a parent image
FROM nginx

# Expose port 80 for web traffic
EXPOSE 80

# Copy your custom HTML file to the container
COPY my-website/index.html /usr/share/nginx/html

# Start the Nginx web server
CMD ["nginx", "-g", "daemon off;"]
```

In this example, we're using the official Nginx image, exposing port 80, copying a custom HTML file, and starting the Nginx server.

Build the Docker image from the project directory. Replace `<your-image-name>` with a name for your image:

```bash
docker build -t <your-image-name> .
```

Now, you can run a container from your custom image:

```bash
docker run -d -p 8080:80 <your-image-name>
```

This command runs the container in detached mode, maps port 8080 on your host to port 80 in the container, and uses the custom image you built.

You can access your custom web server by opening a web browser and navigating to `http://localhost:8080`.

**6. Explore and Manage Containers:**

To see the list of running containers, use the following command:

```bash
docker ps
```

To stop a container, replace `<container-id>` with the container's ID or name:

```bash
docker stop <container-id>
```

To remove a stopped container, use:

```bash
docker rm <container-id>
```

**7. Cleanup:**

To remove unused images and free up disk space, you can use:

```bash
docker image prune
```

These are the basics of working with Docker. Docker offers much more, including Docker Compose for managing multi-container applications, Docker Swarm for orchestration, and Kubernetes integration for container orchestration at scale. Explore Docker's documentation and tutorials to learn more about containerization and its capabilities.

# Docker with Ruby on Rails

**Scenario:** You are developing a Ruby on Rails application, and you want to use Docker to containerize it for development and deployment. Here are the steps:

1. **Create a Dockerfile:**

   Start by creating a `Dockerfile` in your Rails application's root directory. This file contains instructions for building a Docker image for your application.

   ```Dockerfile
   # Use the official Ruby image as the base
   FROM ruby:3.0.3

   # Set the working directory inside the container
   WORKDIR /app

   # Copy your Rails application files into the container
   COPY . .

   # Install Rails application dependencies
   RUN bundle install

   # Expose the port on which your Rails server will run
   EXPOSE 3000

   # Start your Rails application
   CMD ["rails", "server", "-b", "0.0.0.0"]
   ```

2. **Build the Docker Image:**

   Use the following command to build the Docker image. Replace `<your-image-name>` with a name for your image.

   ```bash
   docker build -t <your-image-name> .
   ```

3. **Run the Docker Container:**

   After building the image, you can run a container from it. You can map the container's port 3000 to a port on your host system, such as 3000. This allows you to access your Rails application in a web browser.

   ```bash
   docker run -p 3000:3000 <your-image-name>
   ```

4. **Access Your Rails Application:**

   Your Rails application is now running in a Docker container. Open a web browser and navigate to `http://localhost:3000` to access your application. You can interact with your Rails app as you normally would.

5. **Development and Deployment:**

   You can continue to develop your Ruby on Rails application within the Docker container. When you're ready to deploy it, you can use Docker to build an image and deploy it to your production environment.

The key advantage of using Docker in this scenario is that you have a consistent and isolated development environment, and you can easily move your application between development, testing, and production environments without worrying about differences in system configurations.

Docker can be especially useful when working with complex applications that have many dependencies. It simplifies the process of setting up and deploying these applications, making them more portable and easier to manage.
