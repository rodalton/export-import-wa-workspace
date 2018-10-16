# watson-assistant-workspace

## Introduction 
Teams working to build a virtual agent with Watson Assistant will define the agent's domain using intents and entities and structure the agent's ability to converse through a dialog. The aforementioned intents, entities and dialog are the core components of a Watson Assistant workspace and it's this workspace that a development team will look to version and promote as they build and deploy a virtual agent solution. 

The Watson Assistant API makes it easy to to both export and import a Watson Assistant workspace. 

To export a Watson Assistant workspace from a command prompt or terminal window, we can use curl. Before exporting a particular workspace, we first need the workspace ID that can be obtained from the Watson Assistant UI on IBM Cloud or through the Watson Assistant API. 

## Retrieve Workspace ID
To retrieve a workspace ID using the Watson Assistant API, issue the following curl command 
`curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/assistant/api/v1/workspaces?version=2018-09-20"`

Replace `{username}` and `{password}` in the command above with the appropriate credentials for your Watson Assistant instance. You might notice that your Watson Assistant instance doesn't use username/password as a means of authentication, but instead uses an Identity and Access Management (IAM) API Key. In this case replace `"{username}":"{password}"` with `"apikey:{apikey}"`  where {apikey} is the IAM API Key value for the Watson Assistance service instance. 

The URL used in the command above is for use with a Watson Assistant service instance running in the US South region. Update the URL to the appropriate value for your Watson Assistant instance - this will alter based on region and can be found on the same page as your service credentials from IBM Cloud. 

## Export Watson Assistant Workspace 
Having retrieved the ID for the Watson Assistant workspace, issue the following command to export the workspace to a JSON file 
`curl -u "{username}":"{password}"  "https://gateway.watsonplatform.net/assistant/api/v1/workspaces/<workspace_id>?version=2018-09-20&export=true" > workspace.json`

Again, alter the command above to use the IAM API Key if appropriate for your service instance. The URL should also reflect the region your Watson Assistant instance is running in. 

The command above will export your Watson Assistant workspace in JSON format to a local file called `workspace.json`. Change this file name as needed. 
