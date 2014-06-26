#HPAC Run Book to deploy, update and delete the running service using CloudFormation orchestration.
======================

Welcome to the HPAC Production Drupal Run Book Document.  This file contains all of the documentation associated with the syntax for creating,updating and deleting the production AWS HA Drupal instances using automated scripts and CloudFormation Stack Templates.

### Cloudformation Template Location

The cloudformation template located here

## Creating the HPAC Drupal HA Instances using CloudFormation and the aws create-stack command

### The following Arguments need to be exported within your environment before executing the deployment script.

```
$> export Label=HPAC-Drupal-Instance
$> export CloudCommand=create-stack
$> export DBPassword=hpacdbpassword
$> export SitePassword=hpacsitepassword
$> export KeyName=HPACDrupalKeyPair

```

###Executing the script:

```
$> ./deploy.sh

```

###Output of the script:

```
$> Performing a create-stack in AWS!
$> Command to execute:
$> -----------------------
$> aws cloudformation create-stack --capabilities CAPABILITY_IAM --stack-name HPAC-Drupal-Instance --disable-rollback --template-body file://template.json --parameters ParameterKey=SitePassword,ParameterValue=hpacsitepassword ParameterKey=DBPassword,ParameterValue=hpacdbpassword ParameterKey=Label,ParameterValue=HPAC-Drupal-Instance ParameterKey=KeyName,ParameterValue=HPACDrupalKeyPair
$> {
$> "StackId": "arn:aws:cloudformation:us-east-1:219880708180:stack/HPAC-Drupal-Instance/6f3b2ae0-fd26-11e3-99fa-500150b34c44"
$> }

```

###AWS Console

Check the progress of the CloudFormation Stack execution at the below url (need to be logged in)

```
https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks?filter=active
```

## Updating the HPAC Drupal HA Instances using CloudFormation and the aws update-stack command

Use:  The update-stack command can be used to recreate HPAC instances that have been destroyed manually within the AWS console.  It will compare the HPAC template against what is running in AWS and re-create any missing infrastructure components.

### The following Arguments need to be exported within your environment before executing the deployment script.

```
$> export Label=HPAC-Drupal-Instance
$> export CloudCommand=update-stack
$> export DBPassword=hpacdbpassword
$> export SitePassword=hpacsitepassword
$> export KeyName=HPACDrupalKeyPair

```

###Executing the script:

```
$> ./deploy.sh

```

###Output of the script:

###NOTE: The below error occurs because of the resilency of the HPAC Template pararmeters that are in inherent in the HPAC CloudFormation Template.  The instances will typically recreate themselves within minutes thus the reason that "No updates are to be performed".  This may differ if for some reason this resilency fails for someunknown reason, and your output may differ.

```
$> Performing an update-stack in AWS!

$> A client error (ValidationError) occurred when calling the UpdateStack operation: No updates are to be performed.

```

###AWS Console

Check the progress of the CloudFormation Stack execution at the below url (need to be logged in)

```
https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks?filter=active
```

## Deleting the HPAC Drupal HA Instances using CloudFormation and the aws delete-stack command

Use:  The delete-stack command can be used to "terminate" ALL HPAC instances. CAUTION: This command when executed "destroys" all Web Server Instances, Databases, and Elastic Load Balancers that were created using the HPAC template.

### The following Arguments need to be exported within your environment before executing the deployment script.

```
$> export Label=HPAC-Drupal-Instance
$> export CloudCommand=delete-stack

```

###Executing the script:

```
$> ./deploy.sh

```

###Output of the script:

```
$> Performing an delete-stack in AWS of the Cloudstack named HPAC-Drupal-Instance!
$> Command to execute:
$> -----------------------
$> aws cloudformation delete-stack --stack-name HPAC-Drupal-Instance
```

###AWS Console

Check the progress of the CloudFormation Stack execution at the below url (need to be logged in)

```
https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks?filter=active
```
