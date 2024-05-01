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































