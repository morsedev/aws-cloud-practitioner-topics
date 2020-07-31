# Topics required for AWS Cloud Practitioner Exam

This list is a summary of Andrew's excellent video at freeCodeCamp.org available at https://www.youtube.com/watch?v=3hLmDS179YE

## General

- Regions
	- e.g. us-east (largest)
- Availability Zones 
	- Datacenter owned and run by AWS
	- Each region has at least 2 AZ
	- AZs are identified with a number at the end, e.g. us-east1
	- Ping below 1ms
- Edge Zones
	- Datacenter owned by trusted partner
	- Has direct connection to AWS network
	- Serve requests for CloudFront and Route53
	- S3 buckets and API gateways also use Edge network
	- Benefit: Low latency as close to user's location

## AWS GovCloud
- Host sensitive, controlled, unclassified Information
- Datacenters only operated by US citizens on US soil
- Only accessible to root account holders (need screening process) and US entities
- Used to comply with certain US regulations, e.g. FedRamp, Department of Defense etc.

## Services overview

- EC2
	- Elastic Compute
- AMI (Amazon Machine Image)
	- Snapshot of VM
- Auto Scaling Groups
	- Make sure that e.g. at least 1 server of a group is running
	- Scale capacity up and down when more traffic happens
- Elastic Load Balancer
- S3 Buckets
- Cloudfront
	- CDN
	- Deliver files via shortest route
	- Copies files to multiple edge locations
- RDS
	- Relational Database Service
- AWS Lambda
	- Serverless Functions
- CloudWatch
	- Logging

## EC2 Pricing

- On Demand
	- No long term commitment
	- Only paying by hour
	- Good for short-term, unpredictable, spikey
- RI (Reserved Instances)
	- Good for long term
	- Apps which are predictable and steady
	- Pricing based on
		- Term
		- Class Offering
		- Payment Option
			- Standard
				- Up 75% cheaper than on-demand
				- Cannot change RI attributes (e.g. instance type)
			- Convertible
				- 54% cheaper than on-demand
				- Allows changing RI attributes if greater or equal in value
			- Scheduled
				- Reserve instances for specific timesframes
				- e.g. once a week for a few hours
	- Available 1 or 3 year contract
	- Can resell unused instances via marketplace
	- The longer the cheaper
	- Payment options
		- All Upfront (cheapest)
		- Partial upfront
		- No upfront
- Spot Instances
	- Using AWS idle servers
	- Discounted 90%
	- Is terminated if needed by reserved instance customer
		- If terminated by AWS -> Not charged $$$ for partial hour
		- If terminated by me -> Charged per hour $$$
- Dedicated instance
	- Most expensive
	- When software needs to run on own hardware (isolated)
	- No sharing with other customers (no multi tenancy)
	- On-demand or reserved (70% off)
- Free services
	- IAM
	- Amazon VPC
	- _Auto scaling_
	- _CloudFormation_
	- _Elastic Beanstalk_
	- _Opsworks_
	- _Amplify_
	- _AppSync_
	- _CodeStar_
	- Organizations & Consolidated Billing
	- AWS Cost Explorer

*Items in italic* = Free but might provision other AWS services which cost money

## Support Plans
- Basic
	- For free
	- Support only for Billing and Account
	- 7 Trusted advisor checks
- Developer
	- $20 / months
	- Support via email (response takes up to 24h)
	- No third party support
	- General guidance < 24h
	- System impaired < 12h
	- 7 Trusted advisor checks
- Business
	- $100 / months
	- Support via email (response takes up to 24h)
	- 24/7 tech support via chat or phone
	- General guidance < 24h
	- System impaired (gestört) < 12h
	- Production system impaired < 4h
	- Production system down < 1h	
	- All trusted advisor checks
- Enterprise
	- Same as business above plus:
		- Costs $15,000 / month
		- Business critical system down < 15min
		- Personal concierge
		- TAM
		- All trusted advisor checks

## AWS Marketplace
- Free or paid offerings
- Offerings
  - Operating systems
  - Security
  - Networking
  - Business Intelligence
  - Databases
  - Dev Ops
  - Storage
  - Machine Learning
- Can be offered as:
  - Amazon Machine Images (AMI)
  - AWS CloudFormation templates
  - SaaS
  - Web ACL
  - AWS WAF rules
- Trusted Advisors
  - Are automated Checks:
    - Cost optimization
      - Idle Load Balancers
      - Unassociated Elastic IP addresses
    - Performance
      - High utilization EC2 instances
    - Security
      - MFA on root account
      - IAM Access Key Rotation

