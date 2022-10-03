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
 
 
 
## **IAM BASICS**  
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
## s3 Storage Basics  
Global Storage Platform - regional based/resilient.  
Public service, unlimited data & multi-user.  
Perfecto for almos any data type; movies, audio, photos, text, large data sets...  
Delivers:  
* Objects - wecould say like _file_
   * Key: like fileName
   * Value: **0 - 5 TB**
* Buckets - we could say like _directory_
   * Restrictions:
      * 3 to 63 characters; all lower case, no underscores
      * start with lowercase letter or number
      * Cannot be IP formated, e.g. 1.1.1.1 
      * 100 soft limit per account
      * 1000 hard limit ( by contatcting support can increase up to 1000 buckets) per account.
   * Created on specific AZ. And has primary location on it.
   * Blast Radius = Region.
      * If major failure occurs (natural disaster, huge data corruption) the error will be contained only in that region.
   * Name need to be **Globally Unique** (cannot exist the same name ANYWHERE including other aws accounts)
   * Inifinite scalabe storage system.
   * Flat structure: Everything have the same level (folders don't really exist, eventhough the UI will represent some folders with data inside )
      * Folders are really refer as prefexes of files. (i.e. /old/foo.jpg)
* Patterns & antiPatterns  
Is an **object store**. NOT FILE (e.g. networkFile System) or BLOCK - (essentially virtual hardDrives(can be mounted)e.g. EBS).
   * Great for _offload_  
   e.g. If have blog with a lot of files, this is a great choice.
   * Think s3 is best for I/O of AWS products.

## Cloud Formation BASICS  
Tool to create/update/delete infrastructure in consistent and repetible ways by creating templates.  
Written in YAML or JSON.  
Every template has Resources and _all other things that will be seen in detail after_
* Resource
   * Is a list of resources called: *_logical Resource_*
      * The logical Resource has *_Type_* and *_Properties_*
      * The Type has its own formatting and will instruct what kind of good will be created (ec2, s3, ...)
   * Template will create a STACK for every Resource.
   * The Stack will create the matching Physical Resources; actually creating the goods. 
      * If the template if modified/deleted, then the stack will match the template and will implement the actions to pythisical Resources.
## CloudWatch BASICS  
Collects and manages _operational data_ on your behalf.  
_operational Data_: Any data generated by an environement that details how it performs, normally runs, and logging data.
![Capture d’écran du 2022-08-11 06-08-59](https://user-images.githubusercontent.com/31637504/184063415-5e885adb-1c34-41e3-ab73-e3a2354d9202.png)  
There are 3 main products in one
   * **CloudWatch**: Collection, Monitoring, and Actions based on _metrics_.   
      * _Metrics_:  Collection of related _dataPoint_ on a time Order data Structure. Data related to AWS Products, Apps, on-premises.  
      e.g. CPU utilisation of ec2, diskSpage usage of on-premises SRV, number of users on your webApp, Network I/O.
         * dataPoint: 
            * Timestamp: year-month-day-hour-min-sec-TZ
            * Value: % (in CPU usage for ex.)
         * dimensions:  
         Powerful 'tag' to differentiate _dataPoints_ from each other ( if different EC2 instances are sending the same metric _dimension_ will clasify them.
         * alarm: Can be think as _cloudWatch Event_. Will create an action BASED ON METRICS. 
            * 3 states: OK (not triggered), ALARM (triggered), INSUFFECIENT DATA(needs more data to be enabled).
      * Some products collect data by default. For other products/services a **_CloudWatch Agent_** is required.
   * **CloudWatch Logs**: Collection, Monitoring, and Actions based on _logiging Data_.  
   * **CloudWatch Events**: Event Hub.
      * Trigger by Action: Can trigger event after another event has been executed ( triggering a EC2 instance, creating service, etc. i.e. Similar to Lamda concept)
      * Schedules: Literally as a cronJob. Based on time instead of on action
**NameSpaces**: A way to organize data collected by cloudWatch. Can be viewed as container/folder.  
Every AWS service will create its own _nameSpace_ in the form of: **AWS/service**.  
By association/heritacy the AWS nameSpace is reserved to automatically created AWS services.

## Shared Responsability Model  
Like X as a Service template(aaS) but security wise.  
![Capture d’écran du 2022-08-12 18-52-45](https://user-images.githubusercontent.com/31637504/184406532-fe09303e-0642-4318-9a7e-c6e85d38ae71.png)  
NOTES RELATED TO PHOTO:  
   * **AWS**: 
      * _Software_: It's refering to the Hypervisor,UI that administrates the Instance (e.g. EC2).  
## HighAvailability(HA) vs FaultTolerance(FT) vd DisasterRecovery(DR)  
* **HA**, _Ensures_ an agreed level of operational _performance_(_uptime_), for a _higher than normal period_).
   * Design to be providing services and be fixed as OFTEN as possible. (i.e. If systems fails but are quickly fixed it's still an HA Service).
   * 99,9% threshold to be categorized as HA (8.77 hours/year)
   * 99,999% (5.26 hours/year)
   * Some solutions could by redundance,when having, for example, 2 servers. A lower exmaple could be the reconfiguration of Root switch when 1st root dies.
* **FT**, Property than enables a system to _continue operating properly_ in the event of the _failure of some_ of its _components_.
   * So we can say that its like HA but without a second of downtime.  
   An example could be: HA would be a heart transplant; there's a moment that the body is really dead ( seconds between the swapping of hearts).  
   FT would be a brain surgery; there can be NO ERROR, the person needs to be still giving words to ensure congivity, work...  
* **DR**: Set of policies, tools and procedures to _enable the recovery_ or _continuation_ of _ vital_ thechnology infrastructure and systems _following a natural or human-induced disaster_. (i.e. ROLLBACK(snapshots?)).  
It is composed by 2 primary things:
   * **_Pre-planning_**:  
      1. Having standby premises ready for example  
      2. Having extra hardware ready to go.  
      3. Creating Backups (snapshots)
   *  **_DR Process_**:  
      1. If fails can toggle cloud solution for example.  
      2. Implementing extra hardware when needed.  
      3. NOT BEEING IN THE SAME PREMISE AS PRE-PLANNING!
## DNS 101  
Discovery Service.
Its huge and has to be distributed (the herierchy of DNS NSes).  
   * Key words,
      *  _authoritative| authority_ equals something that is trusted.
         * Only the root (or first NS contacted will be the authority)
      * Walking the tree: when it recurses the tree by the NS until arriving to the answer wanted.
DNS ROOT SERVERS (only 13 SRVs CLUSTERS A-M) and managed by IANA.  
DNS ZONE FILE: we can think of it as the main URL (i.e. amazon.com).  
   * This file will have **RECORDS**=_subURLs_ (i.e. aws.amazon.com | www.amazon.com...) 
   * ACTUALLY the DNS clients doesn't talk to the NS, there's a software called RESOLVER( only function; queries the NS).
      * Has **_Root Hints_** (thats how the resolver can find the nameServers (root ones; from there the root srvs will guide you down if not found)
   * The file is stored in NS (NameServer)
Top level domains(TLDs) are the 2nd part of the address (.com/.org/.io...) and managed by REGISTRY
   * Can be known also as cctld (country codeTLD; mx/fr/uk/...)
## ROUTE 53 BASICS  
There are 13 ROOT servers.
It register domains, host zone files to ( on managed NS), and is GLOBALLY Resilient.   
**Authoritative answer** = the query record we where looking for came from the DNS tree. (result...)
**Non-Authoritative answer** = record retrieve from the Resolver's cache. 
**TTL** = The time (in seconds) where the records will be saved on Resolver's cache.
**PIR** = Organization that manages .org
STEPS when registering domain by Route 53:
   1. Service speacks with TLD srv to seee if domain exists.
   2. Service creates zoneFile (example.org) and allocates the file in AWS mangaged NSs. (normally 4 by zone). 
   3. Service talks again with the TLD and adds the nameServerRecords (NSR) to the TLDs.  
#### ZONES (HostedZones in AWS = ZoneFiles)
Create and manage ZoneFiles. 
It will be hosted on 4 managed servers.  
Can be **public** or **private**. The information are records ( DNS records are the urls we are familiar with ( there are other ones too but will be seen later.)

#### Records  
There are different types of DNS records. Some of them are,
   * **NameServer**: Files to be able to delegate trust between servers on the DNS TreeNetwrok
   * **A** or **AAAA**: its a host to IP record. **A** maps to IPv4 **AAAA** maps to IPv6
   * **CNAME**: HOst to Host records. Canonical records whos function is to decrease A records. If you have different protocols and want to map them yo DNS (i.e. ftp/mail/smtp) CNAME records are created and mapped to an A/AAAA record (cannot be mapped to IP). If the A/AAAA Record is updated, the cname will not be affected and will also be updated.
   * **MX**: Record used more common on smtp (mail). Record's example would be: MX 10 gooMail.
      * The number of the record is a priority, used when more than 1 MX record exist in the Zone's records. The requester will choose the record with the lowest number (higher priority), if the server doesn't respond, i chooses the 2nd one.
      * A MX record can point to a completely unique DNS record (it isn't constrained to the Zone)
   * **TXT**: To prove domain ownership. Maybe an authority will ask you for a string. If that string exists (the authority will query a TXT record on your zone) then the authority will accept that you are the owner. 

## IAM Identity POLICIES  
Set of security settings for AWS. Grants or Denies and created in JSON.  
Statements: can be 1+. Divided by curly braers.  
There are 2 ways of incororating Policies; Inline Policies or Managed policies. Same structure as CSS inline <style> tag or using a css file or using the tag as global.  
The inline policy is used when a exepltoinal/special policy will be given to user/application.  
![IdentityPolicyExample](https://user-images.githubusercontent.com/31637504/184577448-5620d342-ecba-463a-89f0-f14198def88a.png)  
_**Components**_:
   * _Sid_: Statement Id. (optional but always preferable to use)
   * _Action_: can have 1 or more action, could be as wide or as detailed as you want.
      * Specific action
      * wild card
      * list of specific actions.
   * _Resource_: Just like actions ( in formating ) but talks about resources in AWS
   * _Effect_: Allow/Deny. The resources and Actions it had matched.  
   _**Priorities**_:   
   When overlapping the priorities are as followed:
      1. Explicit DENY
      2. Explicit ALLOW
      3. Defualt DENY (IMPLICIT). 
   _we can say its a deny all infra. and after you can give allows to unlock permissions (but an explicit deny will have higher priority)_.  
 
 ### IAM Users  
 Identity used for anything requiring LONG-TERM aws access (.e.g. Humans, apps or service accounts).  
 _Principle_ : Entity trying to access an AWS account. A _principle_ can be people, app, service, or a group of those.
    * It needs to be **authenticated** by IAM and then IAM will **authorize** the action that the principle can do.  
 Amazon Resource Name (ARN) allow to refer to a single or multiple resource within ANY AWS account(formatting is similar to IPv6 as you can see).  
 ![image](https://user-images.githubusercontent.com/31637504/184632402-81b88f7d-6064-4c67-8246-6911b89c531d.png)  
 
 _**keyValues**_:
    * max 5 000 IAM Users per account.
    * 1 IAM User can be member of 10 groups.
    * Could impact system design
       * Internet-scale apps ( number of users )
       * Large orgs | org merges.
       * _there exists solutions for this with roles or Identity Federation._
### IAM Groups  
Trick question could be: can you login into a IAM Group? NO.  
Some Characteristics to know:  
   * Users in group inherits all groups policies and merges them with its own policies too.  
   * No limit of Users in group (can have all 5000 users in all group).  
   * There is no allUser groups by defaults
   * No NESTING
   * Max of 300 Groups (can be bigger if contacting support)
Policies can be attached to resources (s3 for example). This policies known as resource policies can reference identities. 
   i.e. A bucket has a policy associated with that bucket and the policy can give Sally access to the bucket ( resource policy ) by refereing the identities using (ARNs)  
   * PD: Groups are NOT a true identity, The CAN'T be refered as a principal in a policy.
 
### IAM Roles  
Best suited to be used by an unkown number or multiple principles.  
   * i.e. Multiple users on the aws account or different user, apps, or services inside or OUTSIDE your AWS.  
It can be used for "temporary" basis; something becomes that role for a period of time and then stops.  
   * The level represent a level of access but NOT YOU. (like borrowing the permissions).
 
 Roles have 2 types of policies:  
   * **_Trust Policy_**: Controls which identities can assume the role. Can reference user, roles, or SERVICES (like EC2 ) in or out the AWS Account.  
      * It will create temporary Credentials to uers assuming the role (time limited). Created by STS ( SecureTokenService _[sts:AssumeRole]_).  
   * **_Permissions Policy_**: The temporary credentials are the ones that are linked to the Permissions Policy. Uses to authorize. 
   
## When to use IAM ROLES?  
1. The most common are the AWS Services themselves. (like AWS Lambda; function as a Service Product).  
   * **PoC**: Will create a _Lambda Execution Role_ 
      * Trust: Has a trust policy witch trusts the Lambda Service. (will asume the load whenever the lambda Function is executed)  
      * Permission Policy: Grants access to AWS products or Services.  
   When the function runs it'll run sts:AssumeRole wich will execute the secureTokenService creating temporary Credentials to the temporary runTime env.  
Why is it so powerful? It eliminates the need of hardcoding credentials in the code (vulnerability) and makes dynamic Authentication tolerant to upgrades.  
2. BreakGlass style Situation: [ metaphor to BreakGlass for extinguisher, etc. EMERGENCY ).  
Emergeny Role with higher privileges that WILL BE LOGGED.  
3. Adding AWS to existing corporate ENV. (hybrid Cloud)
   * **PoC**:  When wanting to reuse existing identities in, for example, AD or when you're restrained by the 5k max IAM users.
   * **PoC**: WEB Identity. (using google/fb/twitter to loggin) Uses IAM Role to interact with AWS Resources. SCALABLE.  
   
## Service-Linked Roles  
* Very specific IAM Roles that's likned to a specifi AWS service.  
* The role is already predefined by a service.  
* Provides permissions that a service need to interact with other AWS services on my behalf.
* The same _service_ (or _IAM_)can create/delete the role...  
* Can NOT be deleted if it's still in use (if the service that needs it still is in use/exists)
* **_PASS ROLE_: Method inside AWS that gives avilibity to implement ROLE SEPARATION** the example would be using cloudWatch...  
   * **PoC**: The user bob has permission to use CloudWatch but maybe cannot create an EC2. If he creates a CloudWatch template, the stack will _'PassRolePermission'_ to create the resources in the AWS Account.  
   
## AWS Organizations  
Product which allows larger business to manage more than 1 AWS Account in cost effective way, and little to no org overhead. It has a herarchical architecture in a ReverseTree mode (similar to DNS NS) 
### _**How it works?**_:  
1. You choose 1 account who would be the _standard account_ (It can't be inside an organization) and create the Org. here. The organization will be created INSIDE this account but the account won't be inside de org.  
2. The CREATOR account is called: **Management Account** (called MASTER Account before). 
3. THe **Management Account** can send invitation to _standard accounts_. If the invitation is accepted then the invited account will become a _Member Account_.  
4. **Consolidated Billing**: The billing method is removed from the _Member Accounts_ and is send through to the Management Account (also known as payer Account in financial). Will only receive 1 bill with ALL billing of all the AWS Org. 
   * Pretty good to reduce prices due to AWS billing structures; There are AWS Services that are cheaper if they're used more. If the same service is used in different _member Accounts_ the usage will be pooled and its a way to enjoy(classify) to the cheaper/higher consuming rates.  

### Herarchical Structure  
Inverted Tree starting with:  
* **Organizational Rool (OR)**:  
   * Different to ROOT account.  
   * Container inside an AWS Organization that can contain  
      * Member accounts.  
      * The Management Account.  
      * Other containers, called OUs.  
* **Organizational Unit**:  Can contain the same types as the OR. This options gives the chance of creating pretty complex herierchies.  
* **Loggins**: Best Practices(BP) are to have a specific _Member Account_ that manages the Authentication (IAM) and using **IAM Roles** to the other _Member Accounts_ This other _Member Accounts_ will only have IAM Roles. ALSO, keep Management Account only for billing (BP on BIG companies). 
 
### Service Control Policiles (SCP):  
 Still a service of AWS Organization. JSON Documents (like IAM Policy) 
 * can be attached to the Org as a hole.  
 * To 1 or more Org.  
 * Individual AWS Accounts.  
 The Policies are inheritted down, everything that has les herierchy will be affected by a SCP. BUT the _Management Account_ is NOT affected by a SCP.  
 Best practices; Never use the _Management Account_ on any resource/service in prod envs.  
 Some **Characteristics** of SCP:
 * SCPs are account permissions boundaries.  
 * They can limit the accounts.  
    * This would _restrict_ an account ROOT user (even though the ROOT account can't be restricted) by restricting the account as a hole. It's an indirect Restriction.  
 * They **DON'T GRANT** any permissions. (its a boundary delimiter). But can establish what could be granted. Its a higher heriarchy than IAM Policies, 
    * i.e. If a IAM Policy is created for granting EC2 instances accessing s3 buckets BUT Theres a ORG wide SCP denying entry to s3 buckets the IAM Policy will have no effect.  
 * Can have a **ALLOW** List or **DENY** List structure.  
    * ![image](https://user-images.githubusercontent.com/31637504/185287682-8185eac3-11e8-40d0-a0ed-2d73ca930d6d.png)  
       * If there's no FullAWSAccess SCP, then the structure will be DENY ALL and start opening services as needed (this is preferable security wise).  
 ## CloudWatch Logs  
 Public Service: It can be used from AWS | on-premises (all the way to another cloudProvider). A powerful char is that it can create **metrics** based on logs by scanning the logs creating _metric filters_.  
 _Charecteristics on logging Data_:  
 * Stores  
 * Monitors  
 * Access  
 _Integrations_:  
 * AWS Services; EC2, VPC flowLogs, Lambda, cloudTrail, R53...  
 * Unified CloudWatch Agent : when outside of AWS (on-premises or another cloudProvider).  
 _Architecture_:  
 ![cloudWatch Arch](https://user-images.githubusercontent.com/31637504/185293037-0c168408-0ebf-4db8-a3b0-9483a41c8ea3.png)  
 ## cloudTrail Essentials  
 Product/Service that logs all (or almost all) activity in AWS Account.  
 **REGION BASED.**  
 * Logs API calls/accountActivities as a **_cloudTrail Event_**  
 * Sabes 90 days by default in _Event History_. 
    * Service activated and free by devault.  
 * Trail: used to customise cloudTrail Events.  
 There exists 3 different types of events, we'll be concentrating on _Management_ and _Data_ Events for now (The 3rd one is called _Insight_).   
 * **Management**: Provide info about management info performed by resource on the AWS Account. called **_controlPlain Ops_**.  
    * CPOs e.g. : creating, delting, modifying EC2 instance.  
 * **Data**: Information about resource OPERATIONS made on or TO resources.
    * Example: when accessing a s3 bucket, uploading/downloading data, lambda execution.  
    * NOT enabled by default.  
 ### cloudTrail Trails  
 Unit of configuration within the cloudTrail product. Provides configuration on how to operate. Trails are logged by regions.  
 This trails will be captured _Management & Data_ events. Remember DATA is not enabled by default.  
 NOT REALTIME - There's a delay of 15 mins.  
 Configurations on Trails:  
 * _One Region loging_: The trail will log on the region that it's been created.
 * _All regions logging_: Logging all regions; it really creates a collection of trails on every region but managed as 1.  
    * One great feature of ALL-regions Logging is if AWS add a new region it will be added automatically. 
 * _Global Logging_: Global services are in this category (s3, AMI, STS, CloudFront). 
    * To log _global Logging_ the configuration of the Trial needs to enable this feature.  
    * Enable by DEFAULT if using userInterface to create the Trail.  
    * will be logged to the us-east-1 region.  
 * Log history can be configured to more than 90 days.  
 * Can be saved on s3 buckets.  
 * Can export the data into cloudWatch Service.  
 NEW FEATURE: A AWS Org trail can be created. Will log all actions encapsuled by ORGs. 

 ## AWS Control Tower  
 Allows **quick** and **easy** setup of **_multi-account_** environment. It orchestrates other AWS services to provide the functionality.  
 ![controlTower arch](https://user-images.githubusercontent.com/31637504/185438394-a35ef818-b2ae-43d0-a8dc-66851fc8cdb1.png)   
 Services orchestrated:
 * Organizations.  
 * IAM Identity Center (formerly known as AWS SSO).  
 * cloudFormation.  
 * AWS Config.  
 ### Characteristics/Parts of controlTower:  
 Can be thinked as Organization on steroids.   
 The **landingZone** is a **WELL ARCHITECTED** multi-account env (homeRegion = the region where it was created/implemented). The UI (where the majority of users will be interacting with.)  
 It provides:  
 * _SSO/ID Federation(AD)_.  
 * _Centralised Logging & Auditing_  [part of Security OU (also knwon as: foundationalOU) pd: there's another OU created (sandboxOU)]  
    * cloudWatch  
    * cloudTrail    
    * AWS Config  
    * SNS: simpleNotificationService  
 * _Guard Rails_: **Detects/Mandates** rules/standards across all accounts.  
 There are 3 types of _rules/standards_  
    * Mandaroty - Always applied.  
    * Strongly Recommended - SUPER RECOMMENDED.  
    * Elective - used to implement fairly niche reqs. OPTIONAL  
 **_Functioning_**:  
 STATES: _CLEAR_, _IN VIOLATION_ or _NOT ENABLED_
    * _Preventive_: Stop you doing things (SCPs(part of AWS Orgs)). Can be Enforced or not.  
    i.e. allow/deny regions or disallow bucket policy changes. 
    * _Detective_: Compliance checks (AWS Config Rules.)  
    i.e. detect cloudTrail enabled or EC2 having IPv4.  
 * _Account Factory_: Automation and Standarization on creating new account.  
    * Allowed by cloudAdmins or endUsers.
    * Can give **_admin Account_** to given named user (IAM Identity Center)  
 * Dashboard: Single page oversight of the entire env.  

 ## s3 Security
 Buckets, the hole service really is private **by default**. To open permissions on this service there are:
 * _s3 bucket Policies_: A type of resource policy. As its name defines it, it's like a identity Policy but it's jointed to _resources_ instead of Identities. The **Principal** part of the _Statement_ in the policy defines to whom that statement applies to (Identities).  
    * _perspective Permisssions_: Controls who can access the resource. (instead of what can a user do)  
    * _Allow/Deny Constraints_: Different form Identity Polices, _Resource Policies_ influences/manages different accounts. 
       * The policies in place influence everyone accesing the _resource_ regardless if they're on the same or **different** account.  
       * **Anonymous** principals can be created. This gives access/denial to any entitiy even those who're not authenticated in AWS.  
 * _ACLs_: Its used on objects and buckets but they're dying. Even AWS doesn't recommend them due to its lack of flexibility, they're pretty constrained not giving you the possibility of creating more complex permissions.
    * Caracteristics: Subresource, Legacy(outdated)  
       * It can't inlfuence a whole list (the ACL needs to be implemented individually; on a _bucket_ or an _object_. It cant influence a list of...  
 * _Block Public Access_: Newest feature. It's installed in between the accessing of a **ANONYMOUS** Idenitty into a BUCKET with Anonymous access enabled. It's above herierchaly to the Bucket Policy.  
  Theres 4 different profile Settings:
    * ![BLOCK PUBLIC ACCESS](https://user-images.githubusercontent.com/31637504/185538796-3cbbf39a-aeae-46b6-8007-ace18d323c21.png)  
 #### EXAM POWERUP
 **Identity** vs **Resource** POLICIES, when to use what? :  
 * Identity:  
    * When controlling different Resources accross 1 AWS account.   
    * If having a preference for IAM.  
    * If the accessing comes only from 1 same account.  
 * Resource:
    * Controlling only 1 Resource (i.e. s3)  
    * Anonymous or cross-Account Grant.  
 * NEVER use ACLs unless you MUST.  
 ## s3 Static Website Hosting  
 Normal acces is via **AWS APIs** giving it powerfull functionallity to access it via HTTP ( thinking of it as a RESTful API Structure).  
 _Index_ and _Error_ documents are set automatically.  
 Also a _website Endpoint_ is created,  
 The domain name structure is created by a conjuction of the bucket's name, region, and awsstring.  
    If wanting to have a custom domain you create it via Route53 BUT **the bucketname needs to be named exactly as the custom domain** (including DNS topLevelDomain(TLD) names)  
 _2 COMMONLY USED EXAMPLES_  
 * _Offloading_:  outsourcing media of the computing power. If having a webiste, saving all media in a bucket and then referencing the media requests to the s3 bucket. This lower the Computer consumption. 
 * _Out-of-band Pages_: when, for example, putting a website in maintenance a great solution is the static website s3 hosting. Only changing the DNS value to the static website meanwhile the upgrades/debugging/changes are being made on the real complete server.  
 
 ## Object Versioning and MFA Delete 
 ### Object Versioning  
 Controlled at bucket level & ones enable it cannot go back to be disabled (but can be suspended).  
 When versioning is enabled operations which would modify objects will **generate a new version** and use the id value of each object to be able to differintiate verions (when disabled id = _null_).  
 * _Current Version_: Latest version of object.  
 * _Deletion_: Logically will only add a marker above the version you "want to delete" but in escense it's only hidding it. 
    * The marker can be deleted making the previous versions available again. 
    * For permanently deleting an object (or version of object) the id of the wanted object needs to be specified.  
 **ATTENTION**: _Fixating on not being able to disable the versioning is on the deletion actions (it will not be deleting the objects in the conventional matter( as mentioned before)) and storage will grow faster due to all the different verions that it's also storing._  
 ### MFA Delete  
 Versioning needs to be enabled to use this feature. 
 If enabled MFA is required for changing **Object Versioning** state (enabled <-> suspended).  
 Also requiered to FULLY DELETE a version. The MFA TOKEN is requiered
 * **MFA TOKEN** - The concatenation of:  
    * MFA's Serial number.  
    * Generated token.  
## S3 Performance Optimization  
 ![Example Architecture](https://user-images.githubusercontent.com/31637504/186460688-6e04a58d-93d4-4fb6-ad6d-51f0da7b4231.png)  
 #### Performance Characteristics:  
 * When upload: the file is converted to object and uploaded ina signle data stream to s3 ( s3:putObject )  
 * If stream fails - upload fails ( doesn't matter the percentage that has already been uploaded )  
    * Requires full restart.  
 * 1 port upload has a 5GB max ( eventhough, never trust a 3GB+ file on this SINGLE PUT upload )
 * Speed & Reliability = limit of 1 stream.  

 #### Multipart Upload  
  Solution to constraints s3 _singlePUTUpload_ has.  
 Think of it as _torrent_:  
 * Data is broken up  
    * up to 10 000 max parts
       * from 5MB - 5 GB pp.  
       * last part can be smaller than 5MB though.  
 * min data size = 100MB for using this service.  
 * **Transfer Rate = speed**: sum of all individual uploads  
 #### s3 Transfer Acceleration.  
 Default is OFF. To turn it on:  
   * BucketName cannot contain periods  
   * Needs to be DNS compatible.  
 It uses EDGE Locations ( starting with the geographically nearest to you ) to route your data into the bucket instead of using the public internet. Pretty obvious being a smaller network it will be much faster than the public internet.  
 webpage to compare velocity using this feature or NOT to an specific region: http://s3-accelerate-speedtest.s3-accelerate.amazonaws.com/en/accelerate-speed-comparsion.html  
 ## Encryption 101  
 2 main approaches on encryption:  
    * _Rest_: Encrypting a disk for example. If a computer is stolen, it would have encrypted data.  
       * Used when 1 entity (person maybe) is used.  
    * _Transit_: Like ssl/tls, the encryption is in route. You create a Tunnel around the raw data.  
 _Encryption Concepts_:  
 * _Algorithm examples_: Blowfish, AES, RC4, DES, RC5, RC6.  
 * _Symmetric Encryption Keys_: Static key to decyrpt/encrypt data.  
 * _Asymmetric Encryption keys_: Key pairs (public/private keys).  
    * _Public_: Only works to ENCRYPT data. 
    * _Private_: Used to DECRYPT data. 
 So in a nutshell:  
Encryption:  
 iNPUT: PLAINTEXT.  
 input + key INTO an _algorithm_ = CipherText.  
 #### Steganography  
 Hide something "in plain site". Is a way to send data or have data that is encrypted but it's not obvious that it's encrypted (or has hidden data).  
 ## Key Management Service (KMS)  
 * Regional & Public Service  
 * It creates, stores and Manages Cryptographic Keys
    * Handles Symmetric & Assymetric Keys
 * Does crypto operations (like _encrypt_ and _decrypt_) but has a max 4KB data size for direct encryption (there's a workaround...).  
 * **Keys never leave KMS - Provides _FIPS 140-2 (L2) Standard_. (memorize standard)  
 * KMS Keys are isolated to a Region.  
 * Can be AWS owned or customerOwned (almost not interacting with AWS owned as user).  
    * Customer owned keys can be managed by _Customer_ or _AWS_.  
 * KMS Keys can use Rotation.  
    * It can decrypt an old version even after a rotation.  
       * Can use aliases to manage.  
 * Every Key has a policy file.  
 #### Process  
    1. User picks Region.  
    2. Creates Key (CMK) and is saved in KMS (encrypted).  
    3. Creates _Encrypt_ call and data to be encrypted.  
    4. KMS Service _encrypts_ IF SHE'S AUTHORIZED and returns the encrypted data to the user.  
 The permissions are independent from eachOther (roleSeparation)  
 * Encryption  
 * Decryption  
 * Creation/Deletion of keys.  
 _Workaround of 4KS_  
 It's by creating a ney key = DataEncryptionKey (DEK).  
 Created by the _generateDataKey_ function of KMS + a _CMK (KMS created Key)_.  
 Process:  
 1. After creation the service will give you 2 keys (we can think like symmetric and asymmetric key)  
    1. Plaintex Version (symmetric).  
    2. encrypted Version (symmetric) using a kms key.  
 2. Encrypts data using plainText key.  
 3. Deletes the plainText version  .
 4. _stores encrypted key_ with data.  
 ## s3 Encryption  
 _Buckets AREN'T encrypted, objects are..._  
 There are 2 (or 3?) types of encryption:  
 1. **Client-Side**  
    * Uses in-transit encryption (encrypted tunnel)  
    * Before uploading, the data is already encrypted. AWS s3 will never have plainText data. 
 2. **Server-Side**  
    * Also uses in-transit encryption.  
    * Data is encrypted until arriving to s3. (from client-server(s3) it goes via plainText inside https tunnel)  
    * Uses more CPU because the encryption are being made in AWS.  
    * **_3 types of serverSide Encryption_**:  
       1. _SSE-C_: Server-side Encryption with Customer-Provided Keys.  
          * Customer Manages Keys and s3 Manages the Encryption.  
          * Customer gives key and object to AWS.  
          * AWS s3 saves hash of key into encrypted file ( this makes sure the same key was used to encrypt when trying to decrypt).  
       2. _SSE-s3_: Server-Side Encryption with Amazon s3-Managed keys. Uses AES-256.  
          * Diff from _SSE-C_ user only provides plainText object.  
          * s3 creates a masterKey for the encryption process.  
          * s3 will create a new key SPECIFICALLY for every uploaded object. After that s3 will use the _MASTER KEY_ to encrypt the uniqueKey of object. The original key is discarded.  
          * when this method is NOT SUITABLE:  
             1. When need to control keys and access to the keys.  
             2. When need to control keyRol.  
             3. When need to have role Separation.  
       3. _SSE-KMS_: Server-Side Encryption with Customer Master Keys (CMKs) Store in AWS Key Management Service (KMS).  
          * Pretty similiar in a high level view from _SSE-s3_ the difference is on the MASTER KEY. KMS will create a CMK and store it in the KMS Service; this key will work as the MasterKey.  
          * When encryption happens...
             1. KMS creates a dataKey and encrypts it using the CMK.  
             2. KMS sends BOTH keys to s3 to create the encryption.  
             3. Encryption is made with the plainText key and then it's discarded.  
             4. s3 saves encrypted data and attaches the encrypted key to it.  
          * The superPowerful feature of _SSE-KMS_ is than the CMK can be a custome one; providing control of the key (rotation, roleSpecific).  
          * when DECRYPTION happens...  
             1. The CMK is used to decrypt the attached encrypted dataKey.  
             2. The decrypted dataKey is used to decrypt the cipherText.  
          * If admin/user cannot have KMS access then he'll not be able to decrypt things.  
 ![summaryTable s3 Encryption](https://user-images.githubusercontent.com/31637504/187832191-acb05aec-fba5-441b-95f0-5dd207e1486a.png)  
 3. _Bucket Default Encryption_  
 If adding a header: AES-256 | aws:kms it will use the encryption on the header.  
 If the header is not specified, the BUCKET DEFAULT ENCRYPTION will be used.  
 ## s3 Object _Storage Classes_  
 ### _s3 Standard_:  
 Objects are replicated across at least 3AZs in the AWS Region.  
 _When to use?_ For **Frequently Accessed Data** wich is IMPORTANT AND NON REPLACEABLE.  
    * Has eleven 9s of durability = for 10M objects, 1 object loss per 10k years.  
    * Has different mechanisms/checks to detect & fix data corruption.  
       1. Replication over 3 AZs.  
       2. Content-MD5 Checksums.  
       3. Cyclic Redundancy Checks (CRCs).  
    * When an object is updated succesfully, HTTP/1.1 200 code response.  
    * **_PRICE_**  
       * billed a GB/month fee for data stored. 
       * fee per GB for transfer OUT
       * fee per 1k requests. 
       * NO specific retrieval fee, no minimum duration, no minimum size.  
    * 1ms first byte latency
    * Objects can be made _publicly available_.  
 ### _s3 Standard-IA_(InfriquentAccess):  
 _When to use?_ For IMPORTANT & NOT REPLACEABLE DATA BUT **Infriquently Accessed**  
 Same _durability, dataCorruptions Mechanisms, Replicatoin_.  
    * **_PRICES_**  
       * 1/2 price of data storing compared to _ standard_.  
       * There's an extra fee on retrieval (additional to transport fee).  
       * Minimim duration charge = 30 days.  
       * Minimum capacity charge = 128k per obj.  
    We can see if lots of small objects, short duration of objects or constant retrieval THIS IS NOT THE SOLUTION.  
 ### _s3 One Zone-IA_:  
 Cheaper than the 2 above.  
 _When to use?_ For longLive data, infriquently accessed and NON CRITICAL or EASILY REPLACED.  
    * Has the same _minimum constraints_ as _S3IA_ and retrieve fee.  
    * Chepear because it lacks Replication in other AZs (only 1 as the name provides).  
       * It still has eleven9s durability.  
 ### _s3 Glacier - Instant_:  
 Like s3 Standard-IA... but; cheaper storage, more expensive retrival, longer minimum.  
 It comes in handy when you need instant access but less frequent than _Standard-IA_ (once every quarter).  
    * Minimum duratoin charge = 90 days  
 ### _s3 Glacier - Flexible Retrieval_:  
 Same _durability, data COrruptions Mechanisms, Replications_.  
 _When to use?_ When storing archieval data where frequent or realTime access is not necessary.  
    * **PRICES**  
       * 1/6 of s3 Standard storage fee.  
    * **RESTRAINTS**  
       * Objects canNOT be made _public_.  
          * Any access of data requires a **retrieval Process** (beyond object's metadata).  
          * Minimum size = 40KB  
          * Minimum duration = 90 days.  
       * When retrieved the object is saved in SIA TEMPORARELY. (TYPES; faster = +Expensive)  
          * _Expedited_ (1-5 min)  
          * _Standard_ (3-5 hours)  
          * _Bulk_ (5-12 hours)  
       * First byte latency = minutes | hours.  
 ### _s3 Glacier Deep Archive_:  
 _When to use?_ To store archive data that is rarely or never accessed.  
 Data in a _Frozen State_.  
 * **RESTRAINTS**  
    * As all archives, data cannot be publiclty accessible.  
       * Minimum size = 40KB  
       * Minimum duration = 180 days.  
    * When retrieved, goes to SIA TEMPORARELY also but _timeRetrieval_ varies:  
       * _Standard_ (12 hours)  
       * _Bulk_ (up to 48 hours)  
 ### _s3 Intellingent-Tiering_  
 As you can deduce, it is the solution where it automates and makes dynamic the storage tier storage.  
 _When to use?_ When _long-lived data_ with _changing_ or _unknown_ patterns.  
Contains 5 different storage tiers.  
   * Frequent Access.  
      * After 30 days of unAccess moves to _IA_.  
   * Infrequent Access.  
      * After 90 days of unAccess moves to _Archive IA_.  
   * Archive Instant Access.  
      * After 90-270 (configurable) days of unAccess moves to _Archive Access_.  
   * Archive Access. [OPTIONAL]  
      * After 180-720 (configurable) days of unAccess moves to _Deep Archive_.  
   * Deep Archive. [OPTIONAL]  
PRINCIPAL DIFF: has a fee per 1k object monitored ( instead of the retrieval fee other solutions have ).  
## s3 LifeCycle Configuration.  
 **Set of rules** wich apply to a bucket.  
 * **rules** = _actions_, do this if that.  
 * they're set on _buckets_ or _groups of objects_ (shared prefix/tag).  
 There are 2 types of actions:  
    * _Transition_ - Can be changed of tier automatically after some actions ( after 30 days without being accesed for example). What I'm understanding is you could actually create a intelligent-tiering (manually) or also it could bee also seen as a limited intelligent tiering)    
       * ![Transation](https://user-images.githubusercontent.com/31637504/188359603-9aa7b465-ac57-4f22-8cfd-a474e0147128.png)  
       * LIMITATIONS TO TAKE INTO CONSIDERATION.  
       * If on s3 standard there is a minimum of 30 days before transitioning the object into s3-SIA or s3-OZIA.  
       * Same but for going into _glacier classes_, there needs to be an additional 30 days on the SIA, OZIA to transition. (if you create a new rule this isn't the case but if everything is delcared in 1 single rule, this limitations apply.)  
    * _Expiration_ - Can delete or modify the object, also after certain amount of time.  
## s3 Replication  
 The Replication configuration is all made on the Source bucket. Then the service will use a IAM Role to make the necessary actions and the transportition will be encrypted via SSL.  
 There are 2 types:  
 1. _Cross-Region Replication_ **(CRR)**  
 2. _Same-Region Replication_ **(SRR)**  
 Both of this types are very similiar configuration wise, the only difference is when the buckets are on different AWS ACCOUNTS; those need extra configuration _(a bucket/resource policy which gives trust to the source IAM Role to take acction into the Destionation account.)  
 **Options**:  
    * copy _all objects_ or a _subset_ of objects in the bucket.  
    * _Storage Class_ - default is to maintain the same **SC**.  
    * _Ownership_ - default is the source account. (no prb when the buckets are owned by te same account OJO!)  
    * _Replication Time Control_ (RTC) - Garanteed level of predictibility adding visual monitoring. It adds an SLA(ServiceLevelAgreement) of 15 minutes.  
 * _**CONSIDERATIONS FOR EXAM!**_  
    * _Not retroactive_ & versioning needs to be **ON**.  
       * _Not retroactive_ means if the bucket has already objects in it they'll not be copied if not specified manually.  
    * _One-way Replication_ always from _source_ to _destination_.  
    * Can replicate: unencrypted, SSE-S3 & SSE-KMS (this last one needs extra config) data but it cant replicate SSE-C because s3 is not in possesion of the keys.  
    * Maybe obvious but, bucket owner NEEDS permissions to objects.  
    * NO _system events_ (if for example changes made by lifeCylce Conf), _glacier_ or _glacier deep archive_.  AND **NO DELETES!!**  
 _Why use replicatoin?_  
    * on SRR - is for logs Aggregation.  
    * on SRR - PROD and TEST syncronization.  
    * SRR - Resilience with strict sovereignty (some industries are pretty restreined so if for example theres an audit account, this could be a solution).  
    * CRR - Global Resilience Improvement; aide if errors/problems occur. 
    * CRR - Reduce Latency.  
 ## s3 Presigned URLs  
 A way to give a person/applicatoin access to object inside bucket using **your** credentials in a secure way.  
 Process:  
 1. Generate presignedURL (the owner/account will make the request)
    * The request needs to be authenticated & authorized.  
    * Bucket where the permission will be granted.  
    * Date when the URL will expire.  
 2. AWS reponds with the generated _presignedURL_ encodig the details in it.  
 3. The creator shared the _presignedURL_ with whomever he wants.  
 4. The unauthenticated actor uses the URL.  
 ### Exam TIPS  
 * A user can create an URL for an object he has **_no access to_** (by relation, the URL will not be able to access the resource/object)  
 * The URL will match the permissions fo the identity that generated it.  
 * Acces denied could be = never had access, URL has already expired.  
 * **DONT GENERATE WITH AN IAM ROLE** Sometimes the temporary credentials of a role are shorter than the preSignedURL. it could make the URL stop working.  
 ## s3 Select & Glacier Select  
 Functionality to retrieve part of an object instead of a complete one by using SQL-like statements.  
 File formats where this can be possible are, but not exclusively:  
 * CSV  
 * JSON  
 * Parquet  
 * BZIP2 Compression  
    * CSV  
    * JSON  
 The principal functionallity is filtering the data INSIDE the s3 servers, achieving more speed and reducing costs (traffic is lowered).  
 ## s3 Events Notifications  
 **Notifications** generated when events occur in a bucket:  
    * Object _Created_ (PUT, POST, COPY, CompleteMultiPardUpload)  
    * Object _Delete_ (Delete, DeleteMarkerCreated)  
    * Object _Restore_ (Post(INITIATED), Completed) - i.e. Retrieving from archive.  
    * _Replication_ (OperationMissedTHreshold, OperationReplicatedAfterThreshold, OperationNotTracked, OperationFailedReplication.)  
 This notifications can be delivered to _SNS_, _SQS_ & _Lambda Functions_ having the possibilite to trigger _Event driven Proceses_.  
 **_EventBridge_** is the "replacement" of this OLD service where it supports more types of events and more services to connect to.  
 ## s3 Access Logs  
 Gives detailed information of all access actions made into the sourceBucket. Keep in mind this is a BEST EFFORTS log delivery; the logs will arrive to the Target Bucket within a few hours.  
 To enable/make work this feature, this are the steps to follow:  
 1. Enable Logging on the bucket where yo want to revieve the _Access loggings_ via console UI or _PUT Buckt Logging_ via CLI 
 2. An s3 Log Delivery Group is the service which reads and transmits the logs to the TARGET BUCKET.  
 3. Create a Bucket ACL to allow access to _s3 Log Delivery Group_.  
 **LOGFILEs** consis of Log records which are:  
    * New-line delimited.  
    * Attributes are space-delimited.  
 ## VPC Sizing & Structure  
 Considerate the following when planning/creating our VPC;  
 * Size of the VPC  
    * Limits on CIDR - minimum /28 mask (16 IPs)  
    * maximum /16 (65536 IPs)  
 * Are there ane Networks **we can't use**?  
    * if other CIDRS are already in place, ignore them. Overlapping of CIDR can be very messy.  
 * Ranges of other VPCs, Cloud, On-premises, & other vendors  
    * A tip is to think in how manny Regions will the app be present.  
       * Reserve 2+ networks per region per account.  
   * Assume the worse.  
 * Try to think _scalable_ always, mindful with the future.  
 * VPC **Structure** - Where the application will have Tiers (different parts of app (web, app, db)) & resilieny Zones (Availability Zones).  
 ## Custom VPCs  
 * _Custom VPCs_ are Regional Resiliant and Regional isolated.  
 * Can create isolated networks, if wanted there can be more than 1 network in one Region.  
 * I/O is completely desactivated unless exmplicit condiguration.  
    * It VPC has also blast Radious.  
 * We can say they're the contrary of the default VPC:  
    * Flexible configuration.  
 * _Hybrid Netowrking_: It can be configured to interconnect with other cloud vendors as well as on-premises.  
 * When creating the VPC you can decide if creating it on **shared** or **dedicated** HW. PAY ATTENTION TO THIS!  
    * _Default_ - It goes PER RESOURCE created inside the VPC.  
    * _Dedicated Tenancy_ - Everything goes to dedicated HW, pay attention (it has premium payment).  
 * Uses IPv4 Private CIDR Blocks & Public IPs.  
 * Has 1 Primary Private IPv4 CIDR Block.  
    * minimum /28 subnet (16 IPs).  
    * maximum /16 subnet (65536 IP).  
 * Has a soft limit (can be extended by contacting support) for seconday IPv4 Blocks.  
 * Can use also IPv6 CIDR block by adding a /56 subnet mask.  
 * **DNS in a VPC**  
    * Provided by R53  
    * VPC **_Base IP +2_** Address,  
       * The DNS address will be: **10.10.0.2** if, for example, the VPCs address is 10.10.0.0.  
    * **_enableDnsHostnames_** - gives instances DNS Names. (public)  
    * **_enableDnsSupport_** - Enables DNS resolution in VPC.  
 ### VPC Subnets  
 * AZ Resilient.  
 * a subnetwork of a VPC _within a particular AZ_  
    * Can never be changed.  
    * Can never be in more than 1 AZ.  
    * There can be more than 1 Subnet per AZ though.  
 * IPv4 CIDR is a subset of the VPC CIDR (subnetting...).  
    * There are 5 Reserved IP by subnet.  
       * **Network Address**  
       * **Network +1** - VPC Router.  
       * **Netowrk +2** - Reserved [DNS]  
       * **Network +3** - Reserved Future Use  
       * **Broadcast Address** is locked, eventhough it cannot be used in VPCs.  
 * For every VPC there is a DHCP Option Set. [They cannot be changed after being configured].  
 ## VPC Routing & Internet Gateway  
 ### VPC Router  
 * Highly available.  
    * Works on every AZ that the VPC uses.  
 * Present on every VPC.  
    * It has an address on every subnet present (_network+1_ address).  
 * You can create a route table and associate it to a subnet.  
    * A subnet can only have 1 _route table_ associated.  
    * If the the subnet has no specific _route table_ the MAIN one will be used.  
       * The _MAIN route table_ can be associated with many subnets.  
 ### Internet Gateway (IGW)  
 **Region Resilient** attached to a VPC.  
 * 1 VPC can have 0 or 1 IGW.  
 * Can create IGW but not link it to any VPC, once it's related you cannot link it to another VPC.  
 * The IGW can connect the VPC to the _AWS Public Zone_ or to the _Internet_.  
 To create a public VPC:  
    1. Create IGW.  
    2. Atach IGW to VPC.  
    3. Create custom RT.  
    4. Associate RT to VPC.  
    5. Create default Routes onto IGW.  
    6. Configure Subnet to allocate IPv4 addresses (optionall IPv6) by default.  
 #### PD - BASTION HOST/JUMPBOX  
 Bastion Host = Jumpbox. It's an instance in a public subnet where incoming _MANAGEMENT_ connections arrive to have access to internal VPC Resources. As highlithed before thery're used to administer/manage private services/resources on an internal VPC.  
 
 ## _Stateful_ vs _Stateless_ Firewalls  
 _ephemeral_ = Temporary (used when client chooses a _ehpemeral_ port to create a TCP/IP connection to a server.)  
 * _**StateLess**_ 
    * Doesn't understand the state of connections - it sees the request and response of the connections as completely independent. You gotta create rules for every independent request/response and as inbound/outbound.  
    * tip - Request will always have a well-known port. Response will be to an ephimeral port. This could be complicated on stateless Firewalls, you can see why. 
 * **_StateFull _**  
 Intelligent enough to identify the response of a given request. It can "group" the request/response relation of a conversation between servers. It reduces overhead on rules.  
 ## Network Access Control Lists (NACL)  
 **STATELESS**. A traditional firewall available within AWS VPCs. They affect all packets going _inbound/outbound_ of the VPC but not internal traffic. The rule architecture is DENY ALL and EXPLICIT ALLOW/DENY based on a match starting from UP to bottom.  
    * Matches could be : 
       * DST IP  
       * DST PORT  
       * PROTOCOL  
 A _default NACL_ is created always after creating a VPC. It is an ALLOW ALL for inbound/outbound. If creating a _Custom VPC_ it will will DENY ALL by default.  
NACLs CANNOT be assigned to AWS resources, ONLY SUBNETS.  
Can be used together with Security Groups to add explicit DENY.  
## VPC Security Groups (SG)  
**STATEFUL** - if you allow a request, the response will be automatically allowed. 
Be aware, in **SG** there is NO EXPLICIT DENY, you cannot block a specific BAD ACTOR. Because of this limitation we use NACLs in conjutions with SGs.  
* ATTENTION - SGs are attached to an Elastic **Network Interface** (ENI) NOT INSTANCES. The interface might be seen as if you're attaching it to an instance but what it's really happening is, the SG will be attached to the primaryNetworkInterface of that instance.  
*Unique features:  
   * Remember, they cannot block specific traffic. If there's a rule allowing traffic into https, if there's a bad actor you cannot specifically block its ip with SGs.  
   * _Logical References_: You can reference as Source of a SG Rule a _SG_. So every server/client that's associated to the security group mentioned in the rule will be accepted traffic. Very powerful feature making easier security administration. I can see it as a way of compartelizing the sources (due to the limitation of not having EXPLICIT DENYs, but with the limitation of only being inter-subnetting traffic( or can you have publicTraffic associated to a security group? TO SEE...).  
      * _Self References_: A SG can _self-reference_ itself to allow traffic between all servers associated to the SG. All servers associated to that SG will be able to communicate between all the members of the SG.  
## NAT & NAT Gateway  
Network Address Translation.  
Features:  
* _IP Masquerading_ (what the mayority of people think NAT is (but only is 1 feature)) - hiding CIDR Blocks behind one IP.  
   * It gave PRivate CIDR range **outgoing** internet* access.  
   _Traffic flow_:  
      1. Source client (inside subnet) sends a request through its default routning record to a NAT GATEWAY.  
      2. The NAT GATEWAY job is to save a record of the src IP and translate the request to having its own IP and transfers it to the Internet Gateway via the VPC Router.  
      3. The Internet Gateway gives the packet a public ip and sends it to the internet.  
      4. The response is the same process but backwards...  
* The NAT Gateway needs to run from a _Public Subnet_.  
* Uses Elastic IPs (Static IPv4 Public).  
* AZ Resilient Service (High-Availability in AZ).  
   * To have _Region Resiliency_ add 1 natGateway on every AZ.  
* Managed Service.  
   * Charged Based on number of NATGateway (& another on traffic).  
### NAT Instance vs NAT Gateway  
 Before the **NAT Gateway** was an _EC2 Instance_ who worked as the NATting device.  
 NOTE: Default config on instances will drop all packets that are not source or destination of itsel, so if wanted to use the ancient version (_NAT Instance_) you need to disable **Source/Destination Checks** from UI/CLI.  
 * **NAT Gateway** is a much better option for almost every scenario; it scales better, has higher availability & is more customizable. BUT IT DOESN'T OFFER FREE TIER.  
 * **NAT Gateway CANNOT** be used as bastion host or as PORT FORWARDING. Its a managed Service.  
 * SECURITY  
    * _NAT Instance_: Due to being an _EC2 Instance_ ACLs or Security Groups can be used to manage security.  
    * **NAT Gateway**: Don't support Security Groups, can only use NACLs. <-EXAM !  
 * What about IPv6?  
 NAT is not required on IPv6, IT WONT WORK !  
 # EC2  
 Remember this is an IaaS.  
 ## Virtualization 101  
 Proces of running more than 1 OS on a single hardware (server).  
 A computer architecture has something called _kernel_; this is a gateway/bridge thats the one who's capable of ineracting with the HW. If any part of the computer attempted to make a _PRIVILEGED CALL_ the system would crash.  
 When Virtualizaion was created, this issue was solved but via Software (transparent to the Kernel) making it very inefitient:  
 * EMULATED Virtualization:  
    * Instead of the OS after the Kernel "layer" there was a new Layer called (HyperVisor). On top of it there'll be VMs who would think they where "real" being emulated by the HyperVisor.  
    * _Binary Translation_: Translation made between _privilege calls_ from guestVMs into HyperV. The HyperV intercepts all Guests' _privilege calls_ and makes the translation via software.   
    * _Para-Virtualization_: Only works on a small part of OS that can be modified (i.e. Linux). _Privileged Calls_ are modified onto being **HyperCalls**. To achieve this behaviour the source code needs to be modified specifically to the hyperVisor who'll be managing the Guest VMs.  
       * This solution made HyperVisors **ALMOST** virtualization Aware, but there were still software processes.  
    * _Hardware Assisted Virtualization_: Virtualization up to the level of HW. The CPU itself knows there are Virtualization.  
       * The CPU traps guest calls into a specific "place" which it is expecting. At a higher level everything is the same; guest VMs still think they're real. The CPU is the one that catches and sends the _privileged calls_ into the HyperVisor and he's the one sending the info into the kernel. The problem with this solution was all I/O proceses (writing/reading and network traffic) where still pretty demanding to the CPU.  
    * _SingleRoute I/O Virtualization_ (SR-IOV) - All devices (including network cards, disks) are aware of virtualization. Allows for example the network card to pressent itself as new diff cards. on AWS it is called **_Enhanced Networking_**.  
 ## EC2 Architecture  
 * Virtual Machine [OS + Resources].  
 * They're run on EC2 Hosts; Physical Hardware managed by AWS.  
    * _Shared Hosts_: You pay for only the instance used on a HW that other AWS Accounts will also use. You have no access to the host or any other instance that doesn't belong to you.  
       * Ways an EC2 might change HW when on _Shared Host_.  
          1. Host is pout on maintenance by AWS.  
          2. EC2 instance is stopped & started (different from a reboot).  
             * A reboot will not change Host.  
    * _Dedicated Hosts_: Pay entire host and is not shared with no other AWS Account but you. You're paying the entire host instead of only the instance.  
 * AZ Resilient. - **They only RUN on 1 AZ!**  
    *If AZ fails, Host fails, Instance Fails...  
 * _Storage on EC2_  
    * _Instanec Store_: Local Storage attached to the EC2, if the _Instance Store_ is detached & attached to another instance, the data will be  **LOST**.  
    * _Elastic Block Storage: They also are **AZ Resilient**. Only instances in the same AZ can have access to this. This service lets you attach volumes who are also limited to the AZ.  
 * **What's EC2 good for?**  
    * Traditional OS+Applicatoin compute.  
    * Long-Running Compute; there are services who'll be limited when staying always running. EC2 is the answer.  
    * _Server style applications_: An application who always listening  for incoming connections.  
    * Applications who needs _burst_ or _steady-state_ load.  
    * _Monolithic_ application stacks  
      * Single-tier application (evey component (DB, HTTP HOST, ...) are assembeled.  
   * _Migrated_ application workloads or _Disaster Recovery_.  
## EC2 Instance Types  
The biggest difference will be the _Raw_ Ammounts - CPU, MEM, Local Storage Capacity & Type.  
Also the _Resource Ratios_.  
   * Having bigger CPU but less MEM or viceversa...  
It'll influence System Architecture / Vendor - x64, arm64...  
There exist 5 main categories:  
* _General Purpose_ - Default - Diverse worloads, equal resource ratio.  
* _Compute Optimized - Media processing, HighPerformnceComputing (HPC), Scientific Modelling, gaming, Machine Learning.  
   * Offer latest high performance CPUs.  
   * Ratio is generally more charged into CPUs than memory.  
* _Memory Optimized_ - Imbberce of Compute, Processing large in-memory datasets, some database workloads.  
* _Accelerated Computing_ - Hardware dedicated GPU, field programable gate arrays (FPGAs) (This is like MicroProcessors I used in the HW class. Piece of hw supper customizable in a HW base level).  
* _Storage Optimized_ - Sequential and Random I/O, Scale-out transactional DBs, data warehousing, ElasticSearch, Analytics Workloads.  
### Decoding EC2 Types  
i.e. **_R5dn.8xlarge_** <- Instance Type.  
![Instance Type](https://user-images.githubusercontent.com/31637504/191413756-c595ea35-bc31-48ac-baed-2de085a7d30d.png)  
## Storage.  
### Storage Performance  
These 3 cannot exist in assolation, when the exist the 3 of them are present.  
* _I/O [Block] Size_ - Size of the wheels.  
* _I/O Operations per Second [IOPS]_ - Speed of the enginge of a car.  
* _Throughput_ - The max speed.  
The RPMs of an engine (power) is delivered to the wheels, depending on the size of the wheels you either can go faster or slower.  
   * I/O Size x IOPS = Throughput.  
### Elastic Block Store [EBS]  
_Block Storage_: Storage that can be addressed using **blockIds**. I takes raw physical disks and presents an allocation of those physical disks called **VOLUME**. 
* Volumes are RW using a block number on that volume. 
* Can be _encrypted_ using _KMS_.  
Instances see _block Devices_ and can create _FileSystems_ on the device [ext3,4,xfs].  
* Storage is *AZ RESILIENT.*  
EBS volumes can be attached to only 1 ec2 instance (or other service) over a storage network.  
   * Can be _detached_ & _reattached_, not linked to lifecyle of 1 instance.  [persistent]  
   * _Snapshots_ can be created and are saved into _*s3*_. This feature let you migrate info/volumes between AZs.  
      * When doing it you'll be creating a new disk on the new AZ based on the _Snapshot_.  
Can provision differente, types sizes & performace profiles:  
   * SSD  
   * SSD High-Performance  
   * etc.  
Billing = based on GB/month (in some cases _performance_ too).  
### EBS Volume Types  
#### General Purpose SSD  
**GP2** [first iteration ].  
Categories of the **GP2** ssd disk are as follows:  
* Volume size varies from 1 GB - 16 TB.  
* I/O opperations:  
   * The architecture is based on _**Credits**_, more specifically, it's created with a finite Credit allocation. Thinking of it as a _bucket_.The bucket is being refilled of credits periodically on a fixed rate depending on its size.  
      * AN I/O Credit - 16 KB. Assuming then an IOP is 1 operation of a chunk of 16KB per second.  
      * 1 IOPS = 1 Credit  
      * 1 I/O 'bucket' has a capaticy of _5.4 million_ Credits.  
      * Fills at rate of _BaselinePerformance_  
         * By minimum (ignoring volume size) the refilling is 100 I/O Credits per second (Cps). 
         * Beyond the this 100Cps the volume gets refilled 3 Cps per GB of volume size = _Baseline Performance_.  
      * Has a maximum of 3k IOPS by _depleting_ the bucket.  
         * 39 minutes @ 3k IOPS will completely deplete the bucket _if it wasn't being refilled_.  
            * GREAT for _boots_ and _initial workloads_.  
   * When volumes are larger than 1TB the arch changes. 
      * I/O Credits are not longer used.  
      * Volumes always _achieve Baseline_.  
      * max of 16k IPOS per second.  
 **GP3**  
 Is also SSD based but the credit Architecture is not longer present. Can be thinked about as being the _KID_ of **_GP2 & IO1_**. The new arch is:  
 * 3k IOPS at 125MiB/s - STANDARD  
    * Can be increased up to 16k IOPS or 1k MiB/s
 * GP3 is 20% cheaper thant GP2.  
 * _Throughput_ is 4x faster than GP2.  
    * 1k MiB/s vs 250 MiB/s.  
 #### Provisioned IOPS SSD [ io1/2 ]  
 Storage much more faster and _Consistent_ on low latency & jitter. The IOPS can be _independently_ of Size*.  
 Some stats:  
 * IO1/2:  
    * up to 64k IOPS per volume (being 4x GP2/3)  
    * up to 1k MB/s throughput.  
    * Size goes from 4GB - 16TB.  
    * \*io1 max of 50IOPS/GB.  
    * \*io2 max of 500IOPS/GB.  
 * IO2 BlockExpress:  
    * 256k IPOS per volume.  
    * 4k MB/s throughput.  
    * Size goes from 4GB - 64TB.  
    *  \*BlockExpress max of 1000IOPS/GB
 There is also another constraint - **Per instance Perfomance Limit**  
 To arrive to this limit you'll need more than 1 volume at highest levels. The values are:  
    * io1 - 260k IOPS & 7.5k MB/s  
    * io2 - 160k IOPS & 4.75k MB/s  
    * BlockExpress - 260k IOPS & 7.k MB/s  
    
