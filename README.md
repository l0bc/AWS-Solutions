# AWS-Solutions


### Accounts
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

### Budgets
 * Very useful to trying to maintain into the freeTier. Go to budgets on account info.
 
 
 
### IAM BASICS
 Using limited access account ( create accounts for almost any service/user); grant ONLY permissions that the account needs, nothing more.
 Every AWS account has its own IAM DB but
  * It is a global resilience service: Data is replicated in all different regions. 
  
  IAM service has as much priviledge as root account. (stayed on min 3 )
  
