# The RIM Management Dashboard
Your RIM server features a  web-based dashboard to facilitate various machine and account management tasks. You can create preconfigured installers for target computers, manage your existing unattended computers, and much more.  
## Locating the Dashboard
If you are a network administrator who does not have RIM installed, you can simply log into your account on your RIM server's web interface and your dashboard will appear.
If you're a controller using a client issued by the server, the easiest way to get to the dashboard is through the main RIM interface. Clicking the RIM Dashboard button will automatically open the dashboard in your default browser, with the login already taken care of.  
## Authorizing the Client
If you plan on using RIM in addition to administering your server, the first thing you are going to want to do is to provision your RIM client. There will be a link on your dashboard that will take you to a page that allows you to install a server profile. Once you land on this page, you will first be instructed to install the RIM application on your computer if you haven't done so already. Direct download links for the Windows and macOS client applications are provided on this page. The Windows setup file is a stub that will always download the latest version of the client from your server when run. We are unfortunately unable to offer this capability on macOS due to the nature of the package.  
Once RIM is installed on your computer, go back to the profile page and click the "Install Profile" button. You will then receive a dialog from RIM stating that it has been provisioned for use with your server.  
Note that this profile configuration page can be given to end users who will be receiving remote technical support through your organization.

## Managing Organization Members 

Activating the "Organization" button on the RIM dashboard will reveal a menu of options related to organization and member management. The "Members" page will list all the members in your organization. All members can have their role, department and name modified, and any member can be deactivated or removed from an organization except for the organization owner. Note that deactivating a member will render their account inoperable while retaining its record.

Adding members is as simple as entering their email address, selecting their role (user or administrator), optionally entering their name, and selecting their department if one has been created.
If you have multiple members to add, you can use the "Members" edit field to perform a bulk add. This edit field accepts multiple lines of text, allowing you to enter each member's information on a separate line. On each line, you may enter either a single email address, or an email address and a name in the format:  
*email@example.com John Doe*

Once you are finished, click the "Add" button. 

### Departments

Departments allow you to organize members according to the various groups of your organization.

To add a department, enter its name in the "Name" edit box under the "Create department" heading.

### Member Data export

The member list in your organization can be exported as a CSV file. In order to download the export:
1. Choose the field separator that will separate the columns of the file. The available options include:
    * comma
    * Semicolon
    * Tab
1. Activate the "Download" button.

## Restrictions

Depending on the nature of your organization, there may be certain features you do not want your staff to have access to. As such, organization admins can choose the features they wish to allow controllers access to. The "Restrictions" screen, accessed via the "Organization" menu, allows you to configure these permissions.

The permissions that can be toggled include:
* Allow the controller to flip the session
    * If this option is unchecked, the "Flip Session" option will disappear from the session menu, and the keyboard shortcut will not work.
* Allow the controller to start a voice conversation
    * If this option is unchecked, the "Start Voice Conversation" checkbox will disappear from the "Provide Remote Help" screen, as will the menu option in the session menu.
* Allow the controller to request unattended access
    * If this option is unchecked, the option to request unattended access will disappear from the session menu.
* Allow text and files to be transferred between machines via the clipboard
    * If this option is unchecked, RIM will ignore any and all clipboard activity.
* Allow the controller to lock the target machine
    * If this option is unchecked, the option to lock the target machine will disappear from the session menu.

Once you have configured the permissions to your satisfaction, activate the "Update" button. Changes will not affect any active sessions at the time the permissions are changed. They will however take effect for any and all future sessions without requiring a reboot of the client.

## Managing Targets

When you click the "Configure Targets" link, you will arrive at a page that allows you to manage all the machines you have configured for unattended access. You can click on any one of these machines in order to manage it. Once inside, you will be able to:
* Rename the target
* Move the target to a different group (more on target groups later)
* Launch a remote session with the target
* Delete the target

### Target Groups 

Say for instance your workgroup is spread out among several different locations. Or maybe you want to designate groups of machines to your routine maintenance techs. Target groups allow you to do just that. In order to do this, simply click the "Create Target Group" button, name your group, and submit.  
You may have as many target groups as is needed for your use case. 

