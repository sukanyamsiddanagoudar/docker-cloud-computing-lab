# Docker Cloud Computing Lab

This repository contains Docker experiments and hands-on practical work completed as part of the Cloud Computing Laboratory.

The work demonstrates Docker application containerization, running multiple containers from the same image, and communication between containers using a custom Docker network.

## Experiments

| No. | Experiment                                  | Main Concept                         | Status    |
| --- | ------------------------------------------- | ------------------------------------ | --------- |
| 1   | Docker Python Application                   | Application containerization         | Completed |
| 2   | Run the Same Docker Image as Two Containers | Multiple containers from one image   | Completed |
| 3   | Docker Container Networking                 | Container-to-container communication | Completed |

## 1. Docker Python Application

A Python Flask application was developed and containerized using Docker.

The experiment covers:

* Creating a Python Flask application
* Creating a `requirements.txt` file
* Creating a `Dockerfile`
* Building a Docker image
* Running the application inside a Docker container
* Accessing the application through a web browser
* Viewing container logs
* Stopping and removing the container

**Folder:** [01-Docker-Python-App](./01-Docker-Python-App/)

## 2. Run the Same Docker Image as Two Containers

The existing `my-python-app` image was used to create two independent containers and run them at the same time.

| Container         | Host Port | Container Port |
| ----------------- | --------: | -------------: |
| `app-container-1` |      5001 |           5000 |
| `app-container-2` |      5002 |           5000 |

This experiment demonstrates that the same Docker image can be used to create multiple independent containers.

**Folder:** [02-Same-Image-Two-Containers](./02-Same-Image-Two-Containers/)

## 3. Docker Container Networking

A custom Docker network was created and two containers were connected to the same network.

```text
network-container-1
        |
        | app-network
        |
        v
network-container-2
```

Communication between the containers was tested using the container name:

```text
http://network-container-2:5000
```

This demonstrates container-to-container communication through a user-defined Docker network.

**Folder:** [03-Docker-Networking](./03-Docker-Networking/)

## Common Docker Commands

| Command                                 | Purpose                                                 |
| --------------------------------------- | ------------------------------------------------------- |
| `docker --version`                      | Checks whether Docker is installed and available        |
| `docker images`                         | Lists the Docker images available locally               |
| `docker ps`                             | Displays currently running containers                   |
| `docker ps -a`                          | Displays all containers, including stopped containers   |
| `docker logs <container-name>`          | Displays the logs of a container                        |
| `docker stop <container-name>`          | Stops a running container                               |
| `docker rm <container-name>`            | Removes a stopped container                             |
| `docker network create <network-name>`  | Creates a user-defined Docker network                   |
| `docker network ls`                     | Lists Docker networks                                   |
| `docker network inspect <network-name>` | Displays network configuration and connected containers |

## Repository Structure

```text
Docker-Cloud-Computing-Lab/
│
├── README.md
│
├── 01-Docker-Python-App/
│   ├── README.md
│   ├── app.py
│   ├── Dockerfile
│   ├── requirements.txt
│   └── screenshots/
│
├── 02-Same-Image-Two-Containers/
│   ├── README.md
│   └── screenshots/
│
└── 03-Docker-Networking/
    ├── README.md
    └── screenshots/
```

## Technologies Used

| Technology        | Purpose                                   |
| ----------------- | ----------------------------------------- |
| Docker            | Containerization and container management |
| Docker Desktop    | Local Docker environment                  |
| Python            | Application development                   |
| Flask             | Web application framework                 |
| Docker Networking | Communication between containers          |
| PowerShell        | Command-line interaction with Docker      |
