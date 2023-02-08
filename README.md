# Contabo-Windows10
##Installing Windows 10 on a Contabo VPS for dummies

DISCLAIMER:
- You are accepting all risk associated with the installation of Windows on your Contabo vps and the activation method listed as part of these instructions.

Prerequisites:
- A VNC app installed on a computer, tablet, or even your phone.  Search for "VNC Viewer"
- A vps with Contabo (obviously)
- Micorsoft's Remote Desktop App.  Search for "Remote Desktop" and download the one that's published by Microsoft.
  
Put your vps into recovery mode by doing the following from the the My Services section of the user panel:
- Click the blue "Manage" button and select "Rescue System"
- Once the page loads select Clonezilla-live from the "Rescue System Version" dropdown menu.
- Enter a password
- Click "Start Rescues System"

Connect to the vps via VNC:
- On the page that loads when you do the previous steps click the blue "Manage" button.
- Select "VNC Information" and note the IP address and port and close the window.
- Click the blue "Manage" button again and select "VNC Password"
  - Generate a password and note it somewhere.
- Open your VNC app of choice and create a new connection.
  - The address will be in the format of ipaddress:port
  
Load Windows via the rescue system:
- Select "Enter shell command" from the menu
- Type the following and press enter:
  - `su && wget -O- "https://drive.google.com/file/d/1npbdkJb0XevuyICx_E58JuRiAQeUTooa/view?usp=sharing" | gunzip | dd of=/dev/sda`
    - You will be prompted for a password.  The password is the one you enterred when putting the vps into recovery mode.
       - Additionally, this step may take some time so be patient.
- Once the above completes type `reboot`
  
After some time windows will load.  Follow the prompts to set up Windows.

Once you had made it to the desktop click in the search area and type "remote"
- Select Remote Desktop Settings from the results (Probably the second item on the list)
- Click the button where it says "Enable Remote Desktop"
- Disconnect the session/close the VNC app.
  
Open the Remote Desktop program/application

In the search area type `cmd` and press enter.  

Once the command prompt opens type the following pressing enter after each entry:
- `diskpart`
- `List Disk`
- `Select Disk 0`
- `List Partition`
- `Select Partition 3` (This should be listed as "Recovery")
- `Delete Partition Override`
- Close the window
  
Type "partition" in the search area and select the first result.  It should be "Create and Format Hard Disk Partitions"
- Right click (or long press if on tablet/mobile) on the partition listed as "C:"
- Select "Extend Partition"
- Click "OK" (The system automatically sets it up to use the remaining unpartitioned space on the hard drive.
  
Activate windows:
- In the search area type `cmd` and press Enter.
- Type the following and press Enter:
  - `bitsadmin.exe /transfer "JobName" "https://raw.githubusercontent.com/abbodi1406/KMS_VL_ALL_AIO/master/KMS_VL_ALL_AIO.cmd" "C:\Users\YOURUSERNAME\Downloads\activate.cmd`
    - Replace `YOURUSERNAME` with the username you set up when you set up windows.
  - Enter option `2` (Install Activation Auto-Renewal) and press enter. 
  - Once the operation is complete close the window.
    
That's it.  Enjoy using your fresh windows install.
