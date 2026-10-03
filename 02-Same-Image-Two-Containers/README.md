\# 02 — Run the Same Docker Image as Two Containers



\## Aim



To run the same Docker image as two independent containers simultaneously and access them through different host ports.



\## Existing Image



The experiment uses the existing image:



```text

my-python-app

```



No new Docker image is built for this experiment.



\## 1. Verify the Image



```powershell

docker images

```



\*\*Why:\*\* Confirms that the previously created `my-python-app` image is available.



\## 2. Create the First Container



```powershell

docker run -d -p 5001:5000 --name app-container-1 my-python-app

```



\*\*Why:\*\* Creates and starts the first container from the existing image.



The port mapping is:



```text

Host: 5001 → Container: 5000

```



\## 3. Create the Second Container



```powershell

docker run -d -p 5002:5000 --name app-container-2 my-python-app

```



\*\*Why:\*\* Creates another independent container from the same image.



The port mapping is:



```text

Host: 5002 → Container: 5000

```



The host ports are different because two containers cannot use the same host port simultaneously.



\## 4. Verify Both Containers



```powershell

docker ps

```



\*\*Why:\*\* Confirms that both containers are running at the same time.



\## 5. Test Container 1



Open:



```text

http://localhost:5001

```



\*\*Why:\*\* Verifies that `app-container-1` is serving the Flask application.



\## 6. Test Container 2



Open:



```text

http://localhost:5002

```



\*\*Why:\*\* Verifies that `app-container-2` is independently serving the same application.



\## 7. Check Logs



```powershell

docker logs app-container-1

docker logs app-container-2

```



\*\*Why:\*\* Allows the activity of each container to be checked separately.



\## 8. Stop Container 1



```powershell

docker stop app-container-1

```



\*\*Why:\*\* Stops only the first container.



Then:



```powershell

docker ps

```



The second container should still be running.



\## 9. Verify Container 2



Open:



```text

http://localhost:5002

```



\*\*Why:\*\* Demonstrates that stopping one container does not stop the other.



\## 10. View All Containers



```powershell

docker ps -a

```



\*\*Why:\*\* Displays both running and stopped containers.



\## 11. Stop and Remove the Containers



```powershell

docker stop app-container-2

docker rm app-container-1

docker rm app-container-2

```



\*\*Why:\*\* Cleans up the containers after the experiment.



\## 12. Verify the Image



```powershell

docker images

```



\*\*Why:\*\* Confirms that the Docker image still exists even after its containers have been removed.



\## Result



The same Docker image was successfully used to run two independent containers simultaneously, with each container accessible through a different host port.



