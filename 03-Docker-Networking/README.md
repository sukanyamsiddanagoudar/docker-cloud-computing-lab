\# 03 — Docker Container Networking



\## Aim



To create a custom Docker network and demonstrate communication between two Docker containers using container names.



\## Existing Image



The experiment uses the existing Docker image:



```text

my-python-app

```



No new Docker image is built.



\## 1. Create a Custom Docker Network



```powershell

docker network create app-network

```



\*\*What it does:\*\* Creates a user-defined Docker network named `app-network`.



\*\*Why we use it:\*\* Containers connected to the same user-defined network can communicate with each other directly.



\## 2. Verify the Network



```powershell

docker network ls

```



\*\*What it does:\*\* Lists the Docker networks available on the system.



\*\*Why we use it:\*\* Confirms that `app-network` was created successfully.



\## 3. Start the First Container



```powershell

docker run -d --name network-container-1 --network app-network -p 5001:5000 my-python-app

```



\### Command options



\* `docker run` — creates and starts a container.

\* `-d` — runs the container in detached/background mode.

\* `--name network-container-1` — assigns a name to the container.

\* `--network app-network` — connects the container to `app-network`.

\* `-p 5001:5000` — maps host port 5001 to container port 5000.

\* `my-python-app` — specifies the Docker image.



\*\*Why we use it:\*\* The first container needs to be connected to the custom network and exposed to the host so the application can also be tested from a browser.



\## 4. Start the Second Container



```powershell

docker run -d --name network-container-2 --network app-network my-python-app

```



\*\*Why we use it:\*\* Creates another container from the same image and connects it to the same Docker network.



No host port is required for this container because its main purpose is to receive a request from the first container through the Docker network.



\## 5. Verify Both Containers



```powershell

docker ps

```



\*\*Why we use it:\*\* Confirms that both `network-container-1` and `network-container-2` are running.



\## 6. Test the First Container from the Browser



Open:



```text

http://localhost:5001

```



\*\*Why we use it:\*\* Verifies that the Flask application running in `network-container-1` is accessible from the host machine.



\## 7. Test Container-to-Container Communication



Run:



```powershell

docker exec network-container-1 python -c "import urllib.request; print(urllib.request.urlopen('http://network-container-2:5000').read().decode())"

```



\### What this command does



`docker exec` runs a command inside an already-running container.



The Python command sends an HTTP request from:



```text

network-container-1

```



to:



```text

network-container-2:5000

```



The response was:



```text

Hello! My first Docker application is running.

```



\*\*Why we use it:\*\* This directly demonstrates communication between two containers through the Docker network.



\## Why We Use the Container Name Instead of localhost



Inside `network-container-1`:



```text

localhost

```



refers to `network-container-1` itself.



It does \*\*not\*\* refer to `network-container-2`.



Therefore, we use:



```text

http://network-container-2:5000

```



Docker's user-defined network resolves the container name to the appropriate container IP address.



\## 8. Inspect the Docker Network



```powershell

docker network inspect app-network

```



\*\*Why we use it:\*\* Displays the configuration of the network and identifies the containers connected to it.



The network inspection showed both:



```text

network-container-1

network-container-2

```



connected to `app-network`.



\## 9. Clean Up the Containers



```powershell

docker rm -f network-container-1 network-container-2

```



\*\*Why we use it:\*\* Stops and removes both containers in a single command.



The `-f` option forces removal, including stopping a running container first.



\## 10. Remove the Custom Network



```powershell

docker network rm app-network

```



\*\*Why we use it:\*\* Removes the custom Docker network after the experiment is complete.



\## 11. Verify Cleanup



```powershell

docker ps -a

```



\*\*Why:\*\* Confirms that the test containers have been removed.



```powershell

docker images

```



\*\*Why:\*\* Confirms that the `my-python-app` image still exists.



```powershell

docker network ls

```



\*\*Why:\*\* Confirms that `app-network` has been removed.



\## Result



A custom Docker network was successfully created and two containers were connected to it. Communication from `network-container-1` to `network-container-2` was successfully demonstrated using the Docker container name.



This experiment demonstrates the basic principle of container-to-container communication using a user-defined Docker network.



