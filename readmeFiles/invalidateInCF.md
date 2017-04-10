## Invalidation in CloudFront
Invalidating is removing objects from the **CloudFront edge caches before it expires**. Best **use-case:** We have our S3 bucket as our origin. When we upload new version of files, we want our CloudFront to serve our customers with the latest files. Invalidation helps to forcefully remove the old objects from the CloudFront edge cache and replace it with latest files.

To Invalidate objects, you can specify wither the path for the individual object or the whole directory path using the **wildcards ***.

This Invalidation by path can be specified either through AWS console or API/SDK or CLI. Since we want to automate this step, we are going to use AWS CLI, so we can add it to NPM/Yarn scripts. The command to invalidate using AWS CLI is:

```bash
aws cloudfront create-distribution --distribution-id=<YOUR-DISTRIBUTION-ID> --paths '/*'
```

The above command will remove all the objects from CloudFront edge cache. This is handy and can be added to your build script in npm, you can execute this command, when you add new files to your S3 bucket.
