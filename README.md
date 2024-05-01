## Retrieve an existing Docker image and deploy it locally.

### Pull and run a sample application from Docker Hub
1. Start **Docker (dockerdesktop)** locally.
2. Open a command prompt window on your local computer.
3. Enter the code below to pull the ASP.NET Sample app image from the Docker Hub registry. This image contains a sample web app developed by Microsoft, and is based on the default ASP.NET template available in Visual Studio.
```
docker pull mcr.microsoft.com/dotnet/samples:aspnetapp
```
```
**Output**

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
