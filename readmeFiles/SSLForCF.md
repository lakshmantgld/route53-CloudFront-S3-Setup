## Setting up SSL for CloudFront

Setting up SSL for cloudFront is quite an easy step. There are many SSL options available. If you are going to give your end users the cloudFront domain name say **xxxxxx.cloudfront.net**, it is going to be a straightForward approach else, If you have your domain name, some steps have to be followed:

#### Using cloudFront domain Name for SSL:
To enable SSL for default cloudFront domain name, here are the steps:
1. Click your **CloudFront Id** under the distributions section.
2. Select the **Behaviors** tab and click **Edit** button.
3. Now, you will be seeing the **Default Cache Behavior Settings**. Under that, in **Viewer Protocol Policy**, toggle the option **Redirect HTTP to HTTPS** from **HTTP and HTTPS**. This option will redirect the users from HTTP to HTTPS. You can also choose **HTTPS only**. But this option does not work if, you are using a custom domain name.
