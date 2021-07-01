# Sentia Assessment (Nodejs application Migration to Azure)

Sample Nodejs web application built on Azure WEeb app service (container)

## Assumption Made

- Azure Migrate Assessment to web app is all positive
- Does not need full fledged Orchestration (AKS) or full control (VMs)
- Azure Elastic Service can fulfill the log requirement
- Azure Migrate and Azure Migrate DB tool will be used for migration

## Project Timeline

 - Understanding node.js full stack web app architecture -- 3 hours
 - Planning and designing Architecture in Azure -- 3 hours
 - Deploying Solution in Aure and creating ARM (IaC) -- 4 hours
 - Elastic Search understanding -- 2 hours

## Running

For development, you will need Node.js and a node global package

 - #### Clone this repository  

```bash
    $ git clone https://github.com/Gambit0706/Sentia.git
```

- #### Install dependencies
```bash
    $ cd Application
    $ npm install -g
```
- #### Run Application
```bash
    $ cd Application
    $ npm start
```
- #### Running tests
```bash
    $ cd Tests
    $ npm install -g
    $ npm test
```

## Run Github workflow to deploy resources

The ARM templates can be deployed using Git Workflow.
This requires Azure credentials a Azure Service Principal for deployments. 

Follow the steps to create the Azure credentials (Service Principal) :
    * Run the below [az cli]command 
```bash  

   az ad sp create-for-rbac --name "myApp" --role contributor \
                            --scopes /subscriptions/{subscription-id}/resourceGroups/{resource-group} \
                            --sdk-auth
                            
  # Replace {subscription-id}, {resource-group} with the subscription, resource group details

  # The command should output a JSON object similar to this:

  {
    "clientId": "<GUID>",
    "clientSecret": "<GUID>",
    "subscriptionId": "<GUID>",
    "tenantId": "<GUID>",
    (...)
  }
  
```
  * Store the above JSON as the value of a GitHub secret with a name, this workflow uses 'AZURE_CREDENTIALS' name
  * Now in the workflow file in your branch: `.github/workflows/DeployAssessment.yml` adjust the env variable to meet your need accordingly
  * Some env should be unique globally in public Azure, so choose the name uniquely before initiating Git Action
  * committing main/master branch will trigger the deployment
