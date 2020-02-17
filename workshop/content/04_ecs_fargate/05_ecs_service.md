+++
title = "ECS Service"
date = 2020-02-10T14:00:00+11:00
weight = 5
+++

## What is an ECS Service?

Amazon ECS allows you to run and maintain a specified number of instances of a task definition simultaneously in an Amazon ECS cluster. This is called a service. If any of your tasks should fail or stop for any reason, the Amazon ECS service scheduler launches another instance of your task definition to replace it and maintain the desired count of tasks in the service depending on the scheduling strategy used.

In addition to maintaining the desired count of tasks in your service, you can optionally run your service behind a load balancer. The load balancer distributes traffic across the tasks that are associated with the service.

{{% notice info %}}
[Click here](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs_services.html) to learn more about ECS Services.
{{% /notice %}}

## Creating a service in the ECS

Click on `Task Definitions` menu, select `awsbuilders-task-definition` and then select `awsbuilders-task-definition:1`.

![](/images/ecs_fargate/ecs_fargate_service_1.png)

Click on `Actions` and then select `Create Service`.

![](/images/ecs_fargate/ecs_fargate_service_2.png)

Select the options below:

1. Launch type: `Fargate`
2. Cluster: `awsbuilders-cluster`
3. Service Name: `awsbuilders-task-service`

Also, insert the number `1` for `Number of tasks`.

![](/images/ecs_fargate/ecs_fargate_service_3.png)

Select `Rolling update` and click on `Next Step`.

{{% notice info %}}
[Click here](https://aws.amazon.com/blogs/devops/use-aws-codedeploy-to-implement-blue-green-deployments-for-aws-fargate-and-amazon-ecs/) to learn more about Blue/Green deployment and ECS.
{{% /notice %}}

![](/images/ecs_fargate/ecs_fargate_service_4.png)

Select your default VPC and at least two subnets.

These are the subnets where your containers will be running.

{{% notice warning %}}
This is for testing purposes only. In a production environment, you must use multilayered design to avoid exposing your containers.
{{% /notice %}}

![](/images/ecs_fargate/ecs_fargate_service_5.png)

Keep scrolling down - select `Application Load balancer` and click on `EC2 Console` to create a new load balancer.

![](/images/ecs_fargate/ecs_fargate_service_6.png)

Let's create an `Application load balancer` to be in front of your application.

![](/images/ecs_fargate/ecs_fargate_service_7.png)

Type `awsbuilders-alb` for the name and select `internet facing`.

Also, select your default vpc and at least two subnets.

![](/images/ecs_fargate/ecs_fargate_service_8.png)

Click on `Next: Configure Security groups`.

![](/images/ecs_fargate/ecs_fargate_service_9.png)

Select `Create a new security group` and then click on `Next: Configure Routing`.

![](/images/ecs_fargate/ecs_fargate_service_10.png)

Create a new targe group and select `IP` as a `Target Type` and then click on `Next: Register targets`.

![](/images/ecs_fargate/ecs_fargate_service_11.png)

Don't add any target now and click on `Next: Review`.

![](/images/ecs_fargate/ecs_fargate_service_12.png)

Review the settings and click on `Create` to deploy your Application Load Balancer.

![](/images/ecs_fargate/ecs_fargate_service_13.png)

Return to the ECS Service tab and refresh the load balancer list.

You should be able to select the newly created ALB.

![](/images/ecs_fargate/ecs_fargate_service_15.png)

Click on `Add to load balancer`.

![](/images/ecs_fargate/ecs_fargate_service_16.png)

Now, you select the target group name `awsbuilders-alb-targetgroup`.

![](/images/ecs_fargate/ecs_fargate_service_17.png)

Move to the next step by clicking on `Next Step`.

![](/images/ecs_fargate/ecs_fargate_service_18.png)

Finally, hit the button `Create Service`.

![](/images/ecs_fargate/ecs_fargate_service_19.png)

Check if all steps are green and click on `View Service` to open the new ECS Service.

![](/images/ecs_fargate/ecs_fargate_service_20.png)



