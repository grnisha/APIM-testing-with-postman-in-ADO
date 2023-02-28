# APIM testing - configure Postman API tests in Azure DevOps 

This example is exporting an already existing API from Azure APIM into postman and configuring Postman API tests in Azure DevOps. For this example I am using demo conference API, which is configured in my APIM instance. 

**Steps**

Export the api from APIM and select postman. You can choose postman for Web or Windows. 
![image](https://user-images.githubusercontent.com/11030157/221816088-01e9c80c-d76b-480f-bc37-5dcf34ec4b08.png)

 ![image](https://user-images.githubusercontent.com/11030157/221816111-8df3d50c-271b-4310-a52c-cbe3ab24747f.png)
 

This will prompt a dialogue in postman to select a workspace. Once you have selected the workspace, import the api into postman. There is also an option to create collection at the same time and some advanced options

 ![image](https://user-images.githubusercontent.com/11030157/221816180-0a1d8753-96c1-4b01-a12a-ffd3c5885ffb.png)


Now that the API is exported to postman, configure any pre-request steps, variables & tests in postman. In this example, GetSessions endpoint uses a pre-request step to retrieve jwt-token. 

 ![image](https://user-images.githubusercontent.com/11030157/221816275-9bd74d87-0a2e-40b2-9ecf-3b8d593345ef.png)


There are several variables configured in this example as shown below. 

![image](https://user-images.githubusercontent.com/11030157/221816332-8ead5b11-f998-49b3-ad11-0e8c169edc2b.png)

 
The test configured in this example is checking if the API response status is 200. Additional tests can be easily added here , e.g. – tests to check response content, reponse time etc.
 
 ![image](https://user-images.githubusercontent.com/11030157/221816363-c42dce0c-4106-4900-acab-4cda78b6fff2.png)


After configuration is completed, execute the tests to check if everything is working as expected. 

 ![image](https://user-images.githubusercontent.com/11030157/221816417-5cc4b758-c038-4097-baf7-487f97296194.png)


Once everything is working as expected, click on the collection and export it. From the dialogue, select Collection 2.1 and save the json file.

 ![image](https://user-images.githubusercontent.com/11030157/221816459-39d6d853-5a28-4093-8bdf-4371d76f1703.png)


The exported json file also contains the variables we have configured originally (baseUrl, apiKey etc). I have updated values of these variables with place holders (##apiKey##, ##baseUrl## and created a variable group in ADO ‘DemoConfAPIGroup’ to define the values of these variables. You can link this variable group to a Key Vault to securely save sensitive data. The placeholders in json file will be later replaced with required values from variable group during pipeline execution.
 
 ![image](https://user-images.githubusercontent.com/11030157/221816533-01e5481c-b034-425d-b9c7-e67ca4abb091.png)

Now we have the exported and updated json file, let’s move on to creating DevOps pipeline. To run this collection in DevOps pipeline, we need to use newman CLI tool from postman. We can install this tool using npm command (npm install -g newman). To run the tests, we can use the command newman run DemoConfApi.json. The yaml definition for devops pipeline is in azure-pipelines.yml.

The newman run command comes with a few more parameters, which helps to publish the test results. Please note that the -x flag will ignore the exit code and continue executing build steps in the pipeline. If you want to stop the pipeline execution on tests failure, remove this flag. 

Here are the test results after running pipeline:

 ![image](https://user-images.githubusercontent.com/11030157/221816590-cea66442-72b4-4640-9381-c081cdf89314.png)

