If we want to send e-mail from SES, we need a sender and a receiver e-mail address. Obviously, we can use any receiver e-mail address. But sender address has to be verified by SES before using it.

**SES** sender mail verification steps:
1. Select **SES** from **AWS console**. Select `N.Virginia` region, as `ap-northeast-1`(tokyo) does not support SES.
2. In the left, click **Email Addresses** under **Identity Management**.
3. You will see a blue color **Verify a New Email Address* button**.
4. Enter the e-mail address, that you need to verify. After that, Press **Verify this Email Address**.
5. So, We will be receiving an e-mail from SES in privateemail. Once approved there, we can use it as sender address in SES.
