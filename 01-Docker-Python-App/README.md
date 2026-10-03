\# 01 — Docker Python Application



\## Aim



To create a simple Python Flask application, containerize it using Docker, build a Docker image, run the application inside a container, and access it through a web browser.



\## Technologies Used



\* Python

\* Flask

\* Docker

\* Dockerfile

\* Docker Desktop



\## Files



```text

01-Docker-Python-App/

├── app.py

├── Dockerfile

├── requirements.txt

└── screenshots/

```



\## 1. Verify Docker



```powershell

docker --version

```



\*\*Why:\*\* Checks whether Docker is installed and available in the terminal.



\## 2. Build the Docker Image



```powershell

docker build -t my-python-app .

```



\*\*What it does:\*\* Builds a Docker image using the Dockerfile in the current directory.



\*\*Why we use it:\*\* The image packages the Python application and its dependencies into a portable unit that can be used to create containers.



\## 3. Verify the Image



```powershell

docker images

```



\*\*Why:\*\* Confirms that `my-python-app` was successfully created.



\## 4. Run the Container



```powershell

docker run -d -p 5000:5000 --name my-python-container my-python-app

```



\*\*What the options mean:\*\*



\* `docker run` — creates and starts a container.

\* `-d` — runs the container in the background.

\* `-p 5000:5000` — maps host port 5000 to container port 5000.

\* `--name my-python-container` — assigns a name to the container.

\* `my-python-app` — specifies the image.



\*\*Why:\*\* Allows the Flask application to run inside the Docker container and be accessed from the host machine.



\## 5. Check the Running Container



```powershell

docker ps

```



\*\*Why:\*\* Confirms that the container is running.



\## 6. Open the Application



Open the following address in a browser:



```text

http://localhost:5000

```



\*\*Why:\*\* Tests the Flask application through the published Docker port.



\## 7. View Logs



```powershell

docker logs my-python-container

```



\*\*Why:\*\* Shows the application output and HTTP requests received by the Flask server.



\## 8. Stop the Container



```powershell

docker stop my-python-container

```



\*\*Why:\*\* Stops the running container.



\## 9. Remove the Container



```powershell

docker rm my-python-container

```



\*\*Why:\*\* Removes the stopped container after the experiment.



\## 10. Verify the Image



```powershell

docker images

```



\*\*Why:\*\* Demonstrates that removing a container does not remove the Docker image.



\## Result



The Python Flask application was successfully containerized, built into a Docker image, executed inside a container, and accessed through a web browser.



