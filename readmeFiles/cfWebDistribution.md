## Setting up WebDistribution with S3

1. Navigate to **Amazon AWS** -> **CloudFront** -> **Create Distribution**
2. Choose **Web** since we are going to deploy web app.
3. The long form appears and this looks daunting at the first site. Lot of default options is enough for setting up cloudFront. Lets look at the default options in the [Best Practices section](https://github.com/lakshmantgld/route53-CloudFront-S3-Setup/blob/master/readmeFiles/cfBestPractices.md).
4. Copy the **S3 endpoint** and paste it in **Origin Domain Name**.
5. Leave the default options under the **Cache Behavior Settings**.
6. Under **Distribution Settings**, choose the necessary **Price Class** depending upon your use case and your budget.
7. Since we have chose **Both HTTP & HTTPS** option in the above section, we do not need to mind about **SSL Certificate** for now.
8. The other options can be left with default choices itself. Finally, click **Create Distribution** button.

This will create our CloudFront distribution. It will take around 15-20 minutes to deploy this distribution to all the Edge Locations in the world. Please not that any future settings can also take the same amount of time. So, be cautious about the cloudFront settings.

Once, the status has changed to **Deployed**, access the cloudFront Domain Name. This should render your app deployed in S3. Next, lets see [How to setup SSL for CloudFront](https://github.com/lakshmantgld/route53-CloudFront-S3-Setup/blob/master/readmeFiles/SSLForCF.md).
