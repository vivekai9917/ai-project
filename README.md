print("welcome to docker file")

































#!/bin/bash

# STEP 1: Install Docker
sudo apt update
sudo apt install docker.io -y

# STEP 2: Start Docker
sudo systemctl start docker
sudo systemctl enable docker

# STEP 3: Create project folder
mkdir -p ai-docker-project
cd ai-docker-project

# STEP 4: Create app.py
cat > app.py <<'EOF'
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/')
def home():
    return "Welcome to AI Application running inside Docker!"

@app.route('/predict')
def predict():
    return jsonify({
        "model": "AI Model",
        "prediction": "Positive",
        "status": "Success"
    })

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
EOF

# STEP 5: Create requirements.txt
cat > requirements.txt <<'EOF'
flask
EOF

# STEP 6: Create Dockerfile
cat > Dockerfile <<'EOF'
FROM python:3.10-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY app.py .
EXPOSE 5000
CMD ["python", "app.py"]
EOF

# STEP 7: Build Docker image
sudo docker build -t ai-app .

# STEP 8: Run Docker container
sudo docker run -d -p 5000:5000 --name ai-container ai-app

# STEP 9: Verify container
sudo docker ps

# STEP 10: Test application
echo "Testing Home Page:"
curl http://localhost:5000

echo ""
echo "Testing Prediction API:"
curl http://localhost:5000/predict

# STEP 11: Stop container
sudo docker stop ai-container

# STEP 12: Verify container stopped
sudo docker ps -a

echo "Docker practical completed successfully!"   just add viva questions and meaning of all used command--------------------------------------------------------------------

Docker Practical: Deploying an AI Application Using Docker
Aim
To create a simple AI-based web application using Python Flask, package it into a Docker image, run it inside a Docker container, test the application, and stop the container.

1. Install Docker

bash
sudo apt update
sudo apt install docker.io -y
Meaning of commands:

sudo – Executes commands with administrator privileges.

apt – Package management tool in Ubuntu.

update – Updates the package list.

install – Installs software.

docker.io – Docker package.

-y – Automatically confirms installation.

2. Start Docker

bash
sudo systemctl start docker
sudo systemctl enable docker
Meaning:

systemctl – Manages system services.

start – Starts Docker.

enable – Enables Docker to start automatically when the system boots.

3. Create Project Folder

bash
mkdir -p ai-docker-project
cd ai-docker-project
Meaning:

mkdir – Creates a directory.

-p – Creates parent directories if required and avoids errors if the directory exists.

cd – Changes the current directory.

ai-docker-project – Project folder name.

4. Create app.py

bash
cat > app.py <<'EOF'
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/')
def home():
    return "Welcome to AI Application running inside Docker!"

@app.route('/predict')
def predict():
    return jsonify({
        "model": "AI Model",
        "prediction": "Positive",
        "status": "Success"
    })

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
EOF
Meaning:

cat – Creates or displays file content.

> – Redirects content into a file.

app.py – Python application file.

EOF – Marks the end of the input content.

Flask – Python web framework.

jsonify() – Converts Python data into JSON format.

@app.route('/') – Defines the home page.

@app.route('/predict') – Defines the prediction API.

host='0.0.0.0' – Allows connections from outside the container.

port=5000 – Runs the application on port 5000.

5. Create requirements.txt

bash
cat > requirements.txt <<'EOF'
flask
EOF
Meaning:

requirements.txt – Stores Python dependencies.

flask – Python library required by the application.

6. Create Dockerfile

bash
cat > Dockerfile <<'EOF'
FROM python:3.10-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY app.py .
EXPOSE 5000
CMD ["python", "app.py"]
EOF
Meaning of Dockerfile instructions:

Command

Meaning

FROM

Selects the base image.

WORKDIR

Sets the working directory inside the container.

COPY

Copies files into the image.

RUN

Executes commands during image building.

pip install

Installs Python packages.

--no-cache-dir

Prevents pip from storing its package cache.

EXPOSE

Documents the application port.

CMD

Specifies the default startup command.

7. Build Docker Image

bash
sudo docker build -t ai-app .
Meaning:

docker build – Builds a Docker image.

-t – Assigns a name or tag to the image.

ai-app – Name of the Docker image.

. – Specifies the current directory as the build context.

8. Run Docker Container

bash
sudo docker run -d -p 5000:5000 --name ai-container ai-app
Meaning:

docker run – Creates and starts a container.

-d – Runs the container in the background.

-p 5000:5000 – Maps host port 5000 to container port 5000.

--name – Assigns a name to the container.

