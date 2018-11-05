# Learn how to export & import a Watson Assistant workspace
In this simple tutorial we go through the steps to export and import and Watson Assistant workspace using the Watson Assistant API. 

# Table of Contents
1. [Background](#1-background)
2. [Environment Setup](#2-environment-setup)
3. [Retrieve Workspace ID](#3-retrieve-workspace-id)
4. [Export Watson Assistant Workspace](#4-export-watson-assistant-workspace)
5. [Import Watson Assistant Workspace](#5-import-watson-assistant-workspace)
6. [Conclusion](#6-conclusion)


## 1. Background 
Teams working to build a virtual agent with Watson Assistant will define the agent's domain using intents and entities and structure the agent's ability to converse through a dialog. The aforementioned intents, entities and dialog are the core components of a Watson Assistant workspace and it's this workspace that a development team will look to version and promote as they build and deploy a virtual agent solution. The instructions provided in this simple tutorial can be used to create a duplicate of an existing workspace that can be used for training, development, testing, etc.

The Watson Assistant API makes it easy to both export and import a Watson Assistant workspace. 

## 2. Environment Setup
To export a Watson Assistant workspace from a command prompt or terminal window, we can use curl. Note, it's also possible to export a Watson Assistant workspace from the IBM Cloud user interface, but to script or automate the process you're more likley to use the API. Ensure you have curl installed on the machine where you plan to execute the commands in the steps that follow. 

Obviously you're also required to have a least a single instance of Watson Assistant provisioned on IBM Cloud and an asociated workspace to export and import. 


## 3. Retrieve Workspace ID
Before exporting a particular workspace, we first need the workspace ID that can be obtained from the Watson Assistant UI on IBM Cloud or through the Watson Assistant API. 

To retrieve a workspace ID using the Watson Assistant API, issue the following curl command 
```
curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/assistant/api/v1/workspaces?version=2018-09-20"
```

Replace `{username}` and `{password}` in the command above with the appropriate credentials for your Watson Assistant instance. You might notice that your Watson Assistant instance doesn't use username/password as a means of authentication, but instead uses an Identity and Access Management (IAM) API Key. In this case replace `"{username}":"{password}"` with `"apikey:{apikey}"`  where `{apikey}` is the IAM API Key value for the Watson Assistance service instance. 

The URL used in the command above is for use with a Watson Assistant service instance running in the US South region. Update the URL to the appropriate value for your Watson Assistant instance - this will alter based on region and can be found on the same page as your service credentials from IBM Cloud. 

## 4. Export Watson Assistant Workspace 
Having retrieved the ID for the Watson Assistant workspace, issue the following command to export the workspace to a JSON file
```
curl -u "{username}":"{password}"  "https://gateway.watsonplatform.net/assistant/api/v1/workspaces/<workspace_id>?version=2018-09-20&export=true" > workspace.json
```

Again, alter the command above to use the IAM API Key if appropriate for your service instance. The URL should also reflect the region your Watson Assistant instance is running in. Finally, replace `<workspace_id>` with the value retrieved from step 3 above. 

The command above will export your Watson Assistant workspace in JSON format to a local file called `workspace.json`. Change this file name as needed. Once you've exported your Watson Assistant workspace to file, you're free to version the file with a Source Code Management (SCM) system of your choice using appropriate commands. It's also this JSON file that we'll use to import into Watson Assistant to recreate the workspace. That workspace could reside on the same Watson Assistant service instance or another Watson Assistance service instance running on either the same or different IBM Cloud Region. 

## 5. Import Watson Assistant Workspace 
In this last step, we'll import a Watson Assistant workspace into another instance of Watson Assistant. To import a Watson Assistant workspace issue the following command: 
```
curl -H "Content-Type: application/json" -X POST -u "{username}":"{password}" -d @workspace.json "https://gateway.watsonplatform.net/assistant/api/v1/workspaces?version=2018-09-20"
```

As with steps 3 & 4 before, we'll alter the command above to use an IAM API Key if required and update the URL for our Watson Assistant instance if needed. Remember, we can import the Watson Assistant workspace from the `workspace.json` file to the same Watson Assistant instance or another instance as needed. After importing your Watson Assistant workspace, you may decide to change the workspace name to identify a workspace version or release phase - this workspace name change can be completed from the Watson Assistant UI after import. 

## 6. Conclusion 
Following the steps above we learnt how to export and import a Watson Assistant workspace using the Watson Assistant API. To illustrate the steps involved, we issued commands to the Watson Assistant API using curl. These API calls could also be made via an appliction using the Watson SDK or scripted to run as part of a config or build management tool. 
