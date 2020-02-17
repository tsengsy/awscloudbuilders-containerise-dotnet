+++
title = "Clone Github Repo"
date = 2020-02-10T14:00:00+11:00
chapter = false
weight = 5
+++

In order to containerise the .NET application, you will need to clone the repository in your cloud9 machine.

All changes made to the code will be pushed to the GitHub using the git command line.

{{% notice info %}}
[Click here](https://git-scm.com/doc) to learn more about Git.
{{% /notice %}}

## Steps to clone the repository

Create a local copy of the forked repository.

    git clone HTTPS_URL_FORKED_REPO 
    
{{% notice info %}}
Use the URL copied from your forked repository
{{% /notice %}}

Access the folder created by the command above.

    cd awscloudbuilders-containerise-dotnet
    
Lets update the README file to push some changes and setup the github authentication.

    echo -e "\n#### Repo forked, lets go" >> README.md
    
Check if the text `#### Repo forked, lets go` was inserted at the end of the file.

    cat ~/environment/awscloudbuilders-containerise-dotnet/README.md
    
Setup the cache timeout for the GitHub password.

    git config --global credential.helper 'cache --timeout 10800'
   
{{% notice info %}}
[Click here](https://git-scm.com/book/en/v2/Git-Tools-Credential-Storage) to learn more about about how git handles password.
{{% /notice %}}
    
Add all files to the git staging area.

    git add * 

{{% notice info %}}   
[Click here](https://git-scm.com/docs/git-add) to learn more about git add.
{{% /notice %}}

Record the changes to the repository, so we can push to the server.

    git commit -m "First commit"
    
{{% notice info %}}
[Click here](https://git-scm.com/docs/git-commit) to learn more about git commit.
{{% /notice %}}

Push all committed changes to the server.

    git push origin master
    
{{% notice info %}}
[Click here](https://git-scm.com/docs/git-push) to learn more about git push.
{{% /notice %}}

Type username and password used to log in into your Github account.

You should see an output similar to the lines below which confirm the transmission to the remote server.

    Username for 'https://github.com/YOURUSER/awscloudbuilders-containerise-dotnet': YOURUSER
    Password for 'https://YOURUSER@github.com/YOURUSER/awscloudbuilders-containerise-dotnet': 
    Counting objects: 3, done.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 396 bytes | 396.00 KiB/s, done.
    Total 3 (delta 1), reused 0 (delta 0)
    remote: Resolving deltas: 100% (1/1), completed with 1 local object.
    To https://github.com/YOURUSER/awscloudbuilders-containerise-dotnet
       0482d5b..8ee1993  master -> master