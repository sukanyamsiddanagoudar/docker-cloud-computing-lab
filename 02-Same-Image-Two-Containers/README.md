# 02 — Run the Same Docker Image as Two Containers

## Aim

To run the same Docker image as two independent containers simultaneously and access them through different host ports.

## Existing Docker Image

The experiment uses the Docker image created in the previous experiment:

```text
my-python-app
```

No new Docker image is built for this experiment.

## Container Configuration

| Container         | Docker Image    | Host Port | Container Port |
| ----------------- | --------------- | --------: | -------------: |
| `app-container-1` | `my-python-app` |      5001 |           5000 |
| `app-container-2` | `my-python-app` |      5002 |           5000 |

Both containers use the same Docker image but different host ports.

## Step 1 — Verify the Docker Image

```powershell
docker images
```

**Purpose:** Confirms that the existing `my-python-app` image is available before creating the containers.

## Step 2 — Create the First Container

```powershell
docker run -d -p 5001:5000 --name app-container-1 my-python-app
```

| Option                   | Purpose                                    |
| ------------------------ | ------------------------------------------ |
| `docker run`             | Creates and starts a container             |
| `-d`                     | Runs the container in detached mode        |
| `-p 5001:5000`           | Maps host port 5001 to container port 5000 |
| `--name app-container-1` | Assigns a name to the container            |
| `my-python-app`          | Specifies the Docker image                 |

**Purpose:** Creates the first independent container from the existing Docker image.

## Step 3 — Create the Second Container

```powershell
docker run -d -p 5002:5000 --name app-container-2 my-python-app
```

**Purpose:** Creates a second independent container using the same Docker image.

The second container uses host port `5002` because host port `5001` is already being used by the first container.

## Step 4 — Verify Both Containers

```powershell
docker ps
```

**Purpose:** Confirms that both containers are running simultaneously.

Expected configuration:

```text
app-container-1 → localhost:5001 → container:5000
app-container-2 → localhost:5002 → container:5000
```

## Step 5 — Test the First Container

Open:

```text
http://localhost:5001
```

**Purpose:** Verifies that the first container is serving the Flask application.

## Step 6 — Test the Second Container

Open:

```text
http://localhost:5002
```

**Purpose:** Verifies that the second container is independently serving the same Flask application.

## Step 7 — View Container Logs

```powershell
docker logs app-container-1
```

```powershell
docker logs app-container-2
```

**Purpose:** Displays the application activity and requests handled by each container.

## Step 8 — Stop the First Container

```powershell
docker stop app-container-1
```

**Purpose:** Stops only the first container.

Then check:

```powershell
docker ps
```

The second container should continue running.

## Step 9 — Verify the Second Container

Open:

```text
http://localhost:5002
```

**Purpose:** Demonstrates that stopping one container does not stop the other container.

## Step 10 — View All Containers

```powershell
docker ps -a
```

**Purpose:** Displays both running and stopped containers.

## Step 11 — Stop the Second Container

```powershell
docker stop app-container-2
```

**Purpose:** Stops the second running container.

## Step 12 — Remove the Containers

```powershell
docker rm app-container-1
docker rm app-container-2
```

**Purpose:** Removes the containers after completing the experiment.

## Step 13 — Verify the Docker Image

```powershell
docker images
```

**Purpose:** Confirms that removing containers does not remove the Docker image.

## Result

The same Docker image was successfully used to run two independent containers simultaneously.

Both containers served the same Flask application using different host ports, demonstrating that multiple containers can be created from a single Docker image.

## Screenshots

The screenshots documenting the experiment are available in the [`screenshots`](./screenshots/) folder.
