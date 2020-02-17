+++
title = "Buildspec"
date = 2020-02-10T14:00:00+11:00
weight = 2
+++

## What is a Buildspec file?

A build spec is a collection of build commands and related settings, in YAML format, that CodeBuild uses to run a build. You can include a buildspec as part of the source code or you can define a buildspec when you create a build project. 

{{% notice info %}}
[Click here](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html) to learn more about buildspec.
{{% /notice %}}

## Creating Buildspec file

Let's create the buildspec.yml to automate the process that you have done through the `Containerising` chapter.

The buildspec file will be responsible for building the new image, upload it to ECR and then kick the next step of our pipeline.

Before we start, ensure that your terminal is pointing to the right folder.

    cd ~/environment/awscloudbuilders-containerise-dotnet/
    
Lets create the buildspec file.

    nano buildspec.yml
    
Copy all the commands below and replace `[[REPO URI]]` with the AWS ECR URI that you created in the `containerizing` chapter.

> Example of AWS ECR: account-ID.dkr.ecr.region-ID.amazonaws.com/your-Amazon-ECR-repo-name

{{% notice info %}}
Remove the :latest or any tag from the AWS ECR as the buildspec adds it automatically for you.
{{% /notice %}}
    
    version: 0.2
    
    phases:
      install:
        runtime-versions:
          docker: 18
      pre_build:
        commands:
          - echo Logging in to Amazon ECR...
          - aws --version
          - $(aws ecr get-login --region $AWS_DEFAULT_REGION --no-include-email)
          - REPOSITORY_URI=[[REPO URI]]
          - COMMIT_HASH=$(echo $CODEBUILD_RESOLVED_SOURCE_VERSION | cut -c 1-7)
          - IMAGE_TAG=${COMMIT_HASH:=latest}
      build:
        commands:
          - echo Build started on `date`
          - echo Building the Docker image...
          - docker build -t $REPOSITORY_URI:latest .
          - docker tag $REPOSITORY_URI:latest $REPOSITORY_URI:$IMAGE_TAG
      post_build:
        commands:
          - echo Build completed on `date`
          - echo Pushing the Docker images...
          - docker push $REPOSITORY_URI:latest
          - docker push $REPOSITORY_URI:$IMAGE_TAG
          - echo Writing image definitions file...
          - printf '[{"name":"awsbuilders-task-container","imageUri":"%s"}]' $REPOSITORY_URI:$IMAGE_TAG > imagedefinitions.json
    artifacts:
        files: imagedefinitions.json
        
Save the file by pressing 

    1. CONTROL + X 
    2. Y
    3. Enter 

The build specification was written for the following task definition, used by the Amazon ECS service for this tutorial. The REPOSITORY_URI value corresponds to the image repository (without any image tag), and the hello-world value near the end of the file corresponds to the container name in the service's task definition.

## Commit the buildspec file

Follow the instructions below using the terminal.

Add all files to the git staging area.

    git add * 

Record the changes to the repository, so we can push to the server.

    git commit -m "Buildspec file"
    
Push all committed changes to the server.

    git push origin master