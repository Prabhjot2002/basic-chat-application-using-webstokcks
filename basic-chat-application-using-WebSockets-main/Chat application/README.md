
# Simple Websockets Chat App

**Update**: *Check out the enhanced version of this Websocket chat application using AWS CDK [here](https://github.com/aws-samples/websocket-chat-application).*

This repository contains the source code and template for a simple Websockets chat application. It consists of three functions located in separate directories, along with a SAM template that connects them to a DynamoDB table and sets up the necessary permissions:

```
.
??? README.md                   <-- This instructions file
??? onconnect                   <-- Source code for onconnect
??? ondisconnect                <-- Source code for ondisconnect
??? sendmessage                 <-- Source code for sendmessage
??? template.yaml               <-- SAM template for Lambda Functions and DDB
```

## Deployment Options

You have two methods to deploy this application:

### Option 1: Serverless Application Repository

The quickest way is to use AWS's Serverless Application Repository. This allows you to deploy the components directly into your account without additional tools. You'll have the chance to review the deployment before it proceeds. For more details, visit the [application details page](https://serverlessrepo.aws.amazon.com/applications/arn:aws:serverlessrepo:us-east-1:729047367331:applications~simple-websockets-chat-app).

### Option 2: AWS CLI Commands

Alternatively, you can install the [AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html) and use it to package, deploy, and describe your application. The following commands will be necessary:

```bash
sam deploy --guided

aws cloudformation describe-stacks \
    --stack-name simple-websocket-chat-app --query 'Stacks[].Outputs'
```

**Note:** Ensure to back up or modify your `.gitignore` file to include `samconfig.toml`.

## Testing the Chat API

To test the WebSocket API, you can use [wscat](https://github.com/websockets/wscat), a command-line tool for WebSocket testing.

1. [Install NPM](https://www.npmjs.com/get-npm).
2. Install wscat:

```bash
$ npm install -g wscat
```

3. Connect to your published API endpoint using the following command:

```bash
$ wscat -c wss://{YOUR-API-ID}.execute-api.{YOUR-REGION}.amazonaws.com/{STAGE}
```

4. To test the sendMessage function, send a JSON message like the example below. The Lambda function will echo it back using the callback URL:

```bash
$ wscat -c wss://{YOUR-API-ID}.execute-api.{YOUR-REGION}.amazonaws.com/prod
connected (press CTRL+C to quit)
> {"action":"sendmessage", "data":"hello world"}
< hello world
```

## License Summary

This sample code is provided under a modified MIT license. Please refer to the LICENSE file for more information.

---

Please note that I've slightly modified the text for clarity and formatting. Feel free to adjust it further to better suit your needs.