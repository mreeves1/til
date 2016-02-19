# Microservices Architecture
for Web Applications using AWS Lambda and more
given on 2015-02-19 at AWS Pop-up Loft SF

Author: Eugene Israti, Technology Partner
AWS Certified Solutions Architect
email: eugene@mitocgroup.com
web: www.mitocgroup.com

Goal: never have your website go down

Web applications challenges:
* impact of ddos/dos attack - 60% degradations, 27% outage
* traffic can be very spiky due to viral content, ddos, etc.


## Web app hosting on AWS:

* Reference Architecture - autoscaling 3 tier (web/app/replicated data) groups spread across multiple AZs
  * Scales in minutes - huge challenge for breakign news, viral content & attacks
  * Reduced operational complexity - requires devops
  * Flexible choice of tech - requires devs with rick skillset
  * Cost effective

* Serverless Architecture - does not mean there are no servers. It means developers no longer have to think 
  that much about them. Compute services used as resources without wrrying about scaling
  * Static Assets
    * Same as in reference - docs, images, css, html, etc.
  * Dynamic Functionality
    * Use JS framework (e.g. Angular)
    * SEO friendly
  * Completely Serviceless
    * Pre-scaled
    * Low-cost
    * Low-maintenance
  * App-tier - docker containers
    * deploys in seconds
  * Accelerated Backend
    * Write node.js functions and load into Lambda
    * Power up lambda with RESTful endpoints on API Gateway
    * cache, throttle, meter, versio, etc.
  * DB Tier
    * care about reads/writes per second
    * Suggest dynamo db
      * Schemaless
      * Scale only reads and writes
      * Can be expensive so good idea to implement a queue which means eventual consistency but 50% of cost
    * Can also use RDS Aurora
      * Releational
      * MySQL like approach but 5x better

* Demo: Setup Serverless AWS
  * Security - IAM
    Allow lambda to hit dynamodb
  * Front-end
    * Create s3 bucket
    * Add policy that allows read-only anon access
    * When you setup cloudfront choose the s3 endpoint instead of one from the auto-populating list
  * Back-end
    * Upload lambda code and set timeout
    * Need to use API Gateway because of CORS - maps routes to lambda functions and HTTP verb
    * Some kind of wacky enable CORS button
  * Database
  * Code

[Deployed serverless app](https://todo.deep.mg) inspired from open source http://www.todomvc.com

Follow along at: https://github.com/MitocGroup/deep-microservices-todo-app

## AWS Lambda
Event driven compute service for dynamic applications. Now supports VPC.  
[More Info](https://aws.amazon.com/lambda/?hp=tile)

## Amazon API Gateway
Allows you to map endpoints to for instance lambda functions.  
[More Info](https://aws.amazon.com/api-gateway/)

## Microservices

### Tips and tricks?
* Setup alarms for all 4 lambda metrics
* Avoid S3 throttling by integrating s3 -> sns -> lambda
* beware infinite loops

### Benefits
* Very shortlived and thus hard to hack
* Much simpler
* Development cycles are decoupled and shorter?

Need to look into DRY as each microservice is equivalent to one RESTful endpoint. Code reuse between lambdas?
Lambda is stateless so... how does that work? Perhaps with [Cognito](https://aws.amazon.com/cognito/?hp=tile)?
