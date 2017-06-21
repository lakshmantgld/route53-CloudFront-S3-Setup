Name cheap offers mail hosting in three different plans like **Private**, **Business** and **Enterprise**. Here are the steps to create custom e-mail like `no-reply@example.com`.

1. Log into the **name cheap** account and make sure you login to the namecheap's domain owner's account. As mail hosting plans can be enabled only from domain owner's account.
2. Select any of the above mail hosting plans. Once selected, you will have the choice to create your **custom e-mail ID**.
3. The password for the custom mail will be mailed to domain owner's mail account.
4. In order to send/receive e-mails using the created custom mail, You have to make sure the **MX** and **TXT** records are set. These records have to be at the same place as your **NS** records exist. For eg: Even though I bought my domain from namecheap, the **DNS** is hosted in AWS's **Route53** service. So Route53 is the place where my **NS** record exists. So, you have to create a new MX and TXT record in Route53.
5. The values for the **MX** and **TXT** records are [here](https://www.namecheap.com/support/knowledgebase/article.aspx/1340).
6. Once they are updated, you are all set to send and receive e-mails using the custom mail domain.
7. Name cheap provides a webmail client called [privateemail](https://privateemail.com). You can login to web client and view/compose your mails.

This summarizes the custom mail creation. I have also attached the chat archives that I had with **namecheap** customer support for future reference. Here are the [document 1](https://s3-ap-northeast-1.amazonaws.com/nj2jp-technical-documents/Namecheap.pdf) and [document 2](https://s3-ap-northeast-1.amazonaws.com/nj2jp-technical-documents/%5BPrivate-Email%5DNamecheap.pdf).
