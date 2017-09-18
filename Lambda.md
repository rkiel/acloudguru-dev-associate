# Lambda - [back](README.md)

#### History

* IAAS -- Infrastructure As A Service (EC2)
* PAAS -- Platform As A Service (Elastic Beanstalk)
* Containers -- (Docker)
* Serverless -- (Lambda)

#### AWS Lambda - 2015

* A compute service
* Provisions & manages servers
* No worries about OS, patches, scaling
    1. event-driven -- run code in response to events (i.e. changes in S3 bucket or DynamoDB)
    1. http-driven -- using API Gateway or AWS SDK

#### Trigger

Event sources that will invoke your function

* API Gateway
* AWS IoT
* Alexa
* CloudFront
* CloudWatch
* CodeCommit
* Cognito
* DynamoDB
* Kinesis
* S3
* SNS

#### API Gateway

* each request sent invokes a separate Lambda function
* infinite horizontal scaling

### Languages

* Node.js
* Java
* Python
* C#

#### Pricing

* Number of requests
    * fist 1 million requests are free; $0.20 per million requests
* Duration
    * total run time rounded to nearest 100ms
    * amount of memory allocated
    * maximum run time of 5 minutes

#### Exam tips

* Lambda scales out (not up) automatically
* Lambda functions are independent; 1 event == 1 function
* Lambda is serverless
* Know what services are serverless!
    * S3
    * API Gateway
    * Lambda
    * DynamoDB
    * etc
* Lambda functions can trigger other Lambda functions; 1 event == X functions
* Architectures get extremely complicated; AWS X-ray allows you to debug what is happening
* Lambda allows you to do things globally (i.e. backup S3 bucket to another S3 bucket)
* Know your triggers
