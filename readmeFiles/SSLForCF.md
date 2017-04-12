## Setting up SSL for CloudFront

Setting up SSL for cloudFront is quite an easy step. There are many SSL options available. If you are going to give your end users the cloudFront domain name say **xxxxxx.cloudfront.net**, it is going to be a straightForward approach else, If you want your own domain name, some extra steps have to be followed.

### SSL for default CloudFront domain name:
To enable SSL for default cloudFront domain name, here are the steps:
1. Click your **CloudFront Id** under the distributions section.
2. Select the **Behaviors** tab and click **Edit** button.
3. Now, you will be seeing the **Default Cache Behavior Settings**. Under that, in **Viewer Protocol Policy**, toggle the option **Redirect HTTP to HTTPS** from **HTTP and HTTPS**. This option will redirect the users from HTTP to HTTPS. You can also choose **HTTPS only**. But this option does not work if, you are using a custom domain name.
4. After doing the above step, scroll down and click **Yes, Edit**.
5. Then, navigate to **General Tab** and click **Edit**, you will be seeing the **Distribution Settings**, under that make sure that the **Default CloudFront certificate** is toggled. Now, when you use the **xxxxxx.cloudfront.net** in the browser, it automatically redirects from HTTP to HTTPS. or you can use **https://xxxxxx.cloudfront.net** itself directly in the browser. All your viewers can interact with your site in a secured way.

### SSL for custom domain name:
To enable SSL for custom domain name, there are two Custom SSL Client Support namely,

**1. Server Name Indication (SNI)** method and

**2. All Clients** method which is an expensive one(600$/month).

#### 1. Server Name Indication (SNI):
CloudFront serves your content over HTTPS only to clients that support SNI. Older browsers and other clients that do not support SNI can not access your content over HTTPS. But almost all browsers support SNI. This method does not incur any extra cost. Amazon can also get you a free SSL certificate for your custom domain. Here are the steps:

- Click your **CloudFront Id** under the distributions section.
- Select the **Behaviors** tab and click **Edit** button.
- Now, you will be seeing the **Default Cache Behavior Settings**. Under that, in **Viewer Protocol Policy**, toggle the option **Redirect HTTP to HTTPS** from **HTTP and HTTPS**. This option will redirect the users from HTTP to HTTPS. You can also choose **HTTPS only**. But this option does not work if, you are using a custom domain name.
- After doing the above step, scroll down and click **Yes, Edit**.
- Then, navigate to **General Tab** and click **Edit**, you will be seeing the **Distribution Settings**, toggle the **Custom SSL Certificate** instead of **Default CloudFront certificate**. Now, for this step you need a SSL certificate from a approved Certificate Authority. If you have already bought a certificate, you can import it using ACM service or you can get a free SSL certificate for your domain from ACM. Here is some information about that:

AWS provides a service called **ACM(AWS certificate management)** which gets us free SSL certificates, but it can be used only within the AWS. i.e those certificates can only be used in AWS infrastructure like CloudFront.

The process by which it gets the SSL certificate is, first we need to give the domain name, in our case (lakshman.com). Once, we give the domain name, it searches the WHOIS database, which contains the the information about owners of various domains.

In our case, it searches for the domain owner of lakshman. Usually domain owner's name, mail id and address are stored in that database. ACM gets those information and send a approval request mail to the domain owner. This step is made to check the authenticity of the domain owner. So that only domain owner can generate ssl certificate for their respective domains.

Once the owner approves, ACM provides us with a free SSL certificate. We can use that in CloudFront and make our website an HTTPS one.

- Under **Custom SSL Certificate**, import the certificate that Amazon has just generated for you.
- One final step, In the **Alternate Domain Names(CNAMEs)** section, enter the possible domain names in a comma separated form. In our case, it will be ```lakshman.com, *.lakshman.com```. The ***** is to mention the possible subdomains like ```www``` should also direct the CloudFront distribution.

But, the real domain records ```A & CNAME``` record for the domain will be created in the **Route53's** hosted zone. Look here for the [Route53 setup](https://github.com/lakshmantgld/route53-CloudFront-S3-Setup/blob/master/readmeFiles/route53Setup.md).
