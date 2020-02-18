+++
title = "Auto Scaling"
date = 2020-02-10T14:00:00+11:00
weight = 1
+++

## Auto Scaling

The last step proved that ECS and Fargate are now serving your website and it is running as a container.

However, what happens during peak hours? Scaling up/down - would it be a great solution for your workload? 

Auto Scaling is a solution to adjust capacity on the fly by adding and removing tasks based on your load. 

It scales in and out, preventing you from paying unnecessary resources. In addition, it adjusts your tasks to absorb the current workload.

## Load test without Auto scaling

The tool `artillery` is a powerful solution for load testing.

The steps below will use this tool to emulate 100 new users per second for 600 seconds.

{{% notice info %}}
[Click here](https://artillery.io/) to learn more about Artillery.
{{% /notice %}}

Let's flood our application with hundreds of calls.

Using `Cloud9 Terminal`, install the artillery tool.

    npm install -g artillery 

Ensure that your terminal is pointing to the right folder.

    cd ~/environment/awscloudbuilders-containerise-dotnet/

Create the `ecs-load.yml` file.

    nano ecs-load.yml

Paste the configuration below and substitute the `YOUR_ALB_URL` with the address of your application.

    config:
    target: 'http://awsbuilders-alb-1986142420.ap-southeast-2.elb.amazonaws.com'
    phases:
        - duration: 600
        arrivalRate: 100
    http:
        pool: 10
    scenarios:
    - flow:
        - get:
            url: "/"

Save the file by pressing 

    1. CONTROL + X 
    2. Y
    3. Enter 

Run the command

    artillery run ecs-load.yml

The output from the command above should be similar to the lines below.

    Started phase 0, duration: 300s @ 12:25:16(+0000) 2020-02-18
    Report @ 12:25:26(+0000) 2020-02-18
    Elapsed time: 10 seconds
    Scenarios launched:  4994
    Scenarios completed: 2030
    Requests completed:  2030
    RPS sent: 502.31
    Request latency:
        min: 4
        max: 5854.9
        median: 2483.9
        p95: 5572
        p99: 5844.4
    Codes:
        200: 2030

Leave the terminal running the `artillery` and open the Amazon ECS console.

Click on `Cluster` and then click on `awsbuilders-cluster`.

![](/images/extra/extra_auto_scaling_withoutAS_1.png)

Open the service `awsbuilders-task-service`.

![](/images/extra/extra_auto_scaling_withoutAS_2.png)

Click on `Metrics` and open the Cloudwatch link for the metric `CPUUtilization`.

![](/images/extra/extra_auto_scaling_withoutAS_3.png)

Adjust the `period` to `1 minute` and setup the graph to display the last `15 minutes`.

As highlighted in yellow below, the CPU utilization of your single task is increasing significantly due to the heavy load.

![](/images/extra/extra_auto_scaling_withoutAS_4.png)

Go back to your `Cloud9 Terminal` and stop the artillery tool by pressing `CONTROL + C`.

## Setup the Auto Scaling

Open the cluster `awsbuilders-cluster` and then click on your service.

![](/images/extra/extra_auto_scaling_withAS_2.png)

Click on `Update`.

![](/images/extra/extra_auto_scaling_withAS_3.png)

Click on `Next step`.

![](/images/extra/extra_auto_scaling_withAS_4.png)

Once again, click on `Next step`.

![](/images/extra/extra_auto_scaling_withAS_5.png)

Select the `Configure Service Auto Scaling to adjust your service’s desired count` and then insert the values below:

1. Minimum number of tasks: `2`
2. Desired number of tasks: `2`
3. Maximum number of tasks: `10`
4. IAM role for Service Auto Scaling: `Create new role`

The settings above configure auto scaling to keep at least two tasks running, with a maximum of 10 tasks running at the same time.

{{% notice info %}}
[Click here](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-auto-scaling.html) to learn more about ECS and Auto Scaling.
{{% /notice %}}

Click on `Add scaling policy`.

![](/images/extra/extra_auto_scaling_withAS_6.png)

Select `Target Tracking` and insert the values below:

1. Policy name: `awsbuilders-autoscaling`
2. Target value: `5`
3. Scale-out cooldown period: `2`
4. Scale-in cooldown period: `2`

The auto scaling policy will keep your metric as close as possible to the target value of 5%. Also, it won't scale in/out within 2 seconds from the last scaling activity.

{{% notice info %}}
[Click here](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-autoscaling-targettracking.html) to learn more about Target Tracking Scaling Policies.
{{% /notice %}}

{{% notice info %}}
[Click here](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-autoscaling-stepscaling.html) to learn more about Step Scaling Policies
{{% /notice %}}

Click on `Save`.

![](/images/extra/extra_auto_scaling_withAS_7.png)

Click on `Next Step`.

![](/images/extra/extra_auto_scaling_withAS_8.png)

Update the service by click on `Update Service`.

![](/images/extra/extra_auto_scaling_withAS_9.png)

Wait for the changes to apply.

![](/images/extra/extra_auto_scaling_withAS_10.png)

Your service is now provisioning the extra task as per the previous change.

Wait until the second task change the `Desired status` to `Running`.

![](/images/extra/extra_auto_scaling_withAS_11.png)

## Second load test

Run the artillery command again.

    artillery run ecs-load.yml

Watch the cloudwatch metric `CPUUtilization` for 10 minutes and you should see a similar graph as per the below image.

Basically, auto scaling adds more tasks to reduce the cpu utilization as the workload increases. It also removes the unnecessary tasks once the load is reduced.

![](/images/extra/extra_auto_scaling_withAS_12.png)

Check the running tasks in the `Tasks` pane of your service.

![](/images/extra/extra_auto_scaling_withAS_13.png)