#### Access Control (for Enterprise Organizations)

If your organizations assign a support technician to a specific set of machines, you probably want to ensure they only have access to that specific set. This is where the access control setting for target groups comes in.  
When you click on a target group, you are given options to manage the machines in the group, as well as the group itself. The access control section is where you may grant access to this group on a per-account basis. Simply enter the email address of the account you wish to add, then click the "Give Access" button. Note that this account can exist outside of your enterprise organization's domain.  
Once this is done, you will be presented with a table of accounts that are given access to this group. Below each account is a "Revoke Access" button. This button does not require further confirmation.  
It should be noted that all organization administrators are automatically granted access to manage any and all groups that are created under the organization. Additionally, any email addresses under your organization's domains will be added to your organization in RIM by default. Should you require more granular control over who gets onboarded, you can disable this in your organization's main members area. What's more, when in the members area you can add email addresses in bulk by way of commas, spaces or line breaks in between the email addresses.

### Setting up a Preconfigured RIM Installer

One of the easiest ways to set up a machine for unattended or prompted connections is by creating a custom installer. This is incredibly useful if you are configuring mass deployments, or even as a simpler way to get RIM up and running on an end user's computer you plan on providing support for on the regular.

IN order to do this:
1. In the target management screen, click the "Build Target Installer" button.
1. You will first be asked if you want this machine to be configured for fully unattended access, or for prompted access in which the user has to accept a prompt to initiate the connection.
1. You will then be asked for a target group assignment. Note that the target group selection will automatically go to your chosen target group if you initiate the installer configuration from your group's page.
1. You will be asked how long you want this installer to be valid for. It can be valid for anywhere between 7 to 30 days, or permanently valid by setting the expiration to never.
1. You are then given the option to assign a bass name. Any machine provisioned via this installation package will have this base name assigned to it.
1. You will then be presented with a checkbox that lets you opt into an email notification when a user installs RIM via this installer.
1. You will see a checkbox that allows you to build the installer as an MSI package. This option is useful for mass deployment of a custom installer to a machine cluster that will be designated to the given target group.
1. You will be asked to provide an installer name, and optionally some notes. These are for internal records and will not appear within the created installer.
1. Click on "Build Installer." You will be presented with the download link that you can either copy to the clipboard and send to your end user. Alternatively, you may download the installer directly for use in mass deployments. You may delete the installer from this screen should you choose to render it inoperable prematurely.

Now that you have your installer, it can be run in one of two ways. In either case, the installer will query the server to check for validity. If the installer is valid, the machine will be added to your list of machines in both your account as well as the RIM client after the installer is complete. An invalid installer will not run.

#### Normal Execution

The user will get a prompt when running the installer, containing the following information:
* The technician's name along with their organization, if applicable
* the nature of the connection, I.E whether a prompt is required or not

The user can choose to either answer yes or no to the installation. Answering no will cancel the installation. After the installer finishes, the user will get a prompt informing them that their machine is now set up for remote access.

#### Silent Install (Enterprise Installers Only)

A silent install can be initiated by running the executable installer with the */S* command line parameter. This is useful when installing RIM as part of a mass deployment routine.

## Session History

You can view your entire history of past sessions through the RIM dashboard. The session history currently contains the date and time of each session, the name of the computer you connected to, and the duration of the session. You may also choose to add comments to a session via the "Add Comment" link within the session row. This is useful for adding notes on the current status of an incident for your own sake as well as for the sake of organization administrators.

Your entire session history can be exported for later viewing via a spreadsheet application. Activate the "Download session history as CSV" button located below the session history table to reveal a customization page for your data export. On this page, you can choose the timespan of the export, as well as the symbol used to separate the fields.

## Managing your License

The RIM server is designed in such a way that does not allow it to proactively query a cloud service. This is designed to make the server friendly for maximum-security environments, however it does mean that manual license renewal is necessary. The "Refresh" license button allows the server to retreive the currently active license key from the cloud service. The process for relicensing is identical to the initial license activation process, and can be done with or without an active internet connection on the server itself.