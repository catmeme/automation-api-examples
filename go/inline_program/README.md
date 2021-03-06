# Inline Program

This program demonstrates how use automation API with an `inline` Pulumi program. Unline traditional Pulumi programs, inline functions don't require a seperate package on disk, with a `main.go` and `Pulumi.yaml`. Inline programs are just functions, can can be authored in the same `main.go` or be imported from anther package. This example deploys an AWS S3 website, with all the context and deployment automation defined in a single file.

To run this example you'll need a few pre-reqs:
1. A Pulumi CLI installation ([v2.10.1](https://www.pulumi.com/docs/get-started/install/versions/) or later)
2. The AWS CLI, with appropriate credentials.

Running this program is just like any other Go program. No invocation through the Pulumi CLI required:

```shell
$ go run main.go
Created/Selected stack "dev"
Installing the AWS plugin
Successfully installed AWS plugin
Successfully set config
Starting refresh
Refresh succeeded!
Starting update
Updating (dev)

View Live: https://app.pulumi.com/EvanBoyle/inlineS3Project/dev/updates/22


 +  pulumi:pulumi:Stack inlineS3Project-dev creating 
 +  aws:s3:Bucket s3-website-bucket creating 
 +  aws:s3:Bucket s3-website-bucket created 
 +  aws:s3:BucketObject index creating 
 +  aws:s3:BucketPolicy bucketPolicy creating 
 +  aws:s3:BucketObject index created 
 +  aws:s3:BucketPolicy bucketPolicy created 
 +  pulumi:pulumi:Stack inlineS3Project-dev created 
 
Outputs:
    websiteUrl: "s3-website-bucket-bf7e357.s3-website-us-west-2.amazonaws.com"

Resources:
    + 4 created

Duration: 10s

Update succeeded!
URL: s3-website-bucket-bf7e357.s3-website-us-west-2.amazonaws.com
```

To destroy the stack when you're done, invoke the program with an additional `destroy` argument:

```shell
$ go run main.go destroy
Created/Selected stack "dev"
Installing the AWS plugin
Successfully installed AWS plugin
Successfully set config
Starting refresh
Refresh succeeded!
Starting stack destroy
Destroying (dev)

View Live: https://app.pulumi.com/EvanBoyle/inlineS3Project/dev/updates/24


 -  aws:s3:BucketPolicy bucketPolicy deleting 
 -  aws:s3:BucketObject index deleting 
 -  aws:s3:BucketObject index deleted 
 -  aws:s3:BucketPolicy bucketPolicy deleted 
 -  aws:s3:Bucket s3-website-bucket deleting 
 -  aws:s3:Bucket s3-website-bucket deleted 
 -  pulumi:pulumi:Stack inlineS3Project-dev deleting 
 -  pulumi:pulumi:Stack inlineS3Project-dev deleted 
 
Outputs:
  - websiteUrl: "s3-website-bucket-bf7e357.s3-website-us-west-2.amazonaws.com"

Resources:
    - 4 deleted

Duration: 3s

The resources in the stack have been deleted, but the history and configuration associated with the stack are still maintained. 
If you want to remove the stack completely, run 'pulumi stack rm dev'.
Stack successfully destroyed
```