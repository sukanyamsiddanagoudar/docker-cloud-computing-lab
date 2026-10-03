# 03 — Docker Container Networking

## Aim

To create a custom Docker network and demonstrate communication between two Docker containers using the Docker container name.

## Existing Docker Image

The experiment uses the existing Docker image:

```text
my-python-app
```

No new Docker image is created in this experiment.

## Docker Network

A custom user-defined network named `app-network` is created to allow the containers to communicate with each other.

## Step 1 — Create the Docker Network

```powershell
docker network create app-network
```

### Purpose

Creates a custom Docker network named `app-network`.

### Why it is used

Containers connected to the same user-defined Docker network can communicate with each other.

---

## Step 2 — Verify the Network

```powershell
docker network ls
```

### Purpose

Displays all Docker networks available on the system.

### Expected Result

The newly created network should appear as:

```text
app-network
```

---

## Step 3 — Create the First Container

```powershell
docker run -d --name network-container-1 --network app-network -p 5001:5000 my-python-app
```

### Command Explanation

| Option                       | Meaning                                    |
| ---------------------------- | ------------------------------------------ |
| `docker run`                 | Creates and starts a container             |
| `-d`                         | Runs the container in detached mode        |
| `--name network-container-1` | Gives the container a name                 |
| `--network app-network`      | Connects the container to `app-network`    |
| `-p 5001:5000`               | Maps host port 5001 to container port 5000 |
| `my-python-app`              | Specifies the Docker image                 |

### Purpose

Creates the first container, connects it to the custom network, and makes the application accessible from the host machine.

---

## Step 4 — Create the Second Container

```powershell
docker run -d --name network-container-2 --network app-network my-python-app
```

### Purpose

Creates the second container from the same Docker image and connects it to the same `app-network`.

### Why no `-p` option is used

The second container does not need to be accessed directly from the host browser. It will be accessed by the first container through the Docker network.

---

## Step 5 — Verify Both Containers

```powershell
docker ps
```

### Purpose

Checks whether both `network-container-1` and `network-container-2` are running.

The expected setup is:

| Container             | Network       | Host Port | Container Port |
| --------------------- | ------------- | --------: | -------------: |
| `network-container-1` | `app-network` |      5001 |           5000 |
| `network-container-2` | `app-network` |         — |           5000 |

---

## Step 6 — Test the First Container from the Browser

Open:

```text
http://localhost:5001
```

### Purpose

Verifies that the Flask application running in `network-container-1` is accessible from the host machine.

---

## Step 7 — Test Container-to-Container Communication

Run the following command:

```powershell
docker exec network-container-1 python -c "import urllib.request; print(urllib.request.urlopen('http://network-container-2:5000').read().decode())"
```

### Purpose

This command executes a Python program inside `network-container-1` and sends an HTTP request to `network-container-2`.

### Communication Path

```text
network-container-1
        |
        | HTTP request
        | http://network-container-2:5000
        |
        v
network-container-2
```

### Result

The response received was:

```text
Hello! My first Docker application is running.
```

This confirms that the two containers successfully communicated through the Docker network.

---

## Why Is the Container Name Used?

Inside a Docker container, `localhost` refers to that same container.

For example:

```text
localhost
```

inside `network-container-1` refers to:

```text
network-container-1
```

It does not refer to `network-container-2`.

Therefore, the second container is accessed using its container name:

```text
http://network-container-2:5000
```

Docker's user-defined network resolves the container name to the appropriate container address.

---

## Step 8 — Inspect the Docker Network

```powershell
docker network inspect app-network
```

### Purpose

Displays detailed information about the Docker network.

It can be used to verify that both containers are connected to `app-network`.

The network should contain:

```text
network-container-1
network-container-2
```

---

## Step 9 — Remove the Containers

```powershell
docker rm -f network-container-1 network-container-2
```

### Purpose

Stops and removes both containers after completing the experiment.

---

## Step 10 — Remove the Docker Network

```powershell
docker network rm app-network
```

### Purpose

Removes the custom Docker network after the experiment is completed.

---

## Step 11 — Verify the Cleanup

### Check Containers

```powershell
docker ps -a
```

**Purpose:** Verifies that the experiment containers have been removed.

### Check Docker Image

```powershell
docker images
```

**Purpose:** Verifies that the `my-python-app` image still exists.

### Check Docker Networks

```powershell
docker network ls
```

**Purpose:** Verifies that the custom `app-network` has been removed.

---

## Result

A custom Docker network named `app-network` was successfully created.

Two containers were connected to the same network, and communication between `network-container-1` and `network-container-2` was successfully demonstrated using the Docker container name.

## Screenshots

All screenshots for this experiment are available in the [`screenshots`](./screenshots/) folder.
