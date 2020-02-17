+++
title = "ECS Task"
date = 2020-02-10T14:00:00+11:00
weight = 4
+++

## ECS Task Definitions

A task definition contains parameters needed to run Docker containers on Amazon ECS. For example, the docker image and the amount of resources allocated to execute the container are some of the parameters defined in the task definition. In addition, each task definition supports multiple containers.

{{% notice info %}}
[Click here](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task_definitions.html) to learn more about ECS Task Definitions.
{{% /notice %}}

## Creating the ECS Task

Using the AWS Console, search for `ECS`

![](/images/ecs_fargate/ecs_fargate_task_0.png)

Click on `Task Definitions` 

![](/images/ecs_fargate/ecs_fargate_task_1.png)

Start the task definition wizard by clicking on `Create New Task Definition`

![](/images/ecs_fargate/ecs_fargate_task_2.png)

Select `Fargate` and click on `Next Step`. 

{{% notice info %}}
ECS can also be deployed to EC2 instances, [click here](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/launch_container_instance.html) to learn more.
{{% /notice %}}

![](/images/ecs_fargate/ecs_fargate_task_3.png)

Fill in the `Task Definition Name` field with `awsbuilders-task-definition` 


![](/images/ecs_fargate/ecs_fargate_task_4.png)

Keep scrolling down - Select 0.5GB for `Task Memory (GB)` and 0.25vCPU for `Task CPU vCPU`

![](/images/ecs_fargate/ecs_fargate_task_5.png)

Let's create your container - click on `Add container`

![](/images/ecs_fargate/ecs_fargate_task_6.png)

Use `awsbuilders-task-container` for the container name and paste the `Image URI` copied from the AWS ECR console to fill in the `image` field. Don't forget to add `:latest` to the end of the URI.

> Example: 123456789012.dkr.ecr.ap-southeast-2.amazonaws.com/awsbuilders-dotnet:latest

Before clicking on `Update`, set the `Port mappings` to 80 TCP

![](/images/ecs_fargate/ecs_fargate_task_7.png)

After creating the container, click on `create` to finalize the task definition wizard.

![](/images/ecs_fargate/ecs_fargate_task_8.png)