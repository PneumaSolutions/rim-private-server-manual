# Installation
Remote Incident Manager is packaged as either a virtual appliance (OVA) that can be installed on any VMWare product, or as a stand-alone package installable on Windows Server.

## Configuring the Virtual Appliance

We will provide instructions for VMWare Workstation on Windows, Fusion on macOS, and VMWare ESXi.

### Installing on VMWare Workstation

1. Acquire and install VMWare Workstation. Note that while VMWare Workstation is free to download, accessing the download requires the creation of a VMWare account.
1. Open your downloaded RIM package. Workstation Player will bring up the import wizard.
1. Give the VM a name, then press enter.
1. The virtual machine should boot up momentarily. A beep will confirm that it is ready.
<!-- end -->

### Installing on VMWare Fusion

Acquire and install VMWare Fusion. Note that while VMWare Fusion is free to download, accessing the download requires the creation of a VMWare account. Once Fusion is downloaded, installed and configured:
1. Open your downloaded RIM package. Fusion will bring up the import wizard.
1. Click the "Continue" button.
1. A standard save as dialogue will appear, at which point you can give the virtual machine a name and press enter.
1. Once the import completes, click the "Finish" button.
1. The virtual machine should boot up momentarily. A beep will confirm that it is ready.
<!-- end -->

### Installing on VMWare ESXi

Remote Incident Manager should run under most recent versions of the ESXi server. In order to deploy RIM:
1. Once in the eSXi host client, click on "Create or register a Virtual Machine."
1. In the "Select Creation Type" list, choose "Deploy a virtual machine from an OVF or OVA file," then click the next button.
1. Name the virtual machine, then click the "Choose Files:" button. A standard file upload browse window will appear where you can select the .ova file you downloaded.
1. In the "Select the storage type and datastore" screen, you can safely leave everything at its default and hit next.
1. The options in the Select deployment options screen can also be left at their defaults. In particular, it is recommended to ensure "Power on automatically" is checked. If everything is to your liking, hit next.
1. The final screen will allow you to review your settings. Click Finish on this screen, then wait while the vm deploys.
<!-- end -->
Once the VM is deployed, it will power on. If you are not automatically placed within the VM overview screen, click on "Virtual Machines" in the main navigation bar, then click on your new virtual machine. Once inside, click on "Networking." You should see a list of IP addresses, the first one being the IPV4 address. This is the one you will use within your DNS. Allow the IP address to resolve to the hostname of your choosing, then visit the location in your web browser to access the RIM server web interface.

### Updates

Updates will be distributed in the form of iso images.

#### VMWare Workstation

When downloading the iso, we recommend saving it in the same directory as the virtual machine. Once downloaded:
1. From within the VM library, click on "Edit virtual machine settings"
    1. If inside the virtual machine, access the option off the menu or press *CTRL+D*.
1. Select "CD/DVD (IDE)" in the list of hardware devices.
1. Select "Use ISO image file:" or press *Alt+M*.
1. In the "Use ISO image file:" combo-box, type or paste the name of the iso, then press enter.
1. Power up or restart the virtual machine.
    <!-- end -->

#### Fusion

    The process for Fusion is somewhat similar, with some differences as described below. First and foremost, it does not matter where you save the iso image.
1. After selecting the RIM server in your virtual machine library, locate the "Settings" button in the toolbar or press *Command+E*.
1. Select "CD/DVD (IDE)" in the new screen that appears.
1. Activate the "This CD/DVD drive is configured to use the following:" pop up button
1. Select "Choose a disc or disc image …" from the menu.
1. Locate your iso, then click on the file or press enter.
1. Close the settings screen, then start up or restart the virtual machine.
<!-- end -->

#### ESXi

In order to apply a new ISO image:
1. Power off the virtual machine.
1. Click on "Edit the virtual machine's settings."
1. Click on CD/DVD drive.
1. Click the Choose Files:" button, then select the iso you downloaded.
1. Wait for the iso to upload, click on it, then click "Select."
1. Power up the virtual machine.
<!-- end -->


## Setup Process for Windows Server

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

Now that we have a working reverse proxy, it is time to install the RIM server package. The installation is a one-click silent install. Once the installation is finished, the server will start automatically. Note that unless you have set up a reverse proxy as described above, you will need to access the server on port 7460 for initial setup. Additionally, if you intend for your RIM infrastructure to be accessible via the live web, you will need to add your own https firewall rule, as IIS only opens port 80 by default. You do not, however, need to open port 7460.

### Uninstalling the RIM Server

Uninstalling the RIM server is accomplished via standard means. However, its data folder (which resides in c:\ProgramData) will not be deleted. Should you wish to dispose of the data files, you can do so manually.