## Consolidated Billing
- One master account to pay from when having multiple member accounts
- Use Cost Explorer
- Volume Discounts
	- The more you use, the more you save

## Cost Explorer
- Visualize and mange costs
- Create reports
- Forecasting
- Monthly or daily views
- Filter and grouping features

## AWS Budgets
- 3 Types:
	- Usage (hours)
	- Costs ($)
	- Reservations
- Can be tracked monthly, quarterly or yearly levels
- Setup alerts for budgets (e.g. when exceeded)
- Reserveration alerts are supported for EC2, RDS, Redshift, ElastiCache
- Budget can be paid upfront or fixed price
- 1st two budgets are free
- Each budget costs $0.02 / day
- 20,000 budgets limit
- Managed via Budgets Dashboard
- Notification via email or chatbot possible

## TCO Calculator
- TCO = Total Cost of Ownership
- Estimate how much to save when moving from on-prem to AWS
- Creates reports that can be used in presentations (3-year summary)

## AWS Landing Zone
- Helps enterprises to setup a secure AWS multi-account
- Creates a baseline architecture
- Use AVM (Account Vending Machine)
- Creates new accounts based on templates
- Uses SSO for managing accounts
- Example: Separation in 3 different account types:
	- Shared Services Account
	- Log Archive Account
	- Security Account

## Ressource Groups & Tagging
- Tags: Word to organizes ressources
- Ressource Group: Collection of ressources which share the same tags

## AWS Quick Starts
- Templates for popular stacks
- Created by AWS and partners
- Consists of 3 things:
	- Reference architecture for deployment
	- AWS CloudFormation templates (automate and configures the deployment)
	- A deployment guide with explanations

## AWS cost and usage report
- Analyse costs
- Download spreadsheet
- Puts data into S3 bucket
- Use Athena to turn data into a database
- Use QuickSight to visualize data as graphs

## Organizations and Account
- When first sign up that user becomes root/master account
- Can create different organisational Units
- Then create multiple child accounts into each unit
- Useful to separate departments with different permissions/rights, e.g. "Developers"
- Service Control Policies allow to set permissions for each organisational unit, e.g. "Only EC2"

## AWS Networking
- Regions
- .. have VPC Virtual Private Cloud (isolated part of AWS for own network)
- .. have Availability Zone
- .. have Public/Private Subnets
	- Public subnet e.g. for EC2
	- Private subnet for DB
- Internet Gateways allow access e.g. to EC2 instance
- Route Tables defined where traffic should be routed to
- NACL -> Acts as firewall on subnet level
- Security Group -> Acts as firewall on instance level

## Database Services
- DynamoDB
	- NoSQL key/value DB (like Cassandra)
- DocumentDB
	- NoSQL Document DB (MongoDB compatible!)
- RDS
	- Relational DB Service
	- Supports multiple engines like
		- MySQL
		- Postgres
		- MariaDB
		- Oracle
		- Microsoft SQL
		- Aurora
			- Fully managed
			- 5x faster than MySQL
			- 3x faster than PSQL
			- Aurora Serverless: Only runs when you need it (like Lambda)
- Neptune
	- Graph DB (Managed)
- RedShift
	- Columnar DB
	- Petabyte warehouse
ElastiCache
	- Redis or
	- Memcached

## Provisioning
- .. is the allocation or creation of resources and services to a customer
- Elastic Beanstalk
	- Just upload app without having to worry about infrastructure
	- Like heroku
	- Supports .NET, PHP, Node, Python, Ruby, Go, Docker
- OpsWorks
	- Configuration Management Services
	- Provides managed instances of Chef and Puppet
- CloudFormation
	- Infrastructure as code
	- Upload JSON or YAML
	- Configures and sets up all services required
- AWS QuickStart
	- .. are pre-made CloudFormation templates/packages
- AWS Marketplace
	- Catalog of software listings from 3rd parties
	- Can be used to buy, test and deploy software
	- E.g. provide out of the box wordpress installation

## Computing
- EC2
	- Elastic Compute Cloud
	- Configurable server
- ECS
	- Elastic Container Service
	- Docker as a service
- Fargate
	- Also for microservice
	- Don't think about infrasture
	- Paying for cpu usage, not per instance
- EKS
	- Kubernetes as a service
- Lambda
	- Serverless functions
- Elastic Beanstalk
	- Sets up everything (EC2, S3, SNS, CloudWatch, load balancers etc)
	- More for developers, not production
	- Creates EC2 instances under the hood
