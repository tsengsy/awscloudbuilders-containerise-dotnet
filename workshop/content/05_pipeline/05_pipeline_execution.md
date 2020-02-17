+++
title = "Pipeline Execution"
date = 2020-02-10T14:00:00+11:00
weight = 5
+++

## Pipeline Status

Using the AWS Console, search for `CodePipeline` and select the pipeline that you created.

![](/images/pipeline/pipeline_exec_0.png)

Click `Release Change` to force the CodePipeline to run from the beginning.

If the application, Dockerfile, buildspec.yml, ECR and other pipeline services are correct, you should see all steps in green when the execution is completed.

See the example below of an execution that completed without errors.

![](/images/pipeline/pipeline_exec_1.png)

## ECS Containers

Let's get back to the AWS ECS console and open the cluster `awsbuilders-cluster`.

![](/images/pipeline/pipeline_exec_2.png)

Now click on `awsbuilders-task-service`.

![](/images/pipeline/pipeline_exec_3.png)

The events tab shows all steps taken during the 

![](/images/pipeline/pipeline_exec_4.png)

{{% notice info %}}
[Click here](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/container-instance-draining.html) to learn more about Container Instance Draining.
{{% /notice %}}

