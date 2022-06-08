# Instructions on how to set up the IAM roles and permissions


First, we need to give our MWAA instance permissions to be able to run SagMaker tasks. 
Go to the IAM Console - Roles (https://console.aws.amazon.com/iam/home?#/roles)

* Search for the Airflow Instance role, which looks similar to AmazonMWAA-airflow-xxxx-instance-xxxx
* First Edit the JSON of the attached policy and add

```
{
"Effect": "Allow",
"Action": "iam:GetRole",
"Resource": "*"
}
```

* Then attach the following permissions to the Airflow Instance role
* *AmazonS3FullAccess*
* *AmazonSageMakerFullAccess*

Next, we will create a SageMaker service role to be used in the ML pipeline module. 

* Go to the IAM Console - Roles (https://console.aws.amazon.com/iam/home?#/roles)
* Choose *Create role*
* For role type, choose AWS Service, find and choose *SageMaker*, and choose *Next: Permissions*
* On the Attach permissions policy page, choose (if not already selected)
* AWS managed policy *AmazonSageMakerFullAccess*
* AWS managed policy *AmazonS3FullAccess* for access to Amazon S3 resources
* Then choose Next: Tags and then Next: Review.
* For Role name, enter AirflowSageMakerExecutionRole and Choose *Create Role*

