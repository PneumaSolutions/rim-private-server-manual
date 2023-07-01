# Installation
Remote Incident Manager is packaged as a virtual appliance (OVA) that can be installed on any VMWare product. We will provide instructions for VMWare Workstation Player on Windows, as well as Fusion on the Mac
## VMWare Workstation Player.
1. Acquire and install [VMWare Workstation Player](https://download3.vmware.com/software/WKST-PLAYER-1700/VMware-player-full-17.0.0-20800274.exe) and take care of any updates to it if need be.
1. Open your downloaded RIM package. Workstation Player will bring up the import wizard.
1. Give the VM a name, then press enter.
1. The virtual machine should boot up momentarily. A beep will confirm that it is ready.
<!-- end -->
## VMWare Fusion
Fusion requires an account to be created, so we cannot provide the download link directly. Once Fusion is downloaded, installed and configured:
1. Open your downloaded RIM package. Workstation Player will bring up the import wizard.
1. Click the "Continue" button.
1. A standard save as dialogue will appear, at which point you can give the virtual machine a name and press enter.
1. Once the import completes, click the "Finish" button.
1. The virtual machine should boot up momentarily. A beep will confirm that it is ready.
<!-- end -->
# Updates
Updates will be distributed in the form of iso images.
## VMWare Workstation Player 
When downloading the iso, we recommend saving it in the same directory as the virtual machine. Once downloaded:
1. From within the VM library, click on "Edit virtual machine settings"
    1. If inside the virtual machine, access the option off the menu or press *CTRL+B*.
1. Select "CD/DVD (IDE)" in the list of hardware devices.
1. Select "Use ISO image file:" or press *Alt+M*.
1. In the "Use ISO image file:" combo-box, type or paste the name of the iso, then press enter.
1. Power up or restart the virtual machine.
    <!-- end -->
    ## Fusion
    The process for Fusion is somewhat similar, with some differences as described below. First and foremost, it does not matter where you save the iso image.
1. After selecting the RIM server in your virtual machine library, locate the "Settings" button in the toolbar or press *Command+E*.
1. Select "CD/DVD (IDE)" in the new screen that appears.
1. Activate the "This CD/DVD drive is configured to use the following:" pop up button
1. Select "Choose a disc or disc image …" from the menu.
1. Locate your iso, then click on the file or press enter.
1. Close the settings screen, then start up or restart the virtual machine.