+++
title = "Cloud 9 Environment"
date = 2020-02-10T14:00:00+11:00
chapter = false
weight = 3
+++

Today you'll be working in the `AWS Cloud9` IDE.

To help you get hands-on as quickly as possible and to avoid installing any libraries on your machine, we will be using the `AWS Cloud9 IDE`.

AWS Cloud9 is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser. It includes a code editor, debugger, and terminal. Cloud9 comes prepackaged with essential tools for popular programming languages, including JavaScript, Python, PHP, and more, so you don’t need to install files or configure your development machine to start new projects. 

{{% notice info %}}
[Click here](https://aws.amazon.com/cloud9/) to learn more about AWS Cloud 9.
{{% /notice %}}

Let's get started by creating an `AWS Cloud9`using the [AWS Cloud9 console - AP-SOUTHEAST-2](https://ap-southeast-2.console.aws.amazon.com).

{{% notice info %}}
We will be using the Sydney Region for this lab - please double check your cloud 9 environment is set to the AP-SOUTHEAST-2 region.
{{% /notice %}}

## Steps to setup your Cloud9 environment

Search for Cloud9 using the search box.

![console](/images/setup/setup_03_cloud9_1_console.png)

On the Cloud9 splash page, click on `Create Environment`.

{{% notice info %}}
You won't see the splash page if you already have a Cloud9 instance, however, don't re-use any instance that you have created and create a new environment. 
{{% /notice %}}

![create-env](/images/setup/setup_03_cloud9_2_create.png)

Type the name of your instance - e.g. `awsbuilder-cloud9`.

![wizard-name](/images/setup/setup_03_cloud9_3_newwizard1.png)

Leave the default setting and click on `Next Step`.

![wizard-config](/images/setup/setup_03_cloud9_4_newwizard2.png)

Click on `Create environment` and wait.

![wizard-last](/images/setup/setup_03_cloud9_5_newwizard3.png)

Cloud9 will provision your environment and it may take up to 5 minutes to complete.

![environment](/images/setup/setup_03_cloud9_6_starting.png)

Welcome to the Cloud9 environment :)

![environment](/images/setup/setup_03_cloud9_7_environment.png)

1. Blue - any files downloaded to your environment will appear here in the file tree. 
2. Red - any documents you open will show up here. Test this out by double clicking on README.md in the left pane and edit the file by adding some arbitrary text. Then save it by clicking File and Save. Keyboard shortcuts will work as well. 
3. Yellow - it is a bash shell, for the remainder of the lab, use this shell to enter all commands.


