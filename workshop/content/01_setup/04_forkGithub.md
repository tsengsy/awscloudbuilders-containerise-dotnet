+++
title = "Fork the Github Repo"
date = 2020-02-10T14:00:00+11:00
chapter = false
weight = 4
+++

## Github

Github is popular among software developers as it simplifies the process of collaborating on projects; moreover, team members can work on files and easily merge their changes. During the lab, you'll be using Github to deploy your .NET application using the [AWS CodePipeline](https://aws.amazon.com/codepipeline/).

Forking a repository allows you to freely change the code of a repository without affecting the original github account. Most commonly, forks are used to either propose changes to a project or to use the repository as a starting point for a new project.

You'll be forking a public repository containing a .NET application that needs to be containerised. All commits made to the forked repository will trigger a CI/CD pipeline which will deploy ECS/Fargate containers.

As an alternative, AWS CodeCommit is a fully-managed source control service that hosts secure Git-based repositories. It makes it easy for teams to collaborate on code in a secure and highly scalable ecosystem. CodeCommit eliminates the need to operate your own source control system or worry about scaling its infrastructure. [Click here](https://aws.amazon.com/codecommit/) to learn more

## Steps to fork the repository

Open the repository [https://github.com/matheuscanela/awscloudbuilders-containerise-dotnet](https://github.com/matheuscanela/awscloudbuilders-containerise-dotnet) and click on `Sign in`.

![repo](/images/setup/setup_04_forkGithub_1_repo.png)

Type your username and password and click on `Sign in`.

![login](/images/setup/setup_04_forkGithub_2_login.png)

Click on Fork.

![fork](/images/setup/setup_04_forkGithub_3_fork.png)

Wait for Github to copy the repository and save into your account.

![forking](/images/setup/setup_04_forkGithub_4_forking.png)

Now, copy the repository url and save as you'll be using this for the following steps.

![url](/images/setup/setup_04_forkGithub_5_url.png)




