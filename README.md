# AWS-Solutions


### **Accounts**
* A container for identities (users) and Resources
  * Each account has an Account ROOT user. \[no restriction\]
* IAM Service
  * Create dif identities (users, groups, roles) with FULL or LIMITED permissions (more in depth later).

A good practice would be to create new account for DEV, TEST, PROD.
 #### Creating account
  * Use email with + trick to create new "alias"
  * Add billing method
  * On billing preferences, check 3 boxes
  * Enable Cost Explorer
  * Enable Budget Alert
  * In Account page, enable IAM access

### **Budgets**
 * Very useful to trying to maintain into the freeTier. Go to budgets on account info.
 
 
 
### **IAM BASICS**
 * Using "least privilege access" account ( create accounts for almost any service/user); grant ONLY permissions that the account needs, nothing more.
 * Every AWS account has its own IAM DB but
     * It is a global resilience service: Data is replicated in all different regions. 
 * NO COST 
    * Limits on quantity, important on real world usage.
  
 IAM service has as much priviledge as root account; what IAM trusts the account will too.
 #### Jobs (high level)
  1. Identity Provider: create modify and delete Identities
  2. Authenticate: Authenticate users (user, password, IDentitity[AD, LDAP] Federation and MFA )
  3. Authorize: Here the policies get in. 
 
 #### Tipes of identities
  1. _User_ : Represent humans or applications that need access to your accounnt.
  2. _Group_ : Collection of related users. e.g. Dev Team, HR...
  3. _Role_ : used by AWS Services, used when wanting access to account for uncertain number of entities.
     * e.g. if ALL EC2 instances want access to s3 bucket, you'll pick this identity.
  
 #### Policies
  Objects or docs used to allow or deny access to AWS Services when attached to an Identity type ( user, group, role). 
  
 #### Access Keys
  A way to login from cli or APIs. They are form from 2 parts, Access Key _ID_ and _Secret_ Access Key.
     * _Secret_ : Can only be seen when created (works as password SECURE IT!)
  * IAM users can have access keys (up to 2) without a password (or both).
  * Actions include:
     * Creation
     * Deletion
     * Made Inactive
     * made Active
     
## Cloud Computing 
(evaluate how the serv matches with this cats)
1. On-Demand Self-Service: 
   * Can provision capabilities as needed **_without requiring human interaction_**
2. Broad Network Access: 
   * Capabilities are available over the network and accessed through **_standard mechanisms_** (http/s, ssh, rdp, vpn) (private network link - NOT CLOUD)
3. Resource Pooling
   * There is a sense of **_location independence_**. No control or knowledge over the exact _**location**_ of the resources
   * Resources are **_pooled_** to serve multiple consumers using a **_multi-tenant model_**
   
    SUM: Economies of scale, cheaper service.
4. Rapid Elasticity
   * Capabilities can be **_elastically provisioned_** and **_released_** to scale _**rapidly**_ outward and inward with demand.
   * To the consumer, the capabilities available for provisioning often _**appear**_ to be _**unlimited**_
   
   SUM: Scales up/down auto in response to systemLoad
5. Measured Service:  
   * Resource usage can be **_monitored, controlled, reported_**, and **_BILLED_**
   
   SUM: Usage is measured, pay what you consume.

Source: 800-145 NIST

 ### Cloud Types - Public/Private/Multi/Hybrid
 1. **Public**:  
    Complies with 5 Cloud Computing points (CCP) and is available to everyone using only 1 vendor.
    * Multi-cloud: Used different services of different vendors.  
        * Vendors: AWS, AZURE, GOOGLE
 2. **Private**:  
    Dedicated to your business and run from business premises and **still complying with the 5 CCP.**  
    **If it doesn't comply with CCP it would really be _Hybrid ENVIRONMENT/NETWORK_**  
    i.e. Connecting onPremisse DataCenter with PublicCloud.  
       * Vendor's Solution: Outposts, Stack, Anthos
 3. _**Hybrid?**_:  
 Used public/private in conjuction     
 
 ### Cloud Service Models (XaaS)
 When deploying an application anywhere an **_Infrastructure Stack_**:  
 Collection of things that an application needs.  
 From bottom up:  
 ![alt Stack](https://raw.githubusercontent.com/l0bc/AWS-Solutions/main/resources/infStack.png)
 There are parts **YOU** mange and others the **VENDOR**  
 Unit of consumption: A part of the stack and up where **you** manage and there for pay. 
 
 For example: a DC hosting the vendor will only manage the **Facility** of the stack
 
 #### Types of aaS  
 1. **IaaS**  
 Infrastructure as a Service.  
 * _unit of consumption_: OS up.
 * Vendor Management: "infrastructure" (Thais is everything up to Virtualization).
    * i.e. EC2
 2. **PaaS**  
 Platform as a Service.  
 * _unit of consumption_: Runtime up.
 * Vendor Management: From Container down.  
    * i.e. Python app. Vendor would manage everything up to a pythonDocer container. (manly for devs)
 3. **SaaS**  
 Software as a Service.
 * _unit of consumption_: Only Application.
 * Vendor Management: Everything below Application, data, runtime,...
    * i.e. Netflix.
    
    
 ### YAML  
 Human readable data serialization language (key:value)  
 The indentation MATERS a lot. A docker-compose.yml is a very good example.  
 NOTE: when a **key:value** pair has more than one key:value pair with indentation(differenced from hiphens), it's called Dictionary (unordered list).
 
 ### JSON
 Lightweight data-interchange format (human readable and esay for machine parse)  
 **JSON** = **YAML**
 Object = Dictionary  
 Array = List  
 
 
 ### NETWORKING  
 TCP/IP 7 LAYERS PROTOCOL  
 Important, aws uses PAT NATTING or NATGatewya; MANYtoONE and uses sourcePorts to locate the private IPs when arrives to router.  
 
 
 ## AWS FUNDAMENTALS
 ### Public vs Private Services  
 Network is what matters, what can be accessed and from where
 * **Public**:  
 The PUBLIC is the one that can reach this networks  (everyone)
 * **Private**:  
 Uses VPCs: Isolated unless configured otherwise
 * **AWS Public Zone**: Network connected to the internet for public services, like s3.
 ## AWS GLOBAL INFRASTRUCTION  
 Check my .odt file of all this info: REGION > AZ (is like a DataCenter) > EDGE (like cache storaging or replication) 
    * Side thinking... If someone has services in different regions, maybe the conf in another region will be different.  
 * Region: Region Code (us-east-1), and Region Name (N.Vriginia)
 

 ## VPCs  
 Within 1 account & 1 region.  
 REGIONAL Resilient (see the AWS fundamentals.  
 Private and Isolated,  unless you dicide otherwise.  
 Types:  
 * Default VPC  
 Best practices will create de Default VPC but not used on anything Production related (some services demand to have the defaultVPC)
    * Can only have 1  default VPC per REGION (can be deleted and recreatd)
    * VPC CIDR - 172.31.0.0/16
    * Subnets to every AZ existing on the region.
    * ![VPCs defualtInfra](https://user-images.githubusercontent.com/31637504/183339619-2c0fea49-2e6f-496e-b797-2e51cb093946.png)
    * Has Internet Gateway(IGW), Security Group & NACL(networkACL)
    * subnets have public ipv4.
    

 * Custom VPC  
    * Customaze everything in detail. by default is going to be completely isolated/private.
 ## EC2 - Elastic Compute Cloud  
 Default starting point for computer requirements.  
 #### Key Facts  
 * IaaS - Provides Instances (VM) 
 * Private VPC by-default. (on defaultVPC)
    * AZ Resilient - If AZ fails, instance fails
 * On-demand Billing (per second/hour)
    * Storage
       * localhost storage
       * Elastic Block Store (EBS)
    * CPU,RAM consumption
    * Extras; commercial software.
 * Lifecycle - states
    * Running; can jump between stopped & terminated. If terminated, the Instance **WILL BE DELETED**
       * Will charge you on EVERYTHING (Storage, RAM, CPU, Network Traffic)
    * Stopped
       * Charges on: Storage.
    * Terminated
       * No charges, but deletes info.
 * Amazon Machine Image (AMI)  
 Like bootable usbs, or preConfigured images on HypV.  
 Can create EC2s from AMI or create AMI from EC2.  
 *  Permissions:
    * Public - everyone (windows/linux ec2 are on this group.)
    * Owner - Implicit (If I'm owner of AMI I can create Instances on it for me,)
    * Explicit - specific aws accounts grant.
 * Root Volume  
 Contains the boot volume of the Instance
    * Windows: c:\
    * Linux: / (root)  
 Will always exists (can have more than 1 disk/partition mounted).  
 * Block Device Mapping  
 File that maps, identificates volumes mounted
    * Linux: /etc/fstab
