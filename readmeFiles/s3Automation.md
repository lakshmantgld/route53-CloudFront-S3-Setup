## Automate deployment of static website files to S3



There are many ways to do the automation of **S3 deployment**. Here are the things I gathered:


**1. AWS SNS and Lambda:**


This process is useful, if you want to trigger any AWS services on github push. So, here is the process:


1. The github push triggers a message to SNS.
2. The Lambda which is subscribed to the SNS topic is invoked.
3. Inside the Lambda, I clone the github repository.
4. Use AWS's S3 SDK to upload the **build or dist** directory to your S3 bucket. Here is a high level architecture of the above process:

![s3AutomationUsingLambdaSNS](https://raw.githubusercontent.com/lakshmantgld/route53-CloudFront-S3-Setup/master/readmeFiles/s3AutomationUsingLambdaSNS.png)

The downside of this approach is cloning large repos takes time and Lambdas are billed per second. So, this may become expensive for large repos.


**2. Travis:**


Travis is known for its CI(continuous integration) library. A **.travis.yml** is essential for the integration process.


If you want to make some tests after the build and then on success, upload the files to S3. Then this approach will be the best way. Travis is free for open source projects.


The downside is, I could not find a way to isolate a directory from the repo and upload that specific directory alone.


**3. AWS cli:**

This is the cheapest and best way to upload the files to S3. I used this approach. I got this information from this [medium post][2].


Usually in react apps the **build scripts** are triggered by the **npm or yarn** written as scripts in the **package.json**. Here is the command for uploading the files to S3:


```aws s3 sync build/ s3://<bucket-name>```

I added this script as part of the build scripts in package.json. This was very handy and thus automated the manual process of uploading the files to S3.


  [2]: https://medium.com/@omgwtfmarc/deploying-create-react-app-to-s3-or-cloudfront-48dae4ce0af#.dhg6jyltq