ai-container – Container name.

ai-app – Docker image name.

9. Verify Container

bash
sudo docker ps
Meaning:

- docker ps – Displays currently running Docker containers.

10. Test Application

bash
echo "Testing Home Page:"
curl http://localhost:5000

echo ""
echo "Testing Prediction API:"
curl http://localhost:5000/predict
Meaning:

echo – Displays text on the terminal.

curl – Sends HTTP requests to test the application.

localhost – Refers to the current computer.

/ – Home page endpoint.

/predict – Prediction API endpoint.

Expected output:

Home page:


text
Welcome to AI Application running inside Docker!
Prediction API:


json
{
  "model": "AI Model",
  "prediction": "Positive",
  "status": "Success"
}
11. Stop Container

bash
sudo docker stop ai-container
Meaning:

docker stop – Stops a running Docker container.

ai-container – Name of the container to stop.

12. Verify Container Stopped

bash
sudo docker ps -a

echo "Docker practical completed successfully!"
Meaning:

docker ps -a – Displays all containers, including stopped containers.

echo – Prints the completion message.

Exited – Indicates that the container has stopped.

13. Viva Questions and Answers
Q1. What is Docker?

Docker is an open-source platform used to package and run applications inside containers.

Q2. What is a container?

A container is a lightweight, isolated environment used to run an application with its dependencies.

Q3. What is a Docker image?

A Docker image is a read-only template used to create containers.

Q4. What is the difference between an image and a container?

An image is a blueprint, whereas a container is an instance created from that image.

Q5. What is a Dockerfile?

A Dockerfile is a text file containing instructions to build a Docker image.

Q6. What is Docker Hub?

Docker Hub is an online repository used to store and download Docker images.

Q7. What is Flask?

Flask is a lightweight Python web framework used to create web applications and APIs.

Q8. What is an API?

API stands for Application Programming Interface. It allows different software applications to communicate.

Q9. What is the purpose of requirements.txt?

It contains the Python libraries required by the application.

Q10. What is the purpose of EXPOSE 5000?

It documents that the application uses port 5000 inside the container.

Q11. What is port mapping?

Port mapping connects a port on the host machine to a port inside the Docker container.

Q12. What is the use of docker build?

It creates a Docker image using instructions from the Dockerfile.

Q13. What is the use of docker run?

It creates and starts a container from a Docker image.

Q14. What is the difference between docker ps and docker ps -a?

docker ps – Shows running containers.

docker ps -a – Shows all containers, including stopped containers.

Q15. What is the purpose of docker stop?

It stops a running Docker container.

Q16. What is the purpose of sudo?

It executes commands with administrator privileges.

Q17. What is the purpose of -d?

It runs a Docker container in detached or background mode.

Q18. What is the purpose of -t?

It assigns a name or tag to a Docker image.

Q19. What is the purpose of curl?

It sends HTTP requests to test web applications and APIs.

Q20. What is JSON?

JSON stands for JavaScript Object Notation. It is a lightweight data exchange format.

Q21. What is the purpose of the /predict route?

It returns a JSON response containing the model name, prediction, and status.

Q22. Why do we use host='0.0.0.0'?

It allows the Flask application to accept connections from outside the container.

Q23. What is the difference between RUN and CMD?

RUN – Executes commands during image building.

CMD – Specifies the default command when the container starts.

Q24. What are the advantages of Docker?

Portability

Application isolation

Easy deployment

Consistent environment

Efficient resource utilization

Q25. Is this a real AI model?

No. It is a sample prediction API that returns predefined results. It demonstrates Docker deployment rather than actual machine learning.

Q26. What is the default Flask port?

The default Flask development server port is 5000.

Q27. What is the purpose of systemctl?

It manages system services such as starting, stopping, and enabling Docker.

Q28. What is containerization?

Containerization is the process of packaging an application and its dependencies into a container.

Q29. Can multiple containers run on one system?

Yes, multiple Docker containers can run on the same host system.

Q30. Why is Docker useful for AI applications?

It packages AI applications and their dependencies so they can run consistently across different environments.

Q31. What is the difference between a virtual machine and a Docker container?

A virtual machine runs its own operating system, whereas a Docker container shares the host operating system's kernel.

Q32. What is the purpose of the WORKDIR instruction?

It sets the working directory inside the Docker image.

Q33. What is the purpose of COPY?

It copies files from the host system into the Docker image.

Q34. What is the purpose of the -p option in docker run?

It maps host and container ports.

Q35. What happens after docker stop?

The container stops running but remains available for future use.
