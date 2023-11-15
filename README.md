## TP 1: Introduction to docker
In this first part of the lab you will build and run your first docker.

### Step 1: Introduction to Docker
- Docker is a platform that enables developers to easily create, deploy, and run applications in containers.
- Containers are isolated environments that contain everything an application needs to run, including the code, runtime, system tools, libraries, and settings.
### Step 2: Installing Docker
- Docker is available for Windows, macOS, and various Linux distributions.
- To install Docker on your system, follow the instructions for your operating system at this URL: https://docs.docker.com/engine/install/

### Step 3: Running your first Docker container
- To verify that Docker is installed and running correctly, run the following command in your terminal: docker run hello-world
- This command downloads and runs the “hello-world” image from the Docker hub, which displays a message indicating that Docker is installed and working correctly.
### Step 4: Creating a Docker container
- To create a Docker container, you'll first need to download an image from the Docker hub or create your own.
- For this lab, we'll use the Ubuntu image. To download and run the image, run the following command: 

```
docker run -it ubuntu
```

- The -it flag specifies that we want to run the container interactively and allocate a TTY for the container process.

### Step 5: Exploring the Docker container
- You are now inside the Docker container and have a  shell prompt.
- Try running some Linux commands to familiarize yourself with the environment.
- To exit the container, type exit at the prompt.

### Step 6: Stopping and removing containers
- To stop a running Docker container, run the following command: docker stop [container_id]
- To remove a stopped Docker container, run the following command: docker rm [container_id]

## Part 2: Building a Docker Image from Dockerfile and Running the Application

In this section of the lab, you will learn how to run a simple web app by building an existing Dockerfile.

### Step 1: Pull the Required Code from GitHub

Execute the following command:

```
git clone https://github.com/christophezei/INSA---TP-1---Docker.git
```

### Step 2: Build Dockerfile and Run the Web App

Navigate to the cloned directory, then build your image:

```
cd /INSA---TP-1---Docker
docker image build -t webapp .
```
After execution, run the command:

```
docker image ls
```

This command displays the newly created image "webapp." Finally, run a container from this image to launch your application:

```
docker run -p 5000:5000 -d webapp
```

Access the simple web app through your browser using the following link:


```
http://localhost:5000/
```

Congratulations! You've successfully built an application from an existing Dockerfile, showcasing the power of Docker without the need to install any additional packages.

## Part 3: Creating Your Own Dockerfile 
In the previous section, you learned how to build an application with an existing Dockerfile. 
Now, let's explore creating your own Dockerfile to run a Jupyter Notebook.

### Step 1: Creating a Dockerfile
- Create a new directory for the project and navigate to that directory in the terminal.
- Create a new file in the directory named Dockerfile without an extension.
- Add the following lines to the Dockerfile:


```
FROM jupyter/base-notebook:latest
RUN pip install scikit-learn
```

- The first line specifies the base image to use, in this case, the jupyter/base-notebook image with the latest tag.
- The second line runs the pip command to install the scikit-learn package.

### Step 2: Building the Docker image
To build the Docker image, run the following command in the terminal:

```
docker build -t jupyter-scikit-learn .
```

- The -t flag specifies the name and tag to give the image, in this case, jupyter-scikit-learn.
- The . at the end of the command specifies the context, which is the current directory.

### Step 3: Running the Jupyter Notebook
To run the Jupyter Notebook, run the following command in the terminal:

```
docker run --user root -v app:/home/jovyan -e GRANT_SUDO=yes -it --rm -p 8888:8888 jupyter-scikit-learn
```

### Step 4: Using scikit-learn in the Jupyter Notebook

- Open a web browser and navigate to http://localhost:8888. You should see the Jupyter Notebook login page.
- Enter the token displayed in the terminal to log in.
- Once you are logged in, create a new Jupyter Notebook by clicking on the "New" button in the top right corner and selecting "Python 3".
In the new Jupyter Notebook, run the following code to test scikit-learn:

```
import sklearn
print(sklearn.__version__)
```

- The output should show the version of scikit-learn that is installed in the Jupyter Notebook.
- Attempt to import TensorFlow by running

```
import tensorflow as tf
print(tf.__version__)
```
As you can see, TensorFlow is not installed. Follow the steps below to install it:

-Create a requirements.txt file containing "scikit-learn" and "tensorflow."
-Modify the Dockerfile to install packages from requirements.txt.
-Rebuild your image with the modified Dockerfile.
-Run your container and test the TensorFlow installation.

### Step 5: Test an app in ubuntu container

In this segment, your objective is to assess an application in an isolated environment, 
ensuring that all actions, including cloning the repository, 
are performed within the confines of the Docker container. The rationale behind this approach is to maintain a secure and self-contained testing environment. To achieve this, your task is to create a comprehensive Dockerfile. This Dockerfile should not only compile and execute the code from the provided repository but also encompass the necessary steps to clone the repository directly within the container. By encapsulating all processes within the container, we enhance security measures and isolate potential risks from your local machine.

repo to test :

```
https://github.com/lukinoo/calculator_c/tree/main
```


### Conclusion
By the end of this lab, you should now possess practical skills in Docker, ranging from grasping fundamental 
containerization concepts to crafting custom images tailored for specific applications. 
This newfound knowledge enhances your capability to construct reproducible and portable development environments,
fostering efficiency and consistency in your software development workflows.



