# 01 — Docker Python Application

## Aim

To create a simple Python Flask application, containerize it using Docker, build a Docker image, run the application inside a Docker container, and access it through a web browser.

## Technologies Used

| Technology     | Purpose                                |
| -------------- | -------------------------------------- |
| Python         | Application development                |
| Flask          | Web application framework              |
| Docker         | Containerization                       |
| Dockerfile     | Defines the Docker image configuration |
| Docker Desktop | Local Docker environment               |

## Project Files

| File / Folder      | Description                                     |
| ------------------ | ----------------------------------------------- |
| `app.py`           | Python Flask application                        |
| `Dockerfile`       | Instructions used to build the Docker image     |
| `requirements.txt` | Python dependencies required by the application |
| `screenshots/`     | Screenshots of the experiment                   |

## Docker Workflow

The following steps were performed to containerize and run the Flask application.

### Step 1 — Verify Docker Installation

```powershell
docker --version
```

**Purpose:** Checks whether Docker is installed and available from the terminal.

### Step 2 — Build the Docker Image

```powershell
docker build -t my-python-app .
```

**Purpose:** Builds a Docker image named `my-python-app` using the `Dockerfile` in the current directory.

The `.` indicates that the current directory is used as the build context.

### Step 3 — Verify the Docker Image

```powershell
docker images
```

**Purpose:** Displays the Docker images available locally and verifies that `my-python-app` was created successfully.

### Step 4 — Run the Docker Container

```powershell
docker run -d -p 5000:5000 --name my-python-container my-python-app
```

| Option                       | Purpose                                    |
| ---------------------------- | ------------------------------------------ |
| `docker run`                 | Creates and starts a container             |
| `-d`                         | Runs the container in detached mode        |
| `-p 5000:5000`               | Maps host port 5000 to container port 5000 |
| `--name my-python-container` | Gives the container a name                 |
| `my-python-app`              | Specifies the Docker image                 |

**Purpose:** Starts the Flask application inside the Docker container and makes it accessible through the host machine.

### Step 5 — Check the Running Container

```powershell
docker ps
```

**Purpose:** Displays the currently running containers and verifies that `my-python-container` is running.

### Step 6 — Access the Application

Open the following address in a web browser:

```text
http://localhost:5000
```

**Purpose:** Tests whether the Flask application running inside the Docker container can be accessed through the mapped host port.

### Step 7 — View Container Logs

```powershell
docker logs my-python-container
```

**Purpose:** Displays the application output and requests received by the Flask application.

### Step 8 — Stop the Container

```powershell
docker stop my-python-container
```

**Purpose:** Stops the running container without removing it.

### Step 9 — Remove the Container

```powershell
docker rm my-python-container
```

**Purpose:** Removes the stopped container from the system.

### Step 10 — Verify the Docker Image

```powershell
docker images
```

**Purpose:** Confirms that the Docker image still exists after the container has been removed.

## Result

The Python Flask application was successfully containerized using Docker.

A Docker image named `my-python-app` was created, a container was launched from the image, and the Flask application was successfully accessed through a web browser.

## Screenshots

The screenshots documenting the experiment are available in the [`screenshots`](./screenshots/) folder.
