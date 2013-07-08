# Dealing with multiple Internet Explorers
As you should be aware, we support multiple versions of Internet Explorer, all the way back to IE7 in fact. This can make testing all of these various browsers difficult as you cannot have multiple versions of IE installed on a PC at one time. So what do we do to test these browsers? Fortunately, Microsoft provides a handful of VMs/Images that contain a variety of Operating Systems and Internet Explorers to run on a few popular VM applications (such as VMWare or VirtualBox). This guide will go over using these images on VirtualBox.
### Here are some things you will need:
+ Your Mac (or PC, although this guide will be mostly Mac related)
+ An internet connection
+ About an 30 minutes to setup the VM (download of the image may take longer)

When we are through you will have a set of VMs that will have a variety of Windows OSs and IEs. These should be used primarily for testing the IE browsers and should be considered disposable (that is, you can wipe the VM and reinstall it as you see fit). There should be no need to remote desktop from these VMs or use SQL Server on them.

**If you are looking for a _super easy_ way to install ALL of the VMs, just download [VirtualBox](#virtualbox) and follow the steps in [this](#super-easy-install-on-maclinux) section. I highly recommend this route.**

## Initial Downloads
### VirtualBox
First, go to https://www.virtualbox.org/wiki/Downloads. On the downloads page download the VirtualBox platform package for OSX hosts (click the x86/amd64 link to download). Once it downloads, open it up to install VirtualBox on your Mac.

### Virtual Machine Images
Next, go to http://www.modern.ie/en-us/virtualization-tools#downloads and in the first dropdown, select Mac as you desired testing OS. On the second dropdown, select VirtualBox for Mac as your virtualization platform. Multiple boxes should appear below that contain the different OS/IE combinations. You can tell what OS and IE combo the download is by the title in the blue bar (e.g. IE6 - XP, or IE8 - Win7). Some of them will be single downloads (which downloads a .ova file, more on this later), but some are split up into multiple parts.

#### Dealing with multiple part downloads
You can download each of the parts seperately, or you can use curl (via the command line) to download all of the parts at once. Keep in mind that the image downloads can be a bit large and may take some time depending on your connection.

To use curl

1. Open up the Mac's terminal/command line (in Spotlight search for "Terminal", it should be the first result)
2. cd to where you want to download the images (e.g. cd ~/Downloads)
3. Type the following into the terminal (choose the appropriate one for whichever OS/IE combo you want):
    - IE7 - Vista

        ```
        curl -O "https://az412801.vo.msecnd.net/vhd/IEKitV1_Final/VirtualBox/OSX/ \
        IE7_Vista/IE7.Vista.For.MacVirtualBox.part{1.sfx,2.rar,3.rar,4.rar,5.rar}"
        ```
    - IE8 - Win7

        ```
        curl -O "https://az412801.vo.msecnd.net/vhd/IEKitV1_Final/VirtualBox/OSX/ \
        IE8_Win7/IE8.Win7.For.MacVirtualBox.part{1.sfx,2.rar,3.rar,4.rar,5.rar,6.rar}"
        ```

    - IE9 - Win7

        ```
        curl -O "https://az412801.vo.msecnd.net/vhd/IEKitV1_Final/VirtualBox/OSX/ \
        IE9_Win7/IE9.Win7.For.MacVirtualBox.part{1.sfx,2.rar,3.rar,4.rar,5.rar}"
        ```

    - IE10 - Win7

        ```
        curl -O "https://az412801.vo.msecnd.net/vhd/IEKitV1_Final/VirtualBox/OSX/ \
        IE10_Win7/IE10.Win7.For.MacVirtualBox.part{1.sfx,2.rar,3.rar,4.rar}"
        ```

    - IE10 - Win8

        ```   
        curl -O "https://az412801.vo.msecnd.net/vhd/IEKitV1_Final/VirtualBox/OSX/ \
        IE10_Win8/IE10.Win8.For.MacVirtualBox.part{1.sfx,2.rar,3.rar}"
        ```

      The other 2 images (for Windows XP) are just direct downloads of the .ova file, so no need for curl.

    This command will download the individual parts of the VM into your current directory. These commands can also be found on the image download page (http://www.modern.ie/en-us/virtualization-tools#downloads). Just click on the respective "Grab them all with cURL" link to copy/paste the command.

## Installing the VMs
Once you have whichever VMs you want, launch VirtualBox and you should see a screen like (most likely without any VMs installed):

<img src="https://raw.github.com/thebobalu/ie_testing/master/vb_pic/vb_initial_screen.png" width="50%" height="50%"/>

The images you downloaded will either have been downloaded as a .ova file, or in multiple parts. If you are trying to use a VM that is currently in multiple parts, cd to the directory the parts have been downloaded into and run the following command in the terminal to make the .sfx file executable. Just replace 'filename.sfx' with the name of the appropriate .sfx file:
```
chmod +x filename.sfx
```
Once that is done, run the following command in the terminal to expand the files into a .ova file (which VirtualBox can then use). Again, replace 'filename.sfx' with the name of the appropriate .sfx file.
```
./filename.sfx
``` 
Now, back in VirtualBox, click on File on the Mac's menu bar and select 'Import Appliance'. From here, click 'Open appliance' and choose the .ova file for the VM that you want to install. 

Once that completes, select the VM in VirtualBox and click 'Start' and the VM should start up and be ready for use.

Click Continue, check the 'Reinitialize the MAC address of all network cards' checkbox,  then click Import. VirtualBox will then install the VM. This may take some time.

## SUPER EASY Install on Mac/Linux
Just install [VirtualBox](#virtualbox) (from https://www.virtualbox.org/wiki/Downloads) and run the following command in the terminal:
```
curl -s https://raw.github.com/xdissent/ievms/master/ievms.sh | bash
```
Once that completes, which will take awhile to download ALL of the images, you will then have IE6, IE7, IE8, IE9, and IE10 running on separate virtual machines. :)

For more info on this process, see https://github.com/xdissent/ievms.

## Notes
### These VMs will have a time limits on them
+ IE7 – IE10: 90 days of total time from the moment you first use the VM. Basically it’s 30 days usage with two 30-day rearms.

    - To rearm, go into a command prompt and type in “slmgr –rearm“

+ IE6 on WinXP: Will expire 90 days from the time we upload it to modern.IE. There’s no rearm it but they’ll keep this refreshed when the 90 day kill date nears.

### At the end of the 90 days, here’s what will happen:
- IE7 – IE10: You’ll be able to use the VM for an hour before it shuts down
- IE6/WinXP: You’ll be prompted for an activation key with no way to get past it

That said, you should be able to revert the VM to its 'clean' snapshot to reset everything. Keep in mind that you will lose any saved files or downloads on that machine (but you should really only be using these VMs for IE testing purposes).

**For more information, feel free to visit these resources:**
- www.modern.ie
- https://github.com/xdissent/ievms
- http://blog.reybango.com/2013/02/04/making-internet-explorer-testing-easier-with-new-ie-vms/
- www.virtualbox.org

## Tips and Tricks
- If you want to use a higher version of IE on a particular OS (that supports it, of course). You can copy a VM and then upgrade the IE on it to your desired version.
- The super easy installation automatically creates snapshots of the VM in a 'clean' state. You can revert back to this snapshot at anytime if you mess up the VM somehow. For VMs you add yourself, you will need to create the snapshots yourself.
- Make sure you set the shared clipboard to 'bidirectional' on the VM so that you can copy/paste things between your VM and host.
- Make sure that you increase the RAM used on the VM if you are having performance issues.
- If you want to use Windows 7 and IE8 perform the following steps (also found [here](http://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/downgrade-from-ie9-to-ie8-ie9-came-with-the-new/65bb334a-cc68-4940-99f7-6f0bb9376c80)).
    1. On the VM, go to the Control Panel
    2. Click on 'Uninstall a program'
    3. Click on 'View installed updates'
    4. Click on 'Windows Internet Explorer 9'
    5. Click 'Uninstall'
    6. Click 'Restart' to update the VM.
    7. Once complete, you should now have IE8.

- Keep in mind that this covers the major versions of IE. There are some sub-minor versions of each browser where, in rare cases, have caused issues. If you need specific build number versions of IE, for example a Beta release,  you may need to dig around. Many can be found [here](http://www.oldapps.com/internet_explorer.php). 
