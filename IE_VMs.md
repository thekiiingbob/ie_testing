# Dealing with multiple Internet Explorers
As you should be aware, we support multiple versions of Internet Explorer, all the way back to IE7 in fact. This can make testing all of these various browsers difficult as you cannot have multiple versions of IE installed on a PC at one time. So what do we do to test these browsers? Fortunately, Microsoft provides a handful of VMs/Images that contain a variety of Operating Systems and Internet Explorers to run on a few popular VM applications (such as VMWare or VirtualBox). This guide will go over using these images on VirtualBox.
### Here are some things you will need:
+ Your Mac (or PC, although this guide will be mostly Mac related)
+ An internet connection
+ About an 30 minutes to setup the VM (download of the image may take longer)

When we are through you will have a set of VMs that will have a variety of Windows OSs and IEs. These should be used primarily for testing the IE browsers and should be considered disposable (that is, you can wipe the VM and reinstall it as you see fit). There should be no need to remote desktop from these VMs or use SQL Server on them.

If you are looking for a _super easy_ way to install ALL of the VMs, just download VirtualBox and follow the steps in [this](#super_easy) section.

## Initial Downloads
First, go to www.virtualbox.org, and click on Downloads on the left. On the downloads page download the VirtualBox platform package for OSX hosts (click the x86/amd64 link to download). Once it downloads, open it up to install VirtualBox on your Mac.

Next, go to http://www.modern.ie/en-us/virtualization-tools#downloads and in the first dropdown, select Mac as you desired testing OS. On the second dropdown, select VirtualBox for Mac as your virtualization platform. Multiple boxes should appear below that contain the different OS/IE combinations. You can tell what OS and IE combo the download is by the title in the blue bar (e.g. IE6 - XP, or IE8 - Win7). Some of them will be single downloads (which downloads a .ova file, more on this later), but some are split up into multiple parts.

### Dealing with mulpiple part downloads
You can download each of the parts seperately, or you can use curl (via the command line) to download all of the parts at once. Keep in mind that the image downloads can be a bit large and may take some time depending on your connection.

To use curl

1. Open up the Mac's terminal/command line (in Spotlight search for "Terminal", it should be the first result)
2. cd to where you want to download the images (e.g. cd ~/Downloads)
3. Type the following into the terminal:

         curl -O "https://az412801.vo.msecnd.net/vhd/IEKitV1_Final/VirtualBox/OSX/ \
         IE7_Vista/IE7.Vista.For.MacVirtualBox.part{1.sfx,2.rar,3.rar,4.rar,5.rar}"

    This command will download IE7 on Vista, as an example. These commands can also be found on the image download page (http://www.modern.ie/en-us/virtualization-tools#downloads). Just click on the respective "Grab them all with cURL" link to copy/paste the command.

## Installing the VMs
Once you have whichever VMs you want, launch VirtualBox and you should see a screen like (most likely without any VMs installed):

<img src="https://raw.github.com/thebobalu/ie_testing/master/vb_pic/vb_initial_screen.png" width="50%" height="50%"/>

## <a id="super_easy"/> SUPER EASY INSTALL ON MAC/LINUX
Just install VirtualBox and run the following command in the terminal:
```
curl -s https://raw.github.com/xdissent/ievms/master/ievms.sh | bash
```
Once that completes, which will take awhile to download ALL of the images, you will then have IE6, IE7, IE8, IE9, and IE10 running on separate virtual machines. :)

For more info on this process, see https://github.com/xdissent/ievms.

## Notes:
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

TEST
```
curl \
www.google.com
```
