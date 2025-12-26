# AWS Security - S3cret Santa

# Task 1: Introduction

### Answer the questions below

Run `aws sts get-caller-identity`. What is the number shown for the "Account" parameter?

> `123456789012`
> 

```bash

ubuntu@tryhackme:~$ aws --version
aws-cli/2.32.3 Python/3.13.9 Linux/6.8.0-1016-aws exe/x86_64.ubuntu.24

ubuntu@tryhackme:~$ aws sts get-caller-identity
{
    "UserId": "bksptqo8e36yz3fz1ac9",
    "Account": "123456789012",
    "Arn": "arn:aws:iam::123456789012:user/sir.carrotbane"
```

<aside>
💡

Amazon Security Token Service (STS) allows us to utilise the credentials of a user that we have saved during our AWS CLI configuration. We can use the `get-caller-identity` call to retrieve information about the user we have configured for the AWS CLI.

</aside>

# Task 2: IAM: Users, Roles, Groups and Policies

### Answer the questions below

What IAM component is used to describe the permissions to be assigned to a user or a group?

> `policy`
> 

<aside>
💡

Access provided to any user, group or role is controlled through IAM policies. A policy is a JSON document that defines the following:

- What action is allowed (Action)
- On which resources (Resource)
- Under which conditions (Condition)
- For whom (Principal)
</aside>

# Task 3: Practical: Enumerating a User's Permissions

### Answer the questions below

What is the name of the policy assigned to `sir.carrotbane`?

> `SirCarrotbanePolicy`
> 

```bash
##List users
ubuntu@tryhackme:~$ aws iam list-users
{
    "Users": [
        {
            "Path": "/",
            "UserName": "sir.carrotbane",
            "UserId": "bksptqo8e36yz3fz1ac9",
            "Arn": "arn:aws:iam::123456789012:user/sir.carrotbane",
            "CreateDate": "2025-12-26T07:19:32.662163+00:00"
        }
    ]
}
##List inline policies assigned to Sir Carrotbane
ubuntu@tryhackme:~$ aws iam list-user-policies --user-name sir.carrotbane

{
    "PolicyNames": [
        "SirCarrotbanePolicy"
    ]
}

## List attached policies assigned to Sir Carrotbane
ubuntu@tryhackme:~$ aws iam list-attached-user-policies --user-name sir.carrotbane

## Check if Sir Carrotbane is part of a group
ubuntu@tryhackme:~$ aws iam list-groups-for-user --user-name sir.carrotbane

## What permission does SirCarrotbanePolicy grants
ubuntu@tryhackme:~$ aws iam get-user-policy --policy-name SirCarrotbanePolicy --user-name sir.carrotbane

#Here we can see that sir.carrotbane can perform the sts:AssumeRole action.
```

# Task 4: Assuming Roles

### Answer the questions below

Apart from GetObject and ListBucket, what other action can be taken by assuming the bucketmaster role?

> **`ListAllMyBuckets`**
> 

```bash
## Lists all IAM roles in the AWS account
ubuntu@tryhackme:~$ aws iam list-roles
##There's a role named bucketmaster, and it can be assumed by sir.carrotbane

## Lists inline policies (hard-coded) attached directly to the role
ubuntu@tryhackme:~$ aws iam list-role-policies --role-name bucketmaster
## Bucketmaster

## Retrieves full policy document for a specific inline policy
ubuntu@tryhackme:~$ aws iam get-role-policy --role-name bucketmaster --policy-name BucketMasterPolicy
## 3 actions: s3:ListAllMyBuckets, s3:ListBucket, s3:GetObject
```

# Task 5

### Answer the questions below

What are the contents of the cloud_password.txt file?

> `THM{more_like_sir_cloudbane}`
> 

```bash
## Since our profile has permission to ListAllBuckets, we can list the available S3 buckets by running the following command:

ubuntu@tryhackme:~$ aws s3api list-buckets
## Found "easter-secrets-123145" bucket

ubuntu@tryhackme:~$ aws s3api list-objects --bucket easter-secrets-123145
## Listed "cloud_password.txt"

ubuntu@tryhackme:~$ aws s3api get-object --bucket easter-secrets-123145 --key cloud_password.txt cloud_password.txt
## Downloaded file

ubuntu@tryhackme:~$ cat cloud_password.txt
## Revealed TBFC cloud admin password
```

**S3 Commands Explained:**

- **`aws s3api list-buckets`** → Lists **all S3 buckets** in account (ListAllMyBuckets permission)
- **`aws s3api list-objects --bucket <name>`** → Lists **objects/files** in specific bucket (ListBucket permission)
- **`aws s3api get-object --bucket <name> --key <file> <local>`** → **Downloads** object from bucket to local machine (GetObject permission)