---
layout: post
title:  "aws developer associate test CodeDeploy quick note"
date:   2019-02-27 19:00:00 +0900
comments: true
tags:
- aws
- study note
---

# code deploy
integrate with CI/CD tools as well as config management tools `ansible`, `chef`, `puppet`

## Steps to deploy a project
<img src="/img/code_deploy.png">


## deploy methods
1. inplace
- as called `rolling update`
- stop the instance while updating and use other instances (capacity will be smaller)
- can be used for EC2, on-premise systems, not for lambda
- need redeploy for rollback


2. green/blue
- prepare new instances and switch traffic once deployment is done
- blue is is the active deployment, green is the new release
- can also be used for lambda

## appspec file to configure deployment
1. lambda deployment
- version
- resources (name and properties of lambda function)
- hooks (specify when should lambda function run)
  - BeforeAllowTraffic
  - AfterAllowTraffic

2. ec2 and on premises
- version
- os
- files (source and destination)
- hooks
  - ApplicationStop (Gracefully stio the app for the new verion)
  - DownloadBundle (CD agent copies revision files to a temporary location)
  - BeforeInstall (e.g backing up current revision, decrypting files)
  - Install (copy revision files from temp to correct location)
  - After install (e.g config tasks, change permission)
  - ApplicationStart
  - ValidateService (tests)
  - BeforeBlockTraffic (tasks before deregistering from load balancer)
  - BlockTraffic (deregister instances from load balancer)
  - AfterBlockTraffic (tasks after deregistering from load balancer)
