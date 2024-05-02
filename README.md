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
1. Stop the container, it is still loaded and can be restarted. Run the following command in the command prompt window to remove it, replacing `<NAME>` or `<ID>` placeholder with the name of your container. Run:
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
# Customise a Docker Image to run a Personlised Web App
We have looked at how we can pull an image from **Docker Hub**. Docker Hub offers a great selection of images to help kickstart our containerised app development. You can easily obtain an image with the essential features DevOps need and then add our own application on top of it to create a personalised image. To streamline this process, we can automate the steps by creating a **Dockerfile**. <p>

A **Dockerfile** contains the steps for building a custom Docker image.<p>
When a DevOps choses to utilise `Docker` to deploy one of the organisation's web applications. The selected web app is a straightforward implementation of a web `API` for a hotel reservations website. The web API allows for `HTTP POST` and `GET` operations to create and retrieve customer bookings.<p><p>

In this section, we will create a `Dockerfile` for a web application that currently does not have one. Afterward, build the image and run it in our local environment.

## Create a Dockerfile for the web app
1. Start `Docker Desktop`
2. Make a new directory called booking_web_app and `cd` into it 
```
mkdir booking_web_app    # creates the working directoy 
cd booking_web_app       # change directory to booking_web_app
``` 
3. Clone the web app repo: Execute the command in your local computer's command prompt window or a terminal in an IDE to download the source code for the web app.
```
git clone https://github.com/MicrosoftDocs/mslearn-hotel-reservation-system.git
```
4. Change directory to mslearn-hotel-reservation-system and list the files within.
```
cd mslearn-hotel-reservation-system
ls
```
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/731558c5-9d63-4d66-bb07-91f3304b7204)<p>
There is a sourcecode (`src`) amongst the listed output. This is the source code to build the web app. <p>
4. Enter the following command to open the `src` directory.
```
cd mslearn-hotel-reservation-system/src
```
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/d8e91104-13c3-49e4-93e2-67317e02e80f)<p>
5. In the src directory, use the following commands to generate a new file called Dockerfile and then open it in Notepad or Text editor.
```
copy NUL Dockerfile               # Create the Dockerfile on windows cmd prompt
notepad Dockerfile                # Edit the Dockerfile in Windows Notepa
#######################################################################################
vi Dockerfile                   # Create and edit the Dockerfile in Linux/Mac/GitBash
```
6. Add the following code to the Dockerfile:
```
FROM mcr.microsoft.com/dotnet/core/sdk:2.2
WORKDIR /src
COPY ["/HotelReservationSystem/HotelReservationSystem.csproj", "HotelReservationSystem/"]
COPY ["/HotelReservationSystemTypes/HotelReservationSystemTypes.csproj", "HotelReservationSystemTypes/"]
RUN dotnet restore "HotelReservationSystem/HotelReservationSystem.csproj"
```
The `Dockerfile` script includes instructions to retrieve an image that includes the **.NET Core Framework SDK**. It also copies the project files for the web app `(HotelReservationSystem.csproj)` and the library project `(HotelReservationSystemTypes.csproj)` to the **/src** folder within the container. Additionally, the `dotnet restore` command is used to download the necessary dependencies from **NuGet** for these projects.
7. Append the following code to the bottom of the Dockerfile:
```
COPY . .
WORKDIR "/src/HotelReservationSystem"
RUN dotnet build "HotelReservationSystem.csproj" -c Release -o /app
```
Copy the web app's source code to the container and then execute the dotnet build command to compile the app. The compiled DLLs will be saved to the /app directory within the container. 

