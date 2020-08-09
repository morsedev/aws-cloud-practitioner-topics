# Topics Required for AWS Cloud Practitioner Exam

This list is a summary of Andrew Brown's excellent video from freeCodeCamp.org available at https://www.youtube.com/watch?v=3hLmDS179YE

## General

- Regions
	- e.g. us-east (largest)
- Availability Zones 
	- Full datacenter owned and run by AWS
	- Hosts addplications, databases, websites, file storage etc...
	- Each region has at least 2 AZ
	- AZs are identified with a number at the end, e.g. us-east1
	- Ping below 1ms
- Edge Zones
	- Smaller datacenter owned by trusted partner
	- Has direct connection to AWS network
	- Serve requests for CloudFront (CDN) and Route53 (DNS)
	- Mostly used for caching static content
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
	- $20 / month
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
	- Data Warehouse Service
	- Columnar DB
	- Petabyte warehouse
ElastiCache
	- Redis or Memcached

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
- S3 Standard
	- Simple Storage Service
	- Object storage
	- Unlimited space
- S3 Standard IA (Infrequent Access)
	- For data which is accessed not often
	- But when accessed needs rapid access
	- Low cost, high performance
	- Good fir long term storage and backups
- S3 OneZone IA
	- Like S3 Standard IA (Data not often needed but with rapid access)
	- Lower availability and resilience compared to S3 Standard IA
	- Stores in only one AZ (other S3 types store in minimum of 3 AZ)
	- 20% cheaper than S3 Standard IA
	- Good for secondary backups
- S3 Glacier
	- For archiving data (Long term backup)
	- Low cost
	- Takes time to upload
	- Stores in multiple AZ for redundancy
- S3 Intelligent Tiering
	- Uses 2 storage types
	- One for quick acceess, one for low cost
	- Automatically moves data from one to the other
	- Costs additional monitoring and automation fee
	- Good for unknown access patterns
- S3 Transfer Acceleration
	- Faster file upload via Edge Locations
	- Edge Locations have optimized connection to AWS network
	- Good if uploaders are spread all sround the world
	- Also useful if own upload speed is not maxed out
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

## AWS Artifact
- No cost, self-service portal
- Creates a report that proves if AWS meets certain compliance programs
- Downloadable as PDF

## Amazon Inspector
- Runs a security benchmark against EC2 instances
- Checks is EC2 instance is secure
- Network and host assesments possible
- Popular benchmark is CIS which has 699 checks

## AWS WAF
- WAF = Web Application Firewall
- Protects agains common web exploits
- Write own rules to allow or deny traffic
- Possible to use ruleset from a trusted AWS Partner from WAF Rules Marketplace
- WAF can be attached to CloudFront of Application Load Balancer
- Protects against OWASP Top 10 most dangerous attacks:
	- Injection
	- Broken Authentication
	- Sensitive data exposure
	- XML External Entities
	- Broken Access Control
	- Security Misconfigurations
	- Cross Site Scripting
	- Insecure Deserialisation
	- Using Components with known vulnerabilities
	- Insufficient loggin and monitoring

## AWS Shield
- Managed DDoS protection
- No additional charge
- Automatic protection
- AWS Shield standard protects when these are used:
	- Route53
	- CloudFront
- Protects against layer 3, 4 and 7 attacks
- AWS Shield Advanced
	- Costs $3,000 / year
	- Additional protection against larger and more sophisticated attacks
	- Visibility into attack
	- 24/7 support from DDoS experts
	- Available on:
		- Route53
		- CloudFront
		- Elastic Load Balancing
		- Global Accelerator
		- Elastic IP

## Penetration Testing
- Simulate cyber attack to evaluate security
- Is allowed on the following services:
	- ES2 Instances, Nat Gateways, ELB
	- RDS
	- CloudFront
	- Aurora
	- API Gateways
	- AWS Lambda
	- Lightsail resources
	- Elastic Beanstalk environments
- Prohibited Activities
	- DNS Zone walking via Amazon Route 53 Hosted Zones
	- DoS and DDoS
	- Port flooding
	- Protocol flooding
	- Request flooding
- For other simulated attacks AWS approval is required

## Guard Duty
- Threat Detection Service, aka IDS/IPS
	- IDS = Intrusion Detection System
	- IPS = Intrucion Protection System
- Continuously monitors for suspicious activity
- Uses machine learning to analyse AWS logs from:
	- CloudTrail
	- VPC Flow
	- DNS logs
- Will send an alert if something is found
- Automated inciden response via CloudWatch Events (or other 3rd parties) possible

## Key management Services (KMS)
- Managed service to create and control encryption keys
- .. is a multi-tenant HSM
	- HSM = Hardware Security Module
	- .. is a piece of hardware of manage encryption keys
	- Multi-tenant because shared with other customers in isolation
