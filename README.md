# Sentia Assessment (Nodejs application Migration to Azure)

Sample Nodejs web application built on Azure WEeb app service (container)

## Assumption Made

- Azure Migrate Assessment to web app is all positive
- Does not need full fledged Orchestration (AKS) or full control (VMs)
- 
## Installation

For development, you will need Node.js and a node global package

### Node
- #### Node installation on Windows

  Just go on [official Node.js website](https://nodejs.org/) and download the installer.
Also, be sure to have `git` available in your PATH, `npm` might need it (You can find git [here](https://git-scm.com/)).

- #### Node installation on Ubuntu

  You can install nodejs and npm easily with apt install, just run the following commands.

      $ sudo apt install nodejs
      $ sudo apt install npm

- #### Other Operating Systems
  You can find more information about the installation on the [official Node.js website](https://nodejs.org/) and the [official NPM website](https://npmjs.org/).

If the installation was successful, you should be able to run the following command.

    $ node --version
    v8.11.3

    $ npm --version
    6.1.0

If you need to update `npm`, you can make it using `npm`! Cool right? After running the following command, just open again the command line and be happy.

    $ npm install npm -g


### Running

 - #### Clone this repository  

```bash
    $ git clone https://github.com/YOUR_USERNAME/REPOSITORY_NAME.git
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


## Run Github workflow to deploy resourcesA

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
  * Store the above JSON as the value of a GitHub secret with a name, for example 'AZURE_CREDENTIALS'
  * Now in the workflow file in your branch: `.github/workflows/workflow.yml` adjust the variable to meet your need accordingly
  * Web app name should be unique globally, so choose the name uniquely before initiating Git Action