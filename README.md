# 43 A + B : 

# Hello-World Flask Application with Docker


## 1. Set up the Flask Application

1. **Create a Project Directory**  
   Create a new directory for the Flask application:
   ```bash
   mkdir flask-hello-world
   cd flask-hello-world
   ```

2. **Set up a Virtual Environment (Optional but recommended)**  
   ```bash
   python3 -m venv venv
   #On Linux : source venv/bin/activate
   # On Windows : venv\Scripts\activate
   ```

3. **Install Flask**  
   ```bash
   pip install flask
   ```

4. **Create the Flask App**  
   In the project directory, create a new file named `app.py` with the following code:

   ```python
   # app.py

   from flask import Flask

   app = Flask(__name__)

   @app.route('/')
   def hello():
       return "<h1>Hello, World</h1>"

   if __name__ == "__main__":
       app.run(host="0.0.0.0", port=5000)
   ```

## 2. Create the Dockerfile

1. In the project directory, create a file named `Dockerfile` (without any extension) with the following content:

   ```Dockerfile
   # Use an official Python runtime as the base image
   FROM python:3.8-slim

   # Set the working directory in the container
   WORKDIR /app

   # Copy the current directory contents into the container at /app
   COPY . /app

   # Install Flask in the container
   RUN pip install flask

   # Expose the port on which the Flask app will run
   EXPOSE 5000

   # Define the command to run the app
   CMD ["python", "app.py"]
   ```

## 3. Build the Docker Image

1. **Build the Docker image**  
   Run the following command in your project directory:

   ```bash
   docker build -t flask-hello-world .
   ```

## 4. Run the Docker Container

1. **Run the container**  
   Start a container from your image with the following command:

   ```bash
   docker run -d -p 5000:5000 --name flask-container flask-hello-world
   ```

   - `-p 5000:5000` maps port 5000 on your host machine to port 5000 on the container.
   - `-d` will run the container in detatched mode
   - `--name` will assign the name to the container

2. **Verify the Application**  
   Open a web browser and go to [http://localhost:5000](http://localhost:5000). You should see the message:
   
   ```
   Hello, World!
   ```

## 5. Stopping the Container

1. To stop the running container, press `Ctrl+C` in the terminal where the container is running, or find the container ID using:

   ```bash
   docker ps
   ```

   Then stop it with:

   ```bash
   docker stop <container_id>
   ```
