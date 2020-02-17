+++
title = "Dockerfile"
date = 2020-02-10T14:00:00+11:00
weight = 2
+++

## What is a Dockerfile?

A Dockerfile is file containing build instructions to assemble a docker image, the file contains commands like RUN, COPY or WORKDIR.

{{% notice info %}}
[Click here](https://docs.docker.com/engine/reference/builder/) to learn more about dockerfile.
{{% /notice %}}

## Creating the dockerfile

Before we start, ensure that your terminal is pointing to the right folder.

    cd ~/environment/awscloudbuilders-containerise-dotnet/
    
Lets create the Dockerfile.

    nano Dockerfile
    
{{% notice info %}}
You may use a different text editor instead of nano.
{{% /notice %}}

Copy the commands into the `Dockerfile` from the text below.

Each step has been commented to describe what the step action.

    # FROM sets the base image as sdk:3.1 from microsoft
    # https://hub.docker.com/_/microsoft-dotnet-core
    FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
    
    # Sets the working directory for commands like RUN , ENTRYPOINT and COPY
    WORKDIR /source
    
    # copy csproj and restore as distinct layers
    COPY *.sln .
    COPY aspnetapp/*.csproj ./aspnetapp/
    RUN dotnet restore -r linux-x64 
    
    # copy everything else to build app
    COPY aspnetapp/. ./aspnetapp/
    WORKDIR /source/aspnetapp
    
    # Build the application to the /app folder
    RUN dotnet publish -c release -o /app -r linux-x64 --self-contained false --no-restore
    
    # final stage/image
    # 3.1-bionic used for Ubuntu 18.04
    FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-bionic
    WORKDIR /app
    
    # Copy artifacts from the previous docker build
    COPY --from=build /app ./
    ENTRYPOINT ["./aspnetapp"]
    
{{% notice info %}}
References:

[dotnet restore](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-restore?tabs=netcore2x)
[dotnet publish](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-publish?tabs=netcore21)
{{% /notice %}}

Save the file by pressing 

    1. CONTROL + X 
    2. Y
    3. Enter 

{{% notice info %}}  
If you use a different text editor - the commands would be different.
{{% /notice %}}

## Lets build and test the image locally 

Build the image and add the tag `aspnetapp`.

    docker build -t awsbuilders-dotnet .

Run the image in the background and expose the port 8000.

    docker run --rm -d -it -p 8000:80 awsbuilders-dotnet

Use the command `curl` to comfirm the container is serving the webpage.

    curl http://0.0.0.0:8000
    
{{% notice info %}}
The `command` above prints the contents of the html file if the container is running.
{{% /notice %}}

## Cleanup

If you would like to stop the container, you can use the following steps to find and stop the container.

    docker ps

    docker stop CONTAINER_ID