- AWS Batch
	- Organises batch computing workloads across AWS services
	- Launches e.g. EC2 instances or Spot Instances to save money

## Storage
- S3
	- Simple Storage Service
	- Object storage
	- Unlimited space
- S3 Glacier
	- Low cost
	- Takes time to upload
	- Long term backup
- Storage Gateway
	- Hybrid Cloud Storage (on-prem to cloud)
	- With local caching
- EBS
	- Elastic Block Storage
	- Hard drive in the cloud
	- Attach to EC2 instances
	- Cheap solution
	- Attachable to only 1 EC2 instance
- EFS
	- Elastic File Storage
	- Mountable to multiple EC2 instances at the same time
- Snowball
	- Computer shipped to upload data to
	- Faster than transfer over internet
	- Snowball Edge
		- Better version of snowball (faster)
	- Snowmobile
		- Container on a truck, 100 PB
		- Data center on wheels

## Business Centric Services
- Amazon Connects
	- Call center service
	- Store recordings on S3
- Workspaces
	- Virtual Remote Desktop
	- Windows or Linux
	- Bring own license
- WorkDocs
	- Content collaboration service
	- Like sharepoint
- Chime
	- Online meetings
	- Video conferencing
	- Like Slack, Skype
- WorkMail
	- Business Email
- Pinpoint
	- For marketing
	- Send targeted email
	- SMS
	- Push notifications
	- Voice messages
- SES
	- Simple Email Service
	- Send marketing mails etc
	- Difference to Pinpoint: Send emails directly from application
	- For developers
	- For marketing because can to HTML mails
	- ... while SNS can do only plain text
- QuickSight
	- Business Intelligence service
	- Connect multiple datasources
	- Creates graphs for visualisation

## Enterprise Integration (Bring together on-prem and Cloud)
- Direct connect
	- Fiber optic cable to connect on-prem and AWS
- VPN
	- Establish secure connection to AWS
	- Site-to-Site VPN: Connect on-prem to AWS
	- Client VON :Connect client (laptop) to AWS
- Storage Gateway
	- Hybrid storage services
	- Allows on-prem apps to use AWS cloud storage
	- Extend on-prem hard drives to AWS
	- E.g. for backups
- Active Directory
	- AD in AWS (managed)

## Logging services
- CloudTrail
	- Logs all API calls between AWS Services
	- E.g. who created this bucket?
	- Also detect malicious activity
- CloudWatch
	- Collection of multiple services like
		- CloudWatch logs
			- Performance log like CPU utilization
			- Application logs like Node, Nginx
			- Labda logs
		- CloudWatch Metrics
			- Can take data from CloudWatch Logs and turn it into a graph
		- CloudWatch Events
			- Trigger event based on condition
			- E.g. take snapshop of server every hour
		- CloudWatch Alarms
			- Triggers notification based on metrics (e.g. via email)
		- CloudWatch Dashboard
			- Create visualization graphs based on metrics

## Initialism
Need to know as often used in exam

- IAM: Identify and Access Management
- S3: Simple Storage Service
- SWF: Simple Workflow Service
- SNS: Simple Notification Service
- SQS: Simple Queue Service
- SES Simple Email Service
- SSM: Simple Email Service
- SES: Simple Email Service
- SSM: Simple Systems Manager
- RDS: Relation Database Service
- VPC: Virtual Private Cloud
- VPN: Virtual Private Network
- CFN: CloudFormation
- WAF: Web Application Firewall
- MQ: Amazon ActiveMQ
- ASG: Auto Scaling Groups
- TAM: Technical Account Manager
- ELB: Elastic Load Balancer
- ALB: Application Load Balancer
- NLB: Network load Balancer
- EC2: Elastic Cloud Compute
- ECS: Elastic Container Service
- ECR: Elastic Container Repository
- EBS: Elastic Block Storage
- EFS: Elastic MapReduce
- EB: Elastic beanstalk
- ES: Elastic Search
- EKS: Elastic Kubernetes Service
- MKS: Managed Kafka Service
- IoT: Internet of Things
- RI: Reserved Instances

## Shared Responsibility Model
- Customers are responsible for security in the cloud
	- Data
	- Configuration
- AWS is responsible for security of the cloud, e.g.
	- Hardware
	- Managed services
	- Global infrastructure

## AWS Compliance Programs
- Internal policies and procedures of a company to comply with laws and regulations
- E.g. when handling credit card information you need to be PCI DSS compliant

