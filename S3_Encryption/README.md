# S3 Bucket Autoremediation to Enforce Encryption

The purpose of this template is to build AWS resources that automatically encrypt S3 buckets when they are made without encryption.

The template builds an Amazon EventBridge rule and an AWS Lambda function. 

The rule monitors for the creation of a bucket, using the API call of `CreateBucket`. When a bucket is created, a Lambda function is triggered. The function makes an api call of `GetBucketEncryption` to determine if the bucket has encryption.

As a side note, it may be worth noting that a `CreateBucket` API call does not include information about whether the bucket is encrypted or not. A `GetBucketEncryption` API call is used instead to check the bucket's encryption status. If a bucket is not encrypted, for boto3, S3 will return a status code as an exception. This is logged so the function's Amazon CloudWatch LogGroup picks it up. (More information on this behavior here on [GitHub](https://github.com/boto/boto3/issues/1899)).


If the bucket has encryption, nothing will happen except it will log the outcome of the api call to CloudWatch.

If the bucket was not encrypted when it was created, the lambda will enable default encryption with an Amazon S3 master-key (SSE-S3).

## Diagram

Pending

## How to Deploy

Pending
