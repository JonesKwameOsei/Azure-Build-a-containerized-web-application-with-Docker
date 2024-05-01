## Retrieve an existing Docker image and deploy it locally.

### Pull and run a sample application from Docker Hub
1. Start **Docker (dockerdesktop)** locally.
2. Open a command prompt window on your local computer.
3. Enter the code below to pull the ASP.NET Sample app image from the Docker Hub registry. This image contains a sample web app developed by Microsoft, and is based on the default ASP.NET template available in Visual Studio.
```
docker pull mcr.microsoft.com/dotnet/samples:aspnetapp
```

**Output**:
```
aspnetapp: Pulling from dotnet/samples
4abcf2066143: Already exists
aa30b34b64bd: Pull complete
7573946fa12b: Pull complete
e3db45edd5b6: Pull complete
7bd7045ee784: Pull complete
f5ad5c2fd768: Pull complete
9d2ebb3900c5: Pull complete
Digest: sha256:9eff28ca884ba26647500affe757c4c888f977132a09de82387fd71564d66625
Status: Downloaded newer image for mcr.microsoft.com/dotnet/samples:aspnetapp
mcr.microsoft.com/dotnet/samples:aspnetapp

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview mcr.microsoft.com/dotnet/samples:aspnetapp
```
4. Wait for docker to complete pulling the image, then enter the following code to verify that the image has been stored locally.
```
docker image ls
```

**Output**:
```
REPOSITORY                         TAG           IMAGE ID       CREATED        SIZE
mcr.microsoft.com/dotnet/samples   aspnetapp     dcc39f34ca59   3 weeks ago    115MB
docker/welcome-to-docker           latest        c1f619b6477e   5 months ago   18.6MB
kicbase/stable                     v0.0.42       dbc648475405   5 months ago   1.2GB
mcr.microsoft.com/mssql/server     2022-latest   86b87ec5e60a   6 months ago   1.57GB
```
We can see a repository named **mcr.microsoft.com/dotnet/samples** with a tag of **aspnetapp**. This means that docker has pulled the image successfully. 
5. Next, let us get the image run in the background as container and also expose on the web. 
```
docker run -d -p 8080:8080 mcr.microsoft.com/dotnet/samples:aspnetapp
```

6. Access the web app<p>
To access the wep app in the browser, we nopen a web browser and enter the URL for the sample web app: **http://localhost:8080**. You should see a page that looks like the following screenshot:<p>

![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/249dc183-e125-44ee-9e92-8feb056673b4)<p>

We can confirm from **docker desktop**if the image and container exist. <p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/ea307f5e-fcf3-4bbf-b5ca-13df86e720aa)<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/7a45c1c8-ae86-4a1c-9449-a5adaac87e36)<p>

## Perform operations on the the container in the local Docker registry
1. View the running containers in the local registry.
```
docker ps
```
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/9f8e3c4b-0f5a-4b00-b7bc-95393de13828)<p>

The COMMAND field shows the container was started by running the command 'dotnet aspnetapp.dll', which invokes the .NET Core runtime to start the sample web app code. The PORTS field indicates `port 8080` in the container was mapped to `port 8080` on the host computer. The STATUS field shows the application is still running. 

2. Stop the Docker container using the output name or container ID from the previous command by replacing the placeholder <NAME>/<container id>

```
docker container stop <name>/<container ID>
```
3. Use the command below to check if the container is no longer running. Use the -a flag to display the status of all containers, including those that are not running. The output should indicate that the container's status is Exited.
```
docker ps -a
```
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/12755279-dd15-4cc5-8775-58f3fc0d1705)<p>

4. Confirm from the browser if the web app has stopped.<p>
Refresh the page for the sample web app in opened earlier in the web browser (http://localhost:8080/). It should fail with a **Connection Refused error**.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/0d3f555b-c108-4f4d-92a4-9135dd19cd79)<p>

## Remove the container and image from the local registry
1. Stop the container, it is still loaded and can be restarted. Run the following command in the command prompt window to remove it, replacing `<NAME>` or `<ID>` placeholder with the name of your container. Run
```
docker container rm <NAME>
```
The image status on docker desktop, `unsued` indicates the container has been removed.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/46f5314e-6d2d-4d29-8c5b-18f2d5b57e97)<p>

2. Verify container removal by running the command. The command should no longer list the container.
```
docker ps -a
```
It is remove and not running.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/4fca4d75-5ddc-4245-bfef-78b60f810ba2)<p>
3. List the images currently available on your computer. The output should show the samples repository.<p>
```
docker image ls
```
**Output**:
```
REPOSITORY                         TAG           IMAGE ID       CREATED        SIZE
mcr.microsoft.com/dotnet/samples   aspnetapp     dcc39f34ca59   3 weeks ago    115MB
docker/welcome-to-docker           latest        c1f619b6477e   5 months ago   18.6MB
kicbase/stable                     v0.0.42       dbc648475405   5 months ago   1.2GB
mcr.microsoft.com/mssql/server     2022-latest   86b87ec5e60a   6 months ago   1.57GB
```
4. Remove the image from the registry.
```
docker image rm mcr.microsoft.com/dotnet/samples:aspnetapp
```
**Output**:
```
Untagged: mcr.microsoft.com/dotnet/samples:aspnetapp
Untagged: mcr.microsoft.com/dotnet/samples@sha256:9eff28ca884ba26647500affe757c4c888f977132a09de82387fd71564d66625
Deleted: sha256:dcc39f34ca59304fe63dab9b2a36d45a8e669e989be3d4df5131295eead0f793
Deleted: sha256:e89e62c9829f97cca2f465da7f57d491412f964e7ea933bc211d92fe2efb594b
Deleted: sha256:877083ecdbff27ada37d033a59f16d20f82a7c7544f5125f82b727d050cdc31c
Deleted: sha256:5eccfba2a75c8ee5e6e3d6679cc7b20e41a2e61a2fbd171ba694200e2cb41eb5
Deleted: sha256:3a2446b9f9a730513eb6e998a56d11af2dfa02e1d46fa9966026429919bf0be8
Deleted: sha256:79b503757f21dd6e1fbf3883f3c170a29ebac82e1d0ab4298467c36e79f9b4c4
Deleted: sha256:5eda52074615a611da6247776046258a553e90c6450368f50e2e20d125f4fca2
```
The output lists untagged and deleted items. Then, run the command to list the images again and verify that the image for the microsoft/dotnet-samples web app has disappeared.

5. Let us verify if the image has been deleted.
```
docker image ls
```
The output shows that the image is removed. 
```
REPOSITORY                       TAG           IMAGE ID       CREATED        SIZE
docker/welcome-to-docker         latest        c1f619b6477e   5 months ago   18.6MB
kicbase/stable                   v0.0.42       dbc648475405   5 months ago   1.2GB 
mcr.microsoft.com/mssql/server   2022-latest   86b87ec5e60a   6 months ago   1.57GB
```




















