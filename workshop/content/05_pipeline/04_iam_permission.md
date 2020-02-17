+++
title = "IAM Permission"
date = 2020-02-10T14:00:00+11:00
weight = 4
+++

## Add Amazon ECR Permissions to the CodeBuild Role

As mentioned earlier, the buildspec.yml file is responsible for creating and saving your image in the AWS ECR. These next steps add permission to the codebuild, allowing the service to upload the generated image to the remote repository; otherwise, the pipeline process will fail during the build process.

If you quickly examine the status of your newly created pipeline, you will see that it has failed and the reason behind it is because the code-build user is not allowed to upload the image, so let's fix it.

In the AWS Console, search for `IAM`.

![](/images/pipeline/pipeline_iam_1.png)

Click on `Roles` and then `codebuild-awsbuilders-codebuild-servicerole`.

![](/images/pipeline/pipeline_iam_2.png)

Click on `Attach Policies`.

![](/images/pipeline/pipeline_iam_3.png)

Search for the policy `AmazonEC2ContainerRegistryPowerUser`.

Select the policy and hit `Attach policy`.

![](/images/pipeline/pipeline_iam_4.png)

