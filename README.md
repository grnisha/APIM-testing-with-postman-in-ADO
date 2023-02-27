# APIM tesing - configure postman / newman API tests in Azure DevOps 

Step 1 - Export API From APIM to Postman
       <img width="667" alt="image" src="https://user-images.githubusercontent.com/11030157/221599631-d7a021a3-7752-454f-89b4-47c86ee2f407.png">

Step 2 - Configure any pre-request steps, variables & tests in postman. In this example, GetSessions endpoint uses a pre-request script to retrive jwt-token.

<img width="406" alt="image" src="https://user-images.githubusercontent.com/11030157/221600903-db891c2c-66fa-459b-b367-3cac072dfe0d.png">

Configure variables -->

<img width="443" alt="image" src="https://user-images.githubusercontent.com/11030157/221602459-e8089857-b3d3-42d0-b858-bfbc9f1bc370.png">

Tests configured for this sample is a simple one to check if status is 200.
 
<img width="537" alt="image" src="https://user-images.githubusercontent.com/11030157/221600688-280eaeb4-fc5f-4970-833f-584305259cef.png">

step 3 - Export the postman collection and add it to the repo

step 4 - Remove all sensitive infor deom the postman collection , for example api-key, access-token etc and add these to a variable group. This sample uses a variable group 'DemoConfAPIGroup'
<img width="293" alt="image" src="https://user-images.githubusercontent.com/11030157/221603226-36824da0-3bed-4b51-8296-28273260b639.png">

step 5 - Set up pipeline.

