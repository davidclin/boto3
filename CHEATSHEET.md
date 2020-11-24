# Architecture
![Boto3 Architecture](https://github.com/davidclin/boto3/blob/develop/images/boto3_architecture.png)

# What is Botocore?
<pre>
From https://botocore.amazonaws.com/v1/documentation/api/1.10.50/tutorial/index.htm:

"The botocore package provides a low-level interface to Amazon services. It is responsible for:

Providing access to all available services
Providing access to all operations within a service
Marshaling all parameters for a particular operation in the correct format
Signing the request with the correct authentication signature
Receiving the response and returning the data in native Python data structures

botocore does not provide higher-level abstractions on top of these services, operations and responses. 
That is left to the application layer. 
The goal of botocore is to handle all of the low-level details of making requests and getting results from a service.

The botocore package is mainly data-driven. Each service has a JSON description which specifies all of the operations the service supports, all of the parameters the operation accepts, all of the documentation related to the service, information about supported regions and endpoints, etc. Because this data can be updated quickly based on the canonical description of these services, it's much easier to keep botocore current."
</pre>

# What is Boto3?
<pre>
Boto3 is the name of the Python SDK for AWS. It allows you to directly create, update, and delete AWS resources from your Python scripts.

Session  : AWS management console connection
Resource : High level object APIs (easier to use but limited services supported)
Client   : Low  level object APIs (practically all services supported but requires more user handling) 
</pre>

# How to get list of boto3 services using client
<details>
<summary>List of boto3 available service names and resources</summary>

<pre>
CODE
import boto3

# aws management console
session_default_profile = boto3.session.Session(profile_name='default',region_name="us-east-1")

# Get list of available service names
print("-------------------------------")
print("List of available service names")
print("-------------------------------")
result = session_default_profile.get_available_services()
for i in result:
    print(i)

# Get list of available resources
print("-------------------------------")
print("List of available resources:")
print("-------------------------------")
result = session_default_profile.get_available_resources()
for i in result:
    print(i)
    
OUTPUT
-------------------------------
List of available service names
-------------------------------
accessanalyzer
acm
acm-pca
alexaforbusiness
amplify
apigateway
apigatewaymanagementapi
apigatewayv2
appconfig
appflow
application-autoscaling
application-insights
appmesh
appstream
appsync
athena
autoscaling
autoscaling-plans
backup
batch
braket
budgets
ce
chime
cloud9
clouddirectory
cloudformation
cloudfront
cloudhsm
cloudhsmv2
cloudsearch
cloudsearchdomain
cloudtrail
cloudwatch
codeartifact
codebuild
codecommit
codedeploy
codeguru-reviewer
codeguruprofiler
codepipeline
codestar
codestar-connections
codestar-notifications
cognito-identity
cognito-idp
cognito-sync
comprehend
comprehendmedical
compute-optimizer
config
connect
connectparticipant
cur
databrew
dataexchange
datapipeline
datasync
dax
detective
devicefarm
directconnect
discovery
dlm
dms
docdb
ds
dynamodb
dynamodbstreams
ebs
ec2
ec2-instance-connect
ecr
ecs
efs
eks
elastic-inference
elasticache
elasticbeanstalk
elastictranscoder
elb
elbv2
emr
es
events
firehose
fms
forecast
forecastquery
frauddetector
fsx
gamelift
glacier
globalaccelerator
glue
greengrass
groundstation
guardduty
health
honeycode
iam
identitystore
imagebuilder
importexport
inspector
iot
iot-data
iot-jobs-data
iot1click-devices
iot1click-projects
iotanalytics
iotevents
iotevents-data
iotsecuretunneling
iotsitewise
iotthingsgraph
ivs
kafka
kendra
kinesis
kinesis-video-archived-media
kinesis-video-media
kinesis-video-signaling
kinesisanalytics
kinesisanalyticsv2
kinesisvideo
kms
lakeformation
lambda
lex-models
lex-runtime
license-manager
lightsail
logs
machinelearning
macie
macie2
managedblockchain
marketplace-catalog
marketplace-entitlement
marketplacecommerceanalytics
mediaconnect
mediaconvert
medialive
mediapackage
mediapackage-vod
mediastore
mediastore-data
mediatailor
meteringmarketplace
mgh
migrationhub-config
mobile
mq
mturk
neptune
network-firewall
networkmanager
opsworks
opsworkscm
organizations
outposts
personalize
personalize-events
personalize-runtime
pi
pinpoint
pinpoint-email
pinpoint-sms-voice
polly
pricing
qldb
qldb-session
quicksight
ram
rds
rds-data
redshift
redshift-data
rekognition
resource-groups
resourcegroupstaggingapi
robomaker
route53
route53domains
route53resolver
s3
s3control
s3outposts
sagemaker
sagemaker-a2i-runtime
sagemaker-runtime
savingsplans
schemas
sdb
secretsmanager
securityhub
serverlessrepo
service-quotas
servicecatalog
servicecatalog-appregistry
servicediscovery
ses
sesv2
shield
signer
sms
sms-voice
snowball
sns
sqs
ssm
sso
sso-admin
sso-oidc
stepfunctions
storagegateway
sts
support
swf
synthetics
textract
timestream-query
timestream-write
transcribe
transfer
translate
waf
waf-regional
wafv2
workdocs
worklink
workmail
workmailmessageflow
workspaces
xray
-------------------------------
List of available resources:
-------------------------------
cloudformation
cloudwatch
dynamodb
ec2
glacier
iam
opsworks
s3
sns
sqs
</pre>
</details>


# How to print nested dictionaries that contain datetime
<details>
<summary>Using pprint / json</summary>

<pre>
import boto3
import json                                                    # Simple use cases | pip install json
import pprint                                                  # Nested dicts     | pip install pprint
from datetime import datetime                                  # Nested dicts     | pip install datetime
from dateutil.tz import tzutc                                  # Nested dicts     | pip install dateutil

from prettyprinter import cpprint, set_default_style           # Nested dicts     | pip install prettyprinter
set_default_style('light')

session = boto3.session.Session(profile_name='default')

iam_console = session.client(service_name='iam')
print(iam_console.list_users())

result = iam_console.list_users()  # where result is a nested dictionary

# For nested dictionaries with datetime
pprint.pprint(result, width=1)

# Using prettyprint
cpprint(result)

# For simple dictionaries
json.dumps(result, indent=1)


</pre>
</details>

# Resources
[Python, Boto3, and AWS S3: Demystified](https://realpython.com/python-boto3-aws-s3)
