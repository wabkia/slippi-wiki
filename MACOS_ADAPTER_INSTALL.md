# MacOS Gamecube Controller Adapter Install

![image of slippi](https://slippi.gg/static/media/SlippiLogo.81afd6df.svg)

# Adapter Kext Installation
If you have a official Nintendo adapter, or a Mayflash adapter, follow the below steps exactly for Gamecube controller support under macOS. 

> WARNING: ALL STEPS MUST BE COMPLETED FOR THE ADAPTER TO FUNCTION PROPERLY.  
> NOTE: MacOS versions below 10.13 "High Sierra" are NOT supported

### **When entering terminal commands, pay attention to the output: if it says no such file, failure, or anything of the sorts, start from step 1. Third party offbrand adapters may or may not work.**

## Step 1:
1. Boot your Mac into recovery mode by restarting and holding CMD + R until the Apple logo appears.
1. Open a terminal (Utilities in menu bar -> Terminal)
1. Run: `csrutil disable`  
    * This disables SIP protection. Don't worry - you'll re-enable this in a bit. It is required for loading the kernel extension for the adapter.
1. Reboot into normal macOS.

## Step 2:
1. Open a terminal. (This can be found in Applications -> Utilities -> Terminal).
1. Run: `curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/project-slippi/Ishiiruka/slippi/Data/install_smashenabler.sh \| sh`
    * Follow the prompts, pay attention to the output.

## Step 3:
1. Boot your Mac into recovery mode by restarting and holding CMD + R until the Apple logo appears.
1. Open a terminal (Utilities in menu bar -> Terminal)
1. Run: `csrutil enable --without kext`
    > Note: This will say unsupported configuration. This command re-enables SIP, but leaves you the ability to load unsigned kernel extensions on-demand, which is what the adapter requires.
1. Reboot into normal macOS.

### Testing/Post Reboot Ritual
Your kext should now be installed. If Slippi still fails to read your controller, close it, open a terminal and run the following - this is needed more often on Catalina post-reboot, or on Mac models post-2018 that have a T2 security chip:

`sudo kextutil /Library/Extensions/SmashEnabler.kext`

### If you still have issues

1. In a terminal, run:  
`ioreg \| grep WUP-028 -A6`
1. Copy the output into PasteBin (www.pastebin.com)
1. Paste the link, MacOS version, Mac model, and adapter model to \#mac-support in [Slippi Discord](http://discord.gg/pPfEaW5) 

### WHY IS THIS SO DIFFICULT?!
It's an Apple-specific issue that nobody here has control over. We're all in the same boat. 