## Setting up Route53 with CloudFront:

Assuming that you have deployed your SPA app to S3 and integrated that with cloudFront. At this point, you will able to serve your application in a much faster way using cloudFront's edge locations. If you have a custom domain name, say **lakshman.com**, you have to integrate the domain name with your cloudFront distribution. This file is going to walkthrough the above setup.

### Introduction to DNS:

DNS is used to convert human friendly domain names **lakshman.com** into an IP address (192.34.54.34). IP addresses can be either IPv4 or IPv6. DNS has lot of terminologies, let us look at each of those:

#### Top Level Domains (TLD):
If we look at common domain names such as ```google.com, bbc.co.uk, etc```., You will notice a string of characters separated by dots (periods). The last word in a domain name represents the **top level domain**. The second name in the domain name is known as a second level domain name. Examples of **TLD** are ```.com, .edu, .cloud```. These top level domain names are controlled by the **Internet Assigned Numbers Authority (IANA)**.

#### Domain Registrars:
Since all of the names in a given domain name have to be unique, there needs to be a way to organize this all, so that domain names are not duplicated. This is where domain registrars come in. A registrar is an authority that can assign domain names directly under one or more top-level domains. These domains are registered with **InterNIC**, a service of **ICANN**, which enforces uniqueness of domain names across the internet. Each domain name becomes registered in a central database known as the **WHOIS** database.

Now, you can register your domain even in **Route53**. But usually everyone prefers to register with a cost-effective registrar like **GoDaddy or NameCheap**.

#### DNS Record Types:

**SOA:** The administrator of the Zone namely the phone number, mailId of the domain owner. It also contains other information like TTL for name Servers(NS).

**NS:** Name Server records are used by Top Level Domain servers to direct the traffic to the content DNS server which contain the authoritative DNS records namely the **SOA**.

**Note:** If you have registered your domain in a different domain provider like **NameCheap**, first you have to create a **hosted zone in Route53** and then copy the name servers from **Route53** to NameCheap. This step is to direct the traffic from TLD to zone containing the authoritative records. Instructions on creation of **Route53** will be later seen in this readme.

**A:** A records are the fundamental type of DNS record that translates the name to equivalent IP address. A stands for Address record.

**CNAME:** CNAME stands for canonical record. It can be used to resolve one domain name to another. For example, you have **www.lakshman.com** that resolves to **lakshman.com**. I would remember as CNAME points to an A record.

**TTL:** This is not an record. It is time to live. The time that a DNS record is cached either on the resolving server or other Name servers. It is expressed in seconds. The maximum value can be 2 days. It is advised to have a large TTL so there can be lesser latencies.

**Alias Record:** These are created by AWS. basically it can be used only within AWS. Alias records are used to map resource record sets in your hosted Zone in Route53 to Elastic Load Balancers(ELB), CloudFront distributions or S3 buckets/websites.

**Alias** looks more like a CNAME record, both can map one DNS name (lakshman.com) to another target DNS name (elb.amazonaws.com). The **Main Difference:** A **CNAME** can't be used for naked domain name (lakshman.com). CNAME can point to lakshman.com record, which must be an A record or Alias record. Naked domains are the names with just the domain name and the TLD. for eg: google.com and lakshman.com.

### Integrating Route53 with CloudFront distribution:

1. **AWS** -> **Route53** -> click **Hosted Zones** on the left side menu.
2. Click **Create Hosted Zone** button.
3. Enter your **Naked Domain Name** in **Domain Name** text box.
4. Select the type **Public Hosted Zone** and then click **Create** button.
5. Once it is created, you will see **NS** and **SOA** records auto-generated.
6. Copy the **NS** records and paste it in your domain registrar. So that the traffic from TLD will be routed straight to your hosted zone in Route53.
7. In order to create A record, click **Create Record Set**.
8. Leave the name textbox empty, as we first want to point the naked domain name to cloudFront. Let the type be **A-IPv4 address**. Now, select **Alias**, in **Alias Target**, enter your cloudFront domain url which is ******.cloudfront.net.
9. Leave the Routing policy to simple. Click **Save Record Set**. Now that you have created A record. Assuming the domain name is **lakshman.com**, it will route to your **CloudFront distribution**.
10. We need to create a CNAME record to point other sub-domains like ```www.lakshman.com``` to map to the created **A record**.
11. Click **Create Record Set**, enter * in name textbox, rightnow we do not have any other sub-domains, so all sub-domains have to point the A record. Select **CNAME** from Type. In value, type the A record, in our case it will be **lakshman.com**. Click **Save Record Set**. Now even **www.lakshman.com** will forward to **lakshman.com** which in-turn will forward to CloudFront distribution.

Thus, we have deployed our static website using Route53, CloudFront and S3. Follow the best practice like Gzip, Invalidation, TTL policies, SSL to get the best out of the above AWS services.
