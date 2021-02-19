# Setting up a demo environment

You will need to perform the below in Azure CloudShell in order to have the base environment, upon which we will build our demos. 

Note: the git commands below require some auth setup, see Appendix A at the end of this document.
### Get the code

```
mkdir ~/source
pushd ~/source

# This repo has all the setup scripts for LP5-S4 Setup
git clone https://dev.azure.com/ignite-tour-lp5/ignite-tour-lp5-s4/_git/ignite-tour-lp5-s4

# This repo has the database schema scripts
git clone https://github.com/Azure-Samples/tailwind-traders
```

### Set up the demo environment

By default, the scripts will set up two resource groups, one named `lp5s4-app-$USER`  and another called `lp5s4-db-$USER` so each person will have an individual standalone environment within the Ignite The Tour subscription.

All of the naming parameters and conventions are 

```
pushd ./ignite-tour-lp5-s4

# edit the params to meet your needs
code 0-params.sh

# Set up the environment
./setup.sh

popd  

```

Output from each of the commands in the scripts can be found in a corresponding log file for each section of the `setup.sh` file.  e.g. ./2-database.log.


### Clean up

```
source ~/source/ignite-tour-lp5-s1/0-params.sh
az group delete -n $APP_RG --yes --no-wait
az group delete -n $DB_RG --yes --no-wait

rm ~/source/ignite-tour-lp5-s4/.dbpass
rm -rf ~/source/tailwind-traders
rm -rf ~/source/ignite-tour-lp5-s4/
```

### Profit

### Appendix A: git auth
During the period of time where the code for this demo env lives in private repos, there are two separate sets of git auth that have to be set up a single time:

1. auth for dev.azure.com: create alternative credentials.
This can be performed by going to the dev.azure.com page for the repos (https://dev.azure.com/ignite-tour-lp5/_git/ignite-tour-lp5-s1), clicking on _Clone_, filling out the bottom half of the form and choosing "Save Git Credentials". 
For more information, see https://docs.microsoft.com/azure/devops/repos/git/auth-overview?view=vsts&WT.mc_id=devops-0000-debryen. Your alternative credentials ($USER@microsoft.com and the password you supplied) will be used for the git clone prompts.
1. auth for github.com: create a personal access token by choosing Settings->Developer settings->personal access tokens from the drop down menu under your picture on github.com (when logged in). When you create a person access token,
be sure to choose the "\[ \] repo Full control of private repositories" scope box. Note: you must also be a member of the Azure-Samples Organization for the repo to be accessible.
For more infomation on personal auth tokens see https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/. Your github username and the personal access token you created will be used for the git clone prompts.
