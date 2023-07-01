# Troubleshooting
This section will provide solutions to common issues you may run into.
# Inability to resolve rim-server host
## The Problem
Depending on the configuration of your network, your system may not be able to immediately resolve the rim-server hostname to the proper IP address when the machine boots up for the first time.
## The Solution
You will need to obtain the IP address of your virtual machine. If you are able to access your router's control panel, you may obtain the IP address that way. However, because each router has its own interface with varying degrees of accessibility, we will not be able to provide support directly for this method. We can, however, assist in getting the IP address from the VM directly. This involves adding a Serial Port Output to the virtual machine and storing its console output to an output file.
### VMWare Workstation Player
1. Shut down the virtual machine if you haven't already..
1. Click on Edit virtual machine settings" or press *CTRL+D*.
1. Click on "Add..." or press *Alt+A*.
1. Select *serial port* from the list.
1. Click on "Use output file:" or press *Alt+S*.
1. Enter the name of the output file and click "OK."
    1. By default, the output file is saved in the directory of your appliance, c:\users\"yourUserName"\documents\Virtual Machines\"Name of your Machine". Should you wish to change the path where the file will be saved, click on "Browse..." or press *Alt+B*.
1. In any case, you will be asked if you wish to create the file based on the name you entered. Answer yes.
1. Boot up the machine, and wait for it to beep.
1. Navigate to the path at which you saved your serial console's output file, and open the file in notepad. Scroll down a line or two and you should see the IP address of the machine appear.
### VMWare Fusion
The process for Fusion is somewhat similar.
1. After selecting the RIM server in your virtual machine libarary, locate the "Settings" button in the toolbar or press *Command+E*.
1. Locate the "Add Device" button in the toolbar.
1. Select "Serial Port" from the new window that appears.
1. You will be asked to enter the name of the output file. This will be saved in the directory of the virtual machine.
1. Close the virtual machine settings.
1. Boot up the machine, and wait for it to beep.
1. Navigate to the path at which you saved your serial console's output file, and open the file in Text Edit. Scroll down a line or two and you should see the IP address of the machine appear.