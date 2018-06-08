# AWS serverless

Prerequisites

[Install the AWS CLI](http://docs.aws.amazon.com/cli/latest/userguide/installing.html).

[Create an IAM user with admin access](http://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html). The IAM user you associate with the AWS CLI should have admin permissions, including the ability to create IAM roles.

[Configure the AWS CLI to use the admin user](http://docs.aws.amazon.com/cli/latest/reference/configure/).

# Deployment

- Create a new bucket using the following AWS CLI command:
```
aws s3 mb s3://<bucket-name>
```
- Replace the s3-bucket argument with the name of S3 bucket. 
```
aws cloudformation package \
--template-file serverless.cfn.yml \
--output-template-file serverless-xfm.cfn.yml \
--s3-bucket <bucket-name>
```
- Deploy, replace the template-file argument with the full path to the output template file.
```
aws cloudformation deploy \
--template-file <path-to-file/serverless-xfm.cfn.yml> \
--stack-name StartupKitServerless \
--capabilities CAPABILITY_IAM
```

# Testing From the Command Line

In API Gateway console, selecting the StartupKitServerless API, then Stages in the left navigation panel, and finally Stage in the list of stages. The invoke URL should now appear at the top of the right hand panel.
```
curl -X POST -H 'Content-Type: application/json' -d '{"todo_id": "1001", "active": true, "description": "What TODO next?"}' https://<API-URL>/todo/new
```
- To fetch the active TODO items
```
curl https://<API-URL>/todo/active
```



