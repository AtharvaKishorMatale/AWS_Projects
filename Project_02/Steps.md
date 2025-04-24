# DESCRIPTION:-
In this project,I made a simple API that works without using any servers. I used AWS Lambda to write the code and API Gateway to connect the API to the internet. When someone sends a request to the API, it runs the Lambda function and shows a message. This method is cheap and easy to manage because I don’t have to worry about servers.

# STEPS:-

# Step 1: 
-Create a Lambda Function
-First, I opened the AWS Lambda service from the AWS Console.
-I clicked on Create Function and chose Author from scratch.
-Gave my function a name like ServerlessAPI and picked Python 3.x as the language.
-I let AWS make a new role with the basic permissions.
-Then, I added this simple code in the editor:

# CODE:

import json
def lambda_handler(event, context):
    return {
        "statusCode": 200,
        "body": json.dumps({"message": "Hello from Serverless API!"})
    }

Clicked Deploy to save and update the function.

# Step 2: Set Up API Gateway

-Went to the API Gateway service and created a new REST API.
-I selected the Regional option and created the API.
-Then I made a new resource and named it something like /hello.
-After that, I added a GET method under it.
-For the method type, I picked Lambda Function and typed the name of the Lambda function I created earlier.
-Clicked Save and allowed API Gateway to use my Lambda.

# Step 3: Deploy the API

-I clicked on Actions and then selected Deploy API.
-created a new stage and named it prod.
-After deployment, I got a link (Invoke URL) that looked like this:
-https://xyz.execute-api.region.amazonaws.com/prod/hello

# Step 4: Try the API

-I opened the browser or used this command in the terminal:
-Sh
-curl "invoked_Url"
-It showed this message:

# O/P
{
  "message": "Hello from Serverless API!"
}

