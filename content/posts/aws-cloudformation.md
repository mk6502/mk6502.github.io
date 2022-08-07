---
title: "AWS CloudFormation"
date: 2019-03-28T12:39:20-05:00
draft: false
---

If you're doing any production-level work in AWS, you should be using AWS CloudFormation. It's really easy to get started. Let's walk through the basics.

## Why use CloudFormation?
Here’s a common scenario: creating an EC2 instance and assigning an Elastic IP address. Let's say it's for a web server. Great! That's easy. Just spin up an EC2 instance. Choose the correct image, size, security groups, VPC, subnet, keypair, and so on. Then create and assign it an Elastic IP address. No problem!

Now deploy it in QA.

Then deploy it in production.

But production has different security groups. You should probably set up CloudWatch alerts in production too. All of this is getting expensive, so maybe we should turn off the development stack overnight. But at this point we don’t just have one EC2 instance — we also have RDS, some S3 buckets, DynamoDB, and so on. We’ll need all of that configured in each environment. It’s 6 months later now and we need to recreate everything in a different region — did you document how to set everything up?

CloudFormation takes care of all of that for you.

CloudFormation can provision, update, delete, and monitor changes in virtually any AWS service. You can make S3 buckets with specific policies, make IAM roles allowed to access those buckets, spin up a Redshift cluster with that role attached, and so on. You can even create EC2 instances with Elastic IP addresses attached to them (and the VPC, security groups, and subnet associated with that instance).

## An Example

```yaml
AWSTemplateFormatVersion: 2010-09-09
Description: Create an EC2 instance.
Parameters: 
  InstanceNameParameter: 
    Type: String
    Description: Name of the instance.
Resources:
  EC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-0123456789abcdef0
      KeyName: mykeypair
      InstanceType: t3.nano
      SecurityGroupIds:
        - sg-0123456789abcdef0
      SubnetId: subnet-01234567
      BlockDeviceMappings:
        -
          DeviceName: /dev/xvda
          Ebs:
            VolumeSize: 20
      Tags:
        - {Key: "Name", Value: !Ref InstanceNameParameter}
  ElasticIP:
    Type: AWS::EC2::EIP
    Properties:
      Domain: vpc
      InstanceId: !Ref EC2Instance
Outputs:
  ElasticIPAddr:
    Value: !Ref ElasticIP
```

That looks like a lot and the formatting takes some getting used to. But at this point, you can go right into the AWS Console and upload that CloudFormation template and have an EC2 instance and IP address created and set up in a few seconds. JSON is also a supported template format.

## Drift Detection
This is a really cool feature. Let's say your stack has been created and now it's a few months later and someone changed some settings. AWS CloudFormation can detect when changes are made outside of CloudFormation and alert you.

## Updates and Deleting a Stack
You guessed it — if you update your CloudFormation template, AWS will intelligently figure out what it needs to do to update your stack.

Here’s an example — let's say we need to increase the size of the disk on that EC2 instance. We would simply change the value in the template and use CloudFormation to update the stack. AWS would create a new instance with a larger disk and attach the Elastic IP address to the new instance automatically. The old EC2 instance would then be terminated.

### CloudFormation
The best part is that templates are easy to reuse and work with most AWS services, not just EC2. There's a slight learning curve, but the benefits are worth it.