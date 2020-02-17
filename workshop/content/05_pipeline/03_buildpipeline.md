+++
title = "Building the Pipeline"
date = 2020-02-10T14:00:00+11:00
weight = 3
+++

## Codepipeline

AWS CodePipeline is a fully managed continuous delivery service that helps you automate your release pipelines for fast and reliable application and infrastructure updates. CodePipeline automates the build, test, and deploy phases of your release process every time there is a code change, based on the release model you define. This enables you to rapidly and reliably deliver features and updates. You can easily integrate AWS CodePipeline with third-party services such as GitHub or with your own custom plugin. With AWS CodePipeline, you only pay for what you use. There are no upfront fees or long-term commitments.

![](/images/pipeline/pipeline_buildingpipeline_0.png)

{{% notice info %}}
[Click here](https://aws.amazon.com/codepipeline/) to learn more about codepipeline.
{{% /notice %}}

## Building the Pipeline

In your AWS Console, search for `CodePipeline`.

![](/images/pipeline/pipeline_buildingpipeline_1.png)

Click on `Create Pipeline`.

![](/images/pipeline/pipeline_buildingpipeline_2.png)

Use `awsbuilders-codepipeline` for the name and click on `Next`.

![](/images/pipeline/pipeline_buildingpipeline_3.png)

Select `GitHub` for your source and click on `Connect to GitHub`.

![](/images/pipeline/pipeline_buildingpipeline_4.png)

Sign in using your GitHub credentials used to fork the repository.

![](/images/pipeline/pipeline_buildingpipeline_5.png)

Select the repository that you forked, the `master` branch and click on `Next`.

The codepipeline using webhooks will automatically trigger your pipeline if any changes are detected in the main branch.

![](/images/pipeline/pipeline_buildingpipeline_6.png)

Select `AWS Codebuild` as a build provider and click on `Create Project`.

![](/images/pipeline/pipeline_buildingpipeline_7.png)

Use `awsbuilders-codebuild` for the name.

![](/images/pipeline/pipeline_buildingpipeline_8.png)

Select the options below:

1. Managed Image
2. Ubuntu
3. Standard
4. aws/codebuild/standard:3.0
5. Enable the option `Enable this flag if you want to build Docker images or want your builds to get elevated privileges`.

![](/images/pipeline/pipeline_buildingpipeline_9.png)

Keep scrolling down - click on `Continue to CodePipeline`.

![](/images/pipeline/pipeline_buildingpipeline_10.png)

Click on `Next`

![](/images/pipeline/pipeline_buildingpipeline_11.png)

Select the options below:

1. Amazon ECS
2. `awsbuilders-cluster`
3. `awsbuilders-task-services`

Click on `Next`.

![](/images/pipeline/pipeline_buildingpipeline_12.png)

Review and create the pipeline.

![](/images/pipeline/pipeline_buildingpipeline_13.png)