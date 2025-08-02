---
####  You also need to create TLS certificate
1. Go to **AWS Certificate Manager (ACM)**
2. Click **Request**
3. Under **Certificate type**, select **Request a public certificate** and then click **Next**
4. In **Fully qualified domain name**, enter your domain name. In my case, it's **mystatsolve.click**. (you need to use your domain instead of mystatsolve.click )
5. Leave all other settings as default and click **Request**
6. Go to **Certificates** and click on the certificate that has your domain name.
7. In the **Domains**, click **Create records in Route 53** and then click **Create records** to add CNAME of your certificate in your Route 53.
8. Wait untill the validation completing and proceed to setup your cloudfront distribution

