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
  Objects or docs used to allow or deny access to AWS Services when attached to an Identity type ( user, group, role)
  
 
  
