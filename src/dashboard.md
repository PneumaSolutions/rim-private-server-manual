# The RIM Management Dashboard
Your RIM server features a  web-based dashboard to facilitate various machine and account management tasks. You can manage your existing unattended computers, create preconfigured installers for target computers, and much more.  
## Locating the Dashboard
If you're a controller, the easiest way to get to the dashboard is through the main RIM interface. Clicking the RIM Dashboard button will automatically open the dashboard in your default browser, with the login already taken care of.  
If you are a network administrator who does not have RIM installed, you can simply log into your account on your RIM server's web interface and your dashboard will appear.
## Target Groups
Say for instance you're workgroup is spread out among several different locations. Or maybe you want to designate groups of machines to your routine maintenance techs. Target groups allow you to do just that.
For ease of organization, you must create at least one target group before you can configure a machine. In order to do this, simply click the "Create Target Group" button, name your group, and submit.  
You may have as many target groups as is needed for your use case. 
### Access Control (for Enterprise Organizations)
If your organizations assign a support technician to a specific set of machines, you probably want to ensure they only have access to that specific set. This is where the access control setting for target groups comes in.  
When you click on a target group, you are given options to manage the machines in the group, as well as the group itself. The access control section is where you may grant access to this group on a per-account basis. Simply enter the email address of the account you wish to add, then click the "Give Access" button. Once this is done, you will be presented with a table of accounts that are given access to this group. Below each account is a "Revoke Access" button. This button does not require further confirmation.  
It should be noted that all organization administrators are automatically granted access to manage any and all groups that are created under the organization.
## Managing Targets
When you click the "Configure Targets" link, you will arrive at a page that allows you to manage all the machines you have configured for unattended access. You can click on any one of these machines in order to manage it. Once inside, you will be able to:
* Rename the target
* Move the target to a different group (more on target groups later)
* Delete the target
<!-- end -->
Lastly, you will be able to create installers from this page that can be used to provision computers into this target group.
## Setting up a Preconfigured RIM Installer (Pro or above)
One of the easiest ways to set up a machine for unattended or prompted connections is by creating a custom installer. This is incredibly useful if you are configuring mass deployments, or even as a simpler way to get RIM up and running on an end user's computer you plan on providing support for on the regular.
In order to do this:
1. In the target management screen, click the "Build Target Installer" button.
1. You will first be asked if you want this machine to be configured for fully unattended access, or for prompted access in which the user has to accept a prompt to initiate the connection.
1. You will then be asked for a target group assignment. Note that the target group selection will automatically go to your chosen target group if you initiate the installer configuration from your group's page.
1. You will be asked how long you want this installer to be valid for. It can be valid for anywhere between 7 to 30 days. Note that this timeframe only affects the functionality of the installation package. In other words, the machine's RIM configuration will not be disabled when the installation expires.
1. You are then given the option to assign a bass name. Any machine provisioned via this installation package will have this base name assigned to it.
1. After supplying the base name, you will see a checkbox that allows you to build the installer as an MSI package. This option is useful for mass deployment of a custom installer to a machine cluster that will be designated to the given target group.
1. You will be asked to provide an installer name, and optionally some notes. These are for internal records and will not appear within the created installer.
1. Click on "Build Installer." You will be presented with the download link that you can either copy to the clipboard and send to your end user. Alternatively, you may download the installer directly for use in mass deployments.
<!-- end -->
Now that you have your installer, it can be run in one of two ways. In either case, the machine will be added to your list of machines in both your account as well as the RIM client after the installer is complete.
### Normal Execution
The user will get a prompt when running the installer, containing the following information:
* The technician's name along with their organization, if applicable
* the nature of the connection, I.E whether a prompt is required or not
<!-- end -->
The user can choose to either answer yes or no to the installation. Answering no will cancel the installation. After the installer finishes, the user will get a prompt informing them that their machine is now set up for remote access.
### Silent Install
A silent install can be initiated by running the executable installer with the */S* command line parameter. This is useful when installing RIM as part of a mass deployment routine.
## Session History
You can view your entire history of past sessions through the RIM dashboard. The session history currently contains the date and time of each session, the name of the computer you connected to, and the duration of the session. You may also choose to add comments to a session via the "Add Comment" link within the session row. This is useful for adding notes on the current status of an incident for your own sake as well as for the sake of organization administrators.
