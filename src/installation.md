# Installation
The Remote Incident Manager server is packaged as a stand-alone Windows application. While the below process assumes the presence of a Windows Server environment, the instructions will be more or less the same for a standard Windows 10 or 11 environment.

## Setup Process

The RIM server application is packaged as a self-contained MSI package. This server can be installed as the only resident server application on the machine, or work alongside any existing infrastructure through a reverse proxy. We will document the general process for setting up a reverse proxy through Internet Information Services (IIS). Unless otherwise noted, we will avoid specific mentions of the graphical user interface of IIS throughout these instructions. This will allow you to apply these instructions to whichever configuration method (GUI, CLI or web-based admin tool) you use throughout your organization.

### Prerequisits

Before installing the RIM server, it is strongly recommended to have a fully configured IIS infrastructure along with all related packages. In addition, the [Microsoft Visual C++ Redistributables](https://aka.ms/vs/17/release/vc_redist.x64.exe) are required for the RIM server to function.

#### Installing IIS and Additional Modules

1. Install the IIS role onto your server. In addition to the web management tools, http server, etc. make sure that the web sockets protocol module is queued for installation.
1. Install the [Application Request Routing (AAR)](https://www.iis.net/downloads/microsoft/application-request-routing) module, which will allow IIS to function as a reverse proxy.
1. Lastly, install the [URL Rewrite](https://www.iis.net/downloads/microsoft/url-rewrite) module.
<!-- end -->
Now that we have IIS installed, configuration of the reverse proxy can begin.

#### Enabling the Proxy within AAR

In the main server node, you will find an Application Request Routing Cache configuration. A Server Proxy Settings node is contained within. This is where you will go to enable the proxy function.

#### SSL Configuration

RIM does not manage the SSL certificate when running in reverse proxy mode. Instead, you will need to configure the SSL binding and associated certificate for your site in IIS. This can be done either on the default site, or by creating a new website. Be sure to enable https enforce once the ssl binding is configured.

#### Configuring the URL Rewrite Rules

The best way to configure URL rewrite is through a web.config file. In order for this to work, however, you must first add the `HTTP_X_FORWARDED_PROTO` variable to your server's allowed variables. Then, create a file in your webroot called web.config, and paste the following content:
```
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
        <rewrite>
            <rules>
                <rule name="ReverseProxyInboundRule1" stopProcessing="true">
                    <match url="(.*)" />
                    <action type="Rewrite" url="http://localhost:7460/{R:1}" />
                    <serverVariables>
                        <set name="HTTP_X_FORWARDED_PROTO" value="https" />
                    </serverVariables>
                </rule>
            </rules>
            <outboundRules>
                <rule name="ReverseProxyOutboundRule1" preCondition="ResponseIsHtml1">
                    <match filterByTags="A, Form, Img" pattern="^http(s)?://localhost:7460/(.*)" />
                    <action type="Rewrite" value="http{R:1}://domain.tld/{R:2}" />
                </rule>

                <preConditions>
                    <preCondition name="ResponseIsHtml1">
                        <add input="{RESPONSE_CONTENT_TYPE}" pattern="^text/html" />
                    </preCondition>
                </preConditions>
            </outboundRules>
        </rewrite>
        <httpErrors errorMode="DetailedLocalOnly" />
    </system.webServer>
</configuration>
```
Replace domain.tld with your real domain, then save the file. Restart IIS once this file has been saved.

### Installing the RIM Server

If you have set up a working reverse proxy, now is when you would install the RIM server package. Any references to a reverse proxy can be disregarded if it is not part of your configuration.  
The installation is a one-click silent install. Once the installation is finished, the server will start automatically. Note that unless you have set up a reverse proxy as described above, you will need to access the server on port 7460 for initial setup. Additionally, if you intend for your RIM infrastructure to be accessible via the live web, you will need to add your own https firewall rule, as IIS only opens port 80 by default. You do not, however, need to open port 7460.

### Updating the RIM Server

Updates must be installed manually. Simply download and run the latest msi package when informed of an update.

### Uninstalling the RIM Server

Uninstalling the RIM server is accomplished via standard means. However, its data folder (which resides in c:\ProgramData) will not be deleted. Should you wish to dispose of the data files, you can do so manually.