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
 
 
 
 
        