- Can be used in many AWS service by just enabling through clicking a checkbox
- KMS uses Envelope Encryption
	- Protects the key which encrypts data
	- Master key encrypts data key which encrypts data

## Amazon Macie
- Managed service which monitors S3 data access
- Checks for anomalies and generates alerts
- Can detect unauthorised access or data leaks
- Can identify most at-risk users
- Has the following alerts:
	- Anonymised access
	- Config compliance
	- Credential loss
	- Data compliance
	- File hosting
	- Identity Enumeration
	- Information loss
	- Location Anomaly
	- Open Permissions
	- Privilege Escalation
	- Ransomware
	- Service Disruption
	- Suspicious Access

## Security Groups vs. NACL
- Both are firewalls
- Security Groups are at instance level
	- All traffic is denied by default
	- User can create allow rules
	- Allow an EC2 instance access port 22 for SSH
- NACLs are on subnet level
	- NACL = Network Access Control List
	- Can create allow or deny rules
	- Example: Block a specific IP adress

## AWS VPN
- Allows tunnel from network/device to AWS global network
- AWS Site-to-Site VPN allows network (e.g. entire office) to connect to VPC
- AWS Client VPN allows access for single users

## Services not to be confused
These ones all start with the word Cloud:
- CloudFormation (Set up infrastructure via yaml or json)
- CloudTrail (Logs all api calls between AWS Services)
- CloudFront (CDN)
- CloudWatch (Collection of logging service with Events, Alarms and Dashboard)
- CloudSearch (Search engine service, e.g. for adding a search bar to online shop website)

These end with the word Connect:
- Direct Connect (Direct fiber optics cable from data center to AWS)
- Amazon Connect (Call center service with toll free number and automated phone systems)
- Media Connect (Converts video to other codecs / video formats)

 ## Elastic Transcoder vs. Media Convert
 Both services transcode video. Differences are:
 - Elastic Transcoder
 	- The old way
 	- Transcodes videos to streaming formats
 - AWS Elemental MediaConvert
 	- The new way
 	- Transcode videos to streaming formats
 	- Additional features like:
 		- Overlay images
 		- Insert videos clips
 		- Extract caption
 		- Robust UI

## SNS vs SQS
- SNS
	- Simple Notifications Service
	- Pass along messages, e.g. PubSub
	- Send notifications to subscriber e.g. via http, email, SQS or SMS
	- Used for sending plain text emails triggered via other AWS services
		- Example: Billing alarms
	- Good for webhooks, simple internal emails, triggering lambda functions
- SQS
	- Simple Queue Service
	- Puts messages into a queue
	- Applications pull queue using AWS SDK
	- Guaranteed delivery
	- Can retain message for up 14 days
	- Can send sequentially or in parallel
	- can ensure only one message is sent
	- Can ensure messages are delivered at least once
	- Good for delayed tasks, queueing up emails

## Inspector vs. AWS Trusted Advisor
- Both are security tools for performing audits
- Amazon Inspector
	- Audits a single EC2 instance
	- Generates a report from security checks, i.e. 699 checks
- Trusted Advisor
	- Does not generate a report
	- Gives a holistic view or recommendations across multiple service and best practices
	- Example: You have open ports on these security groups

## ALB vs NLB vs CLB
These are all load balancers but each for a different layer
- Application Layer
	- Layer 7
	- http and https
	- Routing rules
	- Can attach WAF
- Network Layer
	- Layer 4 (IP)
	- TCP and TLS traffic
	- High performance, ultra low latency
	- Optimised for sudden and volatile traffic
- Classic
	- Old solution
	- Layer 4 and 7
	- Were used for apps which were built within the EC2 Classic network

## SNS vs SES
Easily confused as both send emails
- SNS
	- Simple Notification Service
	- Practical and internal
	- Send notifications to subscriber via http, email, SQS, sms
	- Used for sending plain text emails sent from other services, e.g. billing alarms
	- Most exam questions are about SNS because most services trigger SNS notifications
	- Must know what are topics and subscriptions in SNS
- SES
	- Simple Email Service
	- Used for marketing email
	- Can send HTML emails
	- Can receive inbound emails
	- Can create email templates
	- Custom domain name email
	- Monitor email reputation

## AWS Artifact vs AWS Inspector
- Artifact
	- Answers: Why should an enterprise trust AWS?
	- Generates security report that's based on compliance frameworks like PCI (Payment card industry)
- Inspector
	- Is an audit tool for security of EC2 instances
	- Answers: How can we know this EC2 instance is secure?
	- Can we prove it?
	- Runs a script that analyses EC2 instance
	- Then creates a PDF report
	- Shows which security checks passed

