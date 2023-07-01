# First-Time Setup
Once you hear the machine beep, it is time to open your browser to http://rim-server. Note that if the rim-server hostname doesn't automatically resolve, you'll need to follow the instructions in our [Troubleshooting Guide](./troubleshooting.md).
Follow the instructions presented by the setup wizard. When entering a hostname, be sure to enter a fully qualified domain name (FQDN)) if your server has a dns record. The hostname you enter in this setup screen will be what is embedded into your client installers. In addition, it defines the url that will be used when visiting your server's web management dashboard, as well as obtaining ssl certificates.
## SSL Certificate
You will have the option of either generating a free Letsencrypt certificate, self-signing, or uploading your own certificate from your certificate authority. Note that if you self-sign, you will need to manually trust https connections to your host.
## SMTP Setup
Enter the smtp credentials issued by your email provider. You are advised to use SMTP port 587 whenever possible.
## First-Time Login
Once setup is complete, you will be able to log into your account. Once you enter your email address, you will be sent an email containing a verification link. Once you click this link, you will be able to provide your name at which point your account will be created.