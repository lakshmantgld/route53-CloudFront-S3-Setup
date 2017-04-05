# Route53-CloudFront-S3-Setup
- This repo is aimed to list out the steps for setting up a Highly Available WebApp using Route53, CloudFront and S3.
- Listing out the best practices like the optimal TTL(time to live), gzip, SSL implementation, automating invalidation requests and so on.

### Technical Architecture:
![Architecture diagram](https://raw.githubusercontent.com/lakshmantgld/route53-CloudFront-S3-Setup/master/readmeFiles/architecture.png)

## Highly Available Web App:
Since setting up of each service requires a brief description, I have divided the instructions into three sections namely **Hosting WebApp in S3**, **Caching using CloudFront** and **Routing using Route53**. Each section contains the general steps, best practices and other miscellaneous things.

### Hosting WebApp in S3:
**Amazon S3** is storage for the Internet. It has a simple web services interface that you can use to store and retrieve any amount of data, at any time, from anywhere on the web. It gives any developer access to the same highly scalable, reliable, fast, inexpensive data storage infrastructure that Amazon uses to run its own global network of web sites.

1. [Deploying React App / SPA in S3](https://github.com/lakshmantgld/route53-CloudFront-S3-Setup/master/readmeFiles/s3Setup.md).