8. Add the following command to the end of the Dockerfile.
```
RUN dotnet publish "HotelReservationSystem.csproj" -c Release -o /app
```
The `dotnet publish` command transfers the website's executable files to a fresh directory while eliminating any temporary files. The files in this directory can be deployed to a website.
9. At the end of the Dockerfile, add
```
EXPOSE 80
WORKDIR /app
ENTRYPOINT ["dotnet", "HotelReservationSystem.dll"]
```
The `initial` command, `EXPOSE 80`, allows access to port 80 within the container. The subsequent command navigates to the `/app` directory where the published version of the web app is located. The last command sets the container to run and execute the `dotnet HotelReservationSystem.dll` command, which contains the compiled code for the web app.
10. Please save the document and then close the text editor. 
**N/B**: In Windows Notepad, ensure that it is save as `All Files` with no file extension.<p>
The full `Dockerfile` will look like this:
```
FROM mcr.microsoft.com/dotnet/core/sdk:2.2
WORKDIR /src
COPY ["/HotelReservationSystem/HotelReservationSystem.csproj", "HotelReservationSystem/"]
COPY ["/HotelReservationSystemTypes/HotelReservationSystemTypes.csproj", "HotelReservationSystemTypes/"]
RUN dotnet restore "HotelReservationSystem/HotelReservationSystem.csproj"
COPY . .
WORKDIR "/src/HotelReservationSystem"
RUN dotnet build "HotelReservationSystem.csproj" -c Release -o /app
RUN dotnet publish "HotelReservationSystem.csproj" -c Release -o /app
EXPOSE 80
WORKDIR /app
ENTRYPOINT ["dotnet", "HotelReservationSystem.dll"]
```
## Build and deploy the image using the Dockerfile
1. Build the Image: use the following commands to create the image for the sample app using the Dockerfile. Ensure to include a period `.` at the end of the command. This command will create the image and save it locally with the name reservationsystem. Confirm that the image is successfully created. When the process is complete, we may see warnings about file and directory permissions, which can be ignored for this exercise.<p>
**Note**:The image may take some time to build.
```
docker build -t reservationsystem .
```
The docker build command operates by creating a container, executing commands within it, and subsequently saving the modifications as a new image.<p>
**output**:
```
[+] Building 745.4s (15/15) FINISHED                                  docker:default
 => [internal] load build definition from Dockerfile                            0.0s
 => => transferring dockerfile: 624B                                            0.0s
 => [internal] load metadata for mcr.microsoft.com/dotnet/core/sdk:2.2          1.0s
 => [internal] load .dockerignore                                               0.0s
 => => transferring context: 2B                                                 0.0s
 => [ 1/10] FROM mcr.microsoft.com/dotnet/core/sdk:2.2@sha256:42699bba2fe454  687.0s
 => => resolve mcr.microsoft.com/dotnet/core/sdk:2.2@sha256:42699bba2fe4545dd7  0.0s
 => => sha256:9935d0c62ace92b388be202275e222007d6cac10b9c1f 10.80MB / 10.80MB  44.9s
 => => sha256:2357b6790b9df0fb28364d113ff94eb67628cb1564aa8607 4.40kB / 4.40kB  0.0s
 => => sha256:146bd6a886182fde06fbf747470b1c89814bc8ab1c96 45.38MB / 45.38MB  158.4s
 => => sha256:db0efb86e80601b5bbdbb7c406426982c4202d339687c14 4.34MB / 4.34MB  12.7s 
 => => sha256:42699bba2fe4545dd753694499e6db08478ba5b3bcc34b92 2.19kB / 2.19kB  0.0s 
 => => sha256:db9b38d066fdbdd5ac5ce862076c27e4ae17f2b57cbacd03 1.80kB / 1.80kB  0.0s 
 => => sha256:e705a4c4fd310b96bfb3d7928428e65f0d3f5bad0cd0 50.07MB / 50.07MB  165.7s 
 => => sha256:563ac9aa7c8039c3169f383c57e43c0d8281d01f6b6c5 13.25MB / 13.25MB  85.6s 
 => => sha256:9db5b5c16f62413ee33c1b77d00b801b18b0a9bb8d 173.40MB / 173.40MB  478.6s
 => => extracting sha256:9935d0c62ace92b388be202275e222007d6cac10b9c1f2c1ea63a  0.6s
 => => extracting sha256:db0efb86e80601b5bbdbb7c406426982c4202d339687c14c3941b  0.2s
 => => extracting sha256:e705a4c4fd310b96bfb3d7928428e65f0d3f5bad0cd0bda1434ae  3.2s
 => => extracting sha256:563ac9aa7c8039c3169f383c57e43c0d8281d01f6b6c59a4f5b0e  0.2s
 => => extracting sha256:9db5b5c16f62413ee33c1b77d00b801b18b0a9bb8dd5151c35cad  2.2s
 => => extracting sha256:ff05a093e8aa7f92b287883ed215c63b767074e67aa2a730ae82  30.4s
 => [internal] load build context                                               0.1s
 => => transferring context: 16.05kB                                            0.1s
 => [ 2/10] WORKDIR /src                                                        0.4s
 => [ 3/10] COPY [/HotelReservationSystem/HotelReservationSystem.csproj, Hotel  0.1s
 => [ 4/10] COPY [/HotelReservationSystemTypes/HotelReservationSystemTypes.csp  0.0s
 => [ 5/10] RUN dotnet restore "HotelReservationSystem/HotelReservationSystem  48.3s
 => [ 6/10] COPY . .                                                            0.0s
 => [ 7/10] WORKDIR /src/HotelReservationSystem                                 0.0s
 => [ 8/10] RUN dotnet build "HotelReservationSystem.csproj" -c Release -o /ap  3.6s
 => [ 9/10] RUN dotnet publish "HotelReservationSystem.csproj" -c Release -o /  4.0s
 => [10/10] WORKDIR /app                                                        0.0s
 => exporting to image                                                          0.6s
 => => exporting layers                                                         0.5s
 => => writing image sha256:91e4b40129c006cfcb56f4581d576715b4de1145ea7beff2ee  0.0s
 => => naming to docker.io/library/reservationsystem                            0.0s

View build details: docker-desktop://dashboard/build/default/default/ohw4sr5b3xh1q3ow4418qgyyc

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview
```
2. List images: We will verify that the the `Dockerfile` execution has created the image and saved in the locally registry:
```
docker image list
```
**output**: The image will have the name `reservationsystem`. We'll also have an image named microsoft/dotnet:
```
REPOSITORY                       TAG           IMAGE ID       CREATED         SIZE
reservationsystem                latest        91e4b40129c0   7 minutes ago   1.87GB
```
Let is confirm from the `Docker Desktop`:<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/9438c04b-8f3f-4e18-a618-ab9338859206)<p>

## Test the web app
1. Run a container using the `reservationsystem` image: The output from Docker will be a long hexadecimal string. The container operates without a graphical interface in the background. `Port 80` within the container is linked or mapped to `port 8080` on the host machine. The container's name is `reservations`.
```
docker run -p 8080:80 -d --name reservations reservationsystem
```
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/2a03da68-6ecb-4fe6-9ab8-3a46ac9f5683)<p>
From the `Docker Desktop`, we can confirm if the container is running.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/81db78be-c9a6-4de1-a0c9-034b4f2ef644)<p>
We can see that the image status is `In Use` as compared to the status `Unuse` before running the container. See the container named `reservations` running the image `reservationsystem`:<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/93df9034-e589-44ee-b5f3-c71298fca442)<p>
2. Access the web app in the browser: Open a web browser and go to `http://localhost:8080/api/reservations/1` . We will be able to view a JSON object displaying the data for reservation number 1, similar to the example output shown below:<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/6ce5cc8d-1602-4c75-b4ac-a985c0e279c2)<p>
To view the details of a specific reservation, simply replace the "1" at the end of the localhost URL with a different reservation number, such as 2 or 20.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/bce11532-b850-443c-a26e-79b17b41d4f2)<p>
3. Verify that the container's `STATU`S is *Up*. Run:
```
docker ps -a
```
The output indicates the `status` is up: <p>
```
CONTAINER ID   IMAGE                                        COMMAND                  CREATED          STATUS                      PORTS                                                                                                                                  NAMES
ed5acef128ad   reservationsystem                            "dotnet HotelReserva…"   19 minutes ago   Up 19 minutes               0.0.0.0:8080->80/tcp                                          ```
```
4. Stop the  reservations container. To stop the container running, apply this command:
```
docker container stop reservations
```
The container has exited:<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/bf9fe494-4e86-44f0-bb1c-0352f92199cb)<p>
5. Delete the reservations container from the local registry.
```
docker rm reservations
```
The container has been removed:<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/a140df3a-3377-4062-95e7-42da304809bb)

# Deploy a Docker image to an Azure Container Instance
Previously, we packaged and tested a booking web app as a Docker image for local use. Now, the aim to utilise the results of that process to deploy the web application globally. To achieve this global availability, we will launch the image as an `Azure Container Instance`. <p>
`Azure Container Instance` allows DevOps team to run a Docker image within the Azure environment.<p>

In this section, we will learn how to rebuild the image for the web app and then transfer it to Azure Container Registry. Afterwards, we will utilize the Azure Container Instance service to run the image.
## Create a container registry
1. Sign in to the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com).
**N/B**: Azure subscription to to run this exercise, and might incur charges.
2. In the `Azure portal`, select `Create a resource` from the resource menu or the Home page to open the Create a resource pane.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/f0f7de6e-981e-4327-a851-5c67d9b0b42d)<p>
3. Choose `Containers` from the menu, then click on `Container Registry`.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/9bd361e5-d91d-4c97-87ee-4faba6ff2237)<p>
The pane for creating a container registry is displayed.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/85cf8a86-a148-4027-9d32-118071660e50)<p>

4. Input the specified values for each setting on the Basics tab.
Under `Project details`:<p>
- `Subscription` - Select your Azure subscription in which you're allowed to create and manage resources.
- `Resource group` - Create a new resource group with the name "learn-deploy-container-aci-rg". Remember this name, as it will be used in the rest of the project.<p>
**N/B**: We will clean up this resource when the project is completed.<p>

Under `Instance details`:
- `Registry name`  - Choose a name for the container registry. The registry name must be unique within Azure and contain between 5 and 50 alphanumeric characters.
- `Location` - Choose a location that is geographically close to you.
- `SKU` - Standard<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/bba3b44b-b3bc-4f5d-9750-5811fb582e28)

5. Click on `Review + create`. Once the `Validation passed` notification pops up, select `Create`. **Wait** until the container registry has been fully deployed before proceeding to the next step.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/4609a977-b521-4734-926c-8248ac6420a6)<p>

6.Click on `Go to resource`. This launch the Container registry pane, which displays key information about your newly created container registry.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/ab27256a-be1f-480a-8eff-f6fa23a839a7)<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/ea382d0e-d0f3-4ebe-988a-c1238cead268)<p>
7. In the resource menu, under the `Settings` section, click the dropdown next to settings and select `Access keys`. This will open the Access keys pane for your container registry.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/8324807a-8df8-429a-8ee3-14c897366b0b)<p>

8. If the Admin user setting is currently disabled, toggle the slider to enable the Admin user access key. Once enabled, the Username and Password for your container registry will be displayed.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/d44d1518-3b6a-402e-8810-cfd7723c4096)<p>

9. Record the following information for your container registry: the `Registry name`, `Login server`, `Username`, and `Password`.<p>
**N/B**: In this project, we are enabling the `admin account access` to allow for uploading images and testing the registry. However, in a `production environment`, it's important to `disable the Admin user account access` and instead use `Microsoft Entra ID Protection` as soon as you've confirmed the registry is functioning as expected.
## Upload the image for the hotel reservation system app to Azure Container Registry
1. Run the following command, replacing `<registry-name>` with the actual name of your container registry, to tag the current `reservationsystem` image with the name of your registry.
```
docker tag reservationsystem:latest <registry-name>.azurecr.io/reservationsystem:latest
```
2. Execute the `docker image ls` command to verify that the image has been tagged correctly.
```
docker image ls
```
The `output` should be similar to the following:
```
REPOSITORY                                            TAG           IMAGE ID       CREATED        SIZE
reservationsystem                                     latest        91e4b40129c0   14 hours ago   1.87GB
jonesdeploywebappaci25.azurecr.io/reservationsystem   latest        91e4b40129c0   14 hours ago   1.87GB
```
This image has also been populated in **Docker Desktop**.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/f1ffa66d-c90f-4e65-8dd3-420f3f294ac3)<p>

3. Sign in to the Azure Container Registry created. Use the `docker login` command and provide the login server for the registry that was noted earlier. When prompted, enter the username and password from the access keys you recorded previously.
```
docker login <login-server>
```
**N/B**: You may encounter an error message indicating that your application is not registered with Microsoft Entra ID. As mentioned earlier in this exercise, we have enabled the Admin user access key to facilitate testing of the deployment.
4. Enter the following command, replacing `<registry-name>` with the actual name of th registry created, to upload the image to your Azure Container Registry.
```
docker push <registry-name>.azurecr.io/reservationsystem:latest
```
## Verify the contents of the registry
1. In the Azure portal, navigate back to your container registry.

2. Under the Services section in the resource menu, select Repositories. This will take you to the Repositories pane for your container registry.

3. Verify that the **reservationsystem** repository is present. Select the **reservationsystem** repository and confirm that it contains an image with the **latest** tag.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/9ce307e0-597e-4004-b58f-f35a1cbd0503)<p>
![Reservationsystem](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/e7398b30-fc6a-44fd-874d-834245f54da6)<p>

## Load and run an image using Azure Container Instance
1. In the Azure portal, navigate to the `Create a resource` section. This will open the `Create a resource` pane.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/ec8f817f-c54f-46a3-b259-802879257edb)<p>
2. From the resource menu, select `Containers` and then choose `Container Instances`.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/56211850-db81-419d-833c-99e1bb13602a)<p>
3. Input the specified values for each setting on the Basics tab.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/befd0891-81be-4d65-8300-c8a129800c47)<p>

|Setting|Value|
| -------|------|
|Project details|
| Subscription	| Select your default Azure subscription in which you're allowed to create and manage resources |
| Resource group |	Reuse the existing resource group learn-deploy-container-aci-rg |
| Container details	|
| Container name |	hotelsysteminstance |
| Region |	Use the default location |
| Image source |	Docker Hub or other registry |
| Image type |	Private |
| Image |	registry-name.azurecr.io/reservationsystem:latest |
| Image registry login server |	Enter the login server name for your registry |
| Image registry username |	Enter the username for your registry |
| Image registry password |	Enter the password for your registry |
| OS Type |	Linux |
| Size |	Leave the default Size set to 1 vcpu, 1.5 GiB memory, 0 gpus | <p>
4. Proceed to the Networking section.
5. For each setting on the Networking tab, input the specified values.<p>

|Setting|Value|
| -------|------|
| Networking type |	Public |
| DNS name label	| Choose a unique name, which will be used as part of the container's URL |
| Ports	|
| Ports |	80 |
| Ports Protocol |	TCP |<p>

6. Choose Next: Advanced.
7. Under the Advanced tab, input the specified values for each setting.<p>

|Setting|Value|
| -------|------|
| Restart policy |	Always |
| Environment variables |	leave all settings blank |
| Command override |	leave blank |<p>

8. Choose **Review + Create**. Wait for validation to finish and make any necessary corrections.
9. Choose **Create**.<p>
![image](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/f7565cd9-c99e-4acc-96b9-3153d72fe982)<p>

10. Once the container instance is created, click on **Go to resource**. The container instance pane will appear.<p>
![hotelsysteminstance](https://github.com/JonesKwameOsei/Build-a-containerized-web-application-with-Docker-/assets/81886509/40cac7ba-2230-4bb1-8ce2-a507fa5a3308)<p>

11. Locate the **fully qualified domain name (FQDN)** of the container instance on the **Overview pane**.<p>

















