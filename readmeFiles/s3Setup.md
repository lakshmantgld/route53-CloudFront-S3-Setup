## Deploying React App / SPA in S3:

### Creation of S3 Bucket:
To upload our data (index.html, bundle.js, images), we first create a bucket in one of the AWS Regions. You can then upload any number of objects to the bucket.

1. Login to **AWS console** and choose **Asia Pacific (Tokyo)** region in the right corner of the screen.
2. Look for **S3** service under **Storage** section.
3. Click **Create Bucket** button in the left corner.
4. Enter the bucket name and select **Tokyo** as the region. The bucket name is unique to that region.
5. Hold on for few seconds, a bucket with our specified name will be created.
6. S3 is a **storage service**, but we are going to use it as our **Static website server**. So, here are the steps to configure it:
  1. Once the bucket is created, you will be in to that bucket page. Click the **Properties** button in the right corner.
  2. From the list of settings, click **Static Website Hosting** and toggle **Enable website hosting**.
  3. By default, files in S3 are accessible only to AWS user. Since, we are going to use it as a public website, we need to relieve some permissions.
  4. From the list of settings, click **Permissions** and click **Add bucket policy**.
  5. In the **dialog for policy**, add the JSON as shown below after replacing the ```<bucket-name>``` with our bucket name:
  ```js
  {
  	"Version": "2008-10-17",
  	"Statement": [
  		{
  			"Sid": "AddPerm",
  			"Effect": "Allow",
  			"Principal": {
  				"AWS": "*"
  			},
  			"Action": "s3:GetObject",
  			"Resource": "arn:aws:s3:::<bucket-name>/*"
  		}
  	]
  }  
  ```

This makes the **static website** to be publicly accessible by all users. Navigating to the **endpoint** in the static website property will render our website in the browser.

Now that we have created S3 bucket to host our files, lets see the setup to [automate the deployment of build files to S3](https://github.com/lakshmantgld/route53-CloudFront-S3-Setup/blob/master/readmeFiles/s3Setup.md).
