---
layout: post
title:  "aws developer associate test IAM quick note"
date:   2019-01-11 23:30:09 +0900
comments: true
tags:
- aws
- study note
---

# iam
- components: `user, group, role, policy`
- user has many groups
- role is defined for aws resources
- policy can be used to define `role, user, group` access
- policy is a json file defining one or more permissions

## create a user
1. console
- need user name and password
- can reqeust to reset password

2. programtic
- access key id, access key secret
- only able to see the secret when creating the user, need to download the csv for further reference

## create a role
1. can create from a aws resource
- e.g EC2 giving s3 read permission, any instance has this role attached can access S3

## exam tips
- iam is global, does not relate to region
- root account is the account first created, shouldn't use this account normally
- always use MFA on root account






