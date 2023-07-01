# First-Time Setup
Once you hear the machine beep, it is time to open your browser to http://rim-server. Note that if the rim-server hostname doesn't automatically resolve, you'll need to follow the instructions in our [Troubleshooting Guide](./troubleshooting.md).
Follow the instructions presented by the setup wizard. When entering a hostname, be sure to enter a fully qualified domain name (FQDN)) if your server has a dns record. This will be important when obtaining and/or uploading an SSL certificate.
## SSL Certificate
You will have the option of either generating a free Letsencrypt certificate, self-signing, or uploading your own certificate from your certificate authority. Note that if you self-sign, you will need to manually trust https connections to your host.