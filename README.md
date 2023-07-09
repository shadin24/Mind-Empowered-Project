## Mind Empowered - Project

### Multi-Container Application Deployment

**Overview:** In this project, you will learn how to deploy a multi-container application using 
Docker Compose. You will start with a simple web application that consists of a Flask backend 
and a React frontend and use Docker Compose to orchestrate the deployment of multiple 
containers. You will also learn how to use Docker volumes to persist data between container 
restarts.
Tasks:
1. Install Docker Compose: Instruct interns to install Docker Compose on their local 
machine and verify that Docker Compose is working properly.
2. Create a Flask backend: Instruct interns to create a simple Flask backend that provides a 
RESTful API for a frontend to consume. The backend should use a PostgreSQL database 
to persist data.
3. Create a React frontend: Instruct interns to create a simple React frontend that 
consumes the RESTful API provided by the Flask backend.
4. Write a Docker Compose file: Instruct interns to write a Docker Compose file that 
defines the multi-container application. The Docker Compose file should define a service 
for the Flask backend, a service for the PostgreSQL database, and a service for the React 
frontend. The file should also define volumes to persist the PostgreSQL data.
5. Build the Docker images: Instruct interns to build the Docker images for the backend 
and frontend services using the Dockerfiles they created in the previous steps.
6. Test the multi-container application: Instruct interns to test the multi-container 
application by running it using Docker Compose and verifying that the frontend can 
successfully consume the backend's RESTful API.
7. Scale the application: Instruct interns to use Docker Compose to scale the backend 
service to multiple replicas and verify that the load is balanced across the replicas.
8. Add a logging service: Instruct interns to add a logging service to the Docker Compose 
file and configure the backend service to log to the logging service.
9. Deploy the multi-container application to a production environment: Instruct interns to 
deploy the multi-container application to a production environment using Docker 
Compose and verify that the application is accessible from a web browser.
10. Document the deployment process: Instruct interns to document the deployment 
process in a README file that includes detailed instructions for building, testing, and 
deploying the multi-container application.

**Deliverables:**
- A Docker Compose file that can be used to deploy the multi-container application.
- Docker images for the backend and frontend services.
- A deployed multi-container application running on a production environment.
- A README file that documents the deployment process.



## Prerequisites

Before starting the deployment process, ensure that you have the following prerequisites installed on your system:

- Docker: Version 19.03.0 or higher
- Docker Compose: Version 1.27.0 or higher
- npm: Version 6 or higher
- Python: Version 3.7 or higher
- pip: Version 20 or higher

## Deployment Steps

Follow these steps to deploy the multi-container application:

### Step 1: Install Docker Compose

1. Ensure that Docker is installed and running on your system.
2. Install Docker Compose by following the official Docker documentation for your operating system: [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)
3. Verify the installation by running the following command in your terminal:

docker-compose --version

vbnet

It should display the version information if Docker Compose is installed correctly.

### Step 2: Clone the Repository

1. Clone the repository containing the multi-container application to your local machine.

```
git clone <repository_url>
```


2. Navigate to the project directory.

```

cd <project_directory>
```



### Step 3: Configure the Backend

1. Inside the project directory, configure the Flask backend by following these steps:
- Create a Python virtual environment:
  ```
  python -m venv venv
  ```

- Activate the virtual environment:
  - Linux/Mac:
    ```
    source venv/bin/activate
    ```

  - Windows:
    ```
    venv\Scripts\activate
    ```

- Install Flask and other dependencies:
  ```
  pip install -r backend/requirements.txt
  ```

- Configure the backend by modifying the necessary configuration files.

### Step 4: Create a Dockerfile for the Backend

1. Inside the project directory, create a file named `Dockerfile` (without any file extension) for the backend.
2. Open the `Dockerfile` in a text editor and add the following content:

```dockerfile
# Use the official Python base image
FROM python:3.9-slim-buster

# Set the working directory in the container
WORKDIR /app

# Copy the requirements file to the working directory
COPY backend/requirements.txt .

# Install the backend dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the backend source code to the working directory
COPY backend/app app

# Set the entry point command to run the backend
CMD ["python", "app/main.py"]
```
 Save the Dockerfile.
 
  ### Step 5: Install Flask

In the project directory, ensure that the Python virtual environment is activated (refer to Step 3).
 Install Flask by running the following command:

    pip install flask

### Step 6: Install the React Frontend

 Navigate to the frontend directory within the project directory:

    

    cd frontend

Install the required dependencies by running the following command:

    npm install

Wait for the installation to complete. This will download and install all the necessary packages and libraries for the React frontend.

### Step 7: Create a Dockerfile for the Frontend

  Inside the frontend directory, create a file named Dockerfile.prod (without any file extension) for the frontend.

  Open the Dockerfile.prod in a text editor and add the following content:

    

    # Use the official Node.js base image
    FROM node:14-alpine

    # Set the working directory in the container
    WORKDIR /app

    # Copy the frontend source code to the working directory
    COPY . .

    # Install the frontend dependencies and build the production-ready assets
    RUN npm install && npm run build

    # Set the entry point command to serve the built assets
    CMD ["npm", "start"]

  Save the Dockerfile.prod.

### Step 8: Configure Docker Compose

  Create a new file named docker-compose.yml in the project directory.

  Copy and paste the following code into the docker-compose.yml file:

    

    version: "3"
    services:
      backend:
        build:
          context: ./backend
        ports:
          - "5000:5000"
        depends_on:
          - db
        volumes:
          - ./backend/app:/app
        environment:
          - POSTGRES_HOST=db
          - POSTGRES_PORT=5432
          - POSTGRES_USER=postgres
          - POSTGRES_PASSWORD=postgres
          - POSTGRES_DB=mydatabase

      frontend:
        build:
          context: ./frontend
          dockerfile: Dockerfile.prod
        ports:
          - "80:80"

      db:
        image: postgres:13
        volumes:
          - ./postgres-data:/var/lib/postgresql/data
        environment:
          - POSTGRES_USER=postgres
          - POSTGRES_PASSWORD=postgres
          - POSTGRES_DB=mydatabase

Save the docker-compose.yml file.

### Step 9: Build Docker Images

Build the Docker images for the backend and frontend services by running the following commands in the project directory:

    

    docker-compose build backend
    docker-compose build frontend

Wait for the images to be built. This may take a few minutes depending on your system and internet speed.

## Step 10: Start the Application

Start the multi-container application using Docker Compose:

    

    docker-compose up -d

Docker Compose will create and start the containers defined in the docker-compose.yml file in detached mode (-d flag).

Wait for the containers to start up and ensure that there are no errors in the logs.

Once the containers are running, the application should be accessible at the appropriate URL or IP address.

### Step 11: Verify the Application

Open a web browser and visit the URL or IP address where the application is deployed.
Verify that the React frontend is successfully consuming the RESTful API provided by the Flask backend.
Interact with the application to ensure that it functions as expected.

### Step 12: Scaling the Backend Service

To scale the backend service to multiple replicas, update the docker-compose.yml file as follows:

    

      services:
        backend:
          # ... other configurations ...
          scale: 3

Adjust the number of replicas (3 in the example) based on your requirements.

Save the file and run the following command to apply the changes:

    

    docker-compose up -d --scale backend=3

  This command will scale the backend service to the specified number of replicas.

  Verify that the load is balanced across the backend replicas.

### Step 13: Additional Configurations

   If additional configurations are required, such as SSL/TLS termination, load balancer setup, or custom domain mapping, refer to the relevant documentation for your hosting environment or infrastructure.
## Conclusion

  You have successfully deployed the multi-container application using Docker Compose. The application should now be up and running, allowing users to interact with the Flask backend through the React frontend.



















