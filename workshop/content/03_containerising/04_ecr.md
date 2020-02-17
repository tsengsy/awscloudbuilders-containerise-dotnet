+++
title = "Amazon ECR"
date = 2020-02-10T14:00:00+11:00
weight = 4
+++

## Amazon ECR

Amazon Elastic Container Registry (ECR) is a fully-managed Docker container registry which makes it easy for developers to store, manage, and deploy Docker container images. Amazon ECR is integrated with Amazon Elastic Container Service (ECS), simplifying your development to production workflow. Amazon ECR eliminates the need to operate your own container repositories or worry about scaling the underlying infrastructure. Amazon ECR hosts your images in a highly available and scalable architecture, allowing you to reliably deploy containers for your applications. Integration with AWS Identity and Access Management (IAM) provides resource-level control of each repository. With Amazon ECR, there are no upfront fees or commitments. You pay only for the amount of data you store in your repositories and data transferred to the Internet.

{{% notice info %}}
[Click here](https://aws.amazon.com/ecr/) to learn more about AWS ECR.
{{% /notice %}}

## Creating the ECR repository

Open the AWS Console and search for ECR.

![console](/images/containerising/containerising_1_console_ecr.png)

Click on `Get started`.

![splash](/images/containerising/containerising_2_ecr_splash.png)

Insert the name `awsbuilders-dotnet` for the repository name and click on `Create repository`.

![new](/images/containerising/containerising_3_ecr_new.png)

`Image URI` will be used for further steps, so lets copy this.

After copying the `Image URI`, select the `awsbuilders-dotnet` repository.

![list](/images/containerising/containerising_4_ecr_repo_list.png)

This is your repository and all images will be stored here.

Click on `View Push Commands`

![repo](/images/containerising/containerising_5_ecr_repo.png)

These are the commands and instructions to authenticate, build and push your image to the AWS ECR service.

![commands](/images/containerising/containerising_6_ecr_commands.png)


## Pushing the container to Amazon ECR

Let’s recap.

1. You have successfully created a Dockerfile
2. Built your Docker image
3. Provisioned ECR

Now, you need to upload your image to your remote registry.

Use the commands 1, 3 and 4 from the ECR push commands window in order to upload your image.