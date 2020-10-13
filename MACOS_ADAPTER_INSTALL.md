<p align="center">
  <img src="https://slippi.gg/static/media/SlippiLogo.81afd6df.svg"/>
</p>

# Gamecube Controller Adapter Kext Installation
If you have a official Nintendo adapter, or a Mayflash adapter, follow the below steps exactly for Gamecube controller support under macOS. 

> WARNING: **ALL STEPS MUST BE COMPLETED FOR THE ADAPTER TO FUNCTION PROPERLY.**

> NOTE: MacOS versions below 10.13 "High Sierra" are **NOT** supported

#### **When entering terminal commands, pay attention to the output: if it says no such file, failure, or anything of the sorts, start from step 1. Third party offbrand adapters may or may not work.**

## Step 1:
1. Boot your Mac into recovery mode by restarting and holding CMD + R until the Apple logo appears.
1. Open a terminal (Utilities in menu bar -> Terminal)
1. Run: `csrutil disable`  
    * This disables SIP protection. Don't worry - you'll re-enable this in a bit. It is required for loading the kernel extension for the adapter.  
1. Reboot into normal macOS.

## Step 2:
1. Open a terminal. (This can be found in Applications -> Utilities -> Terminal).
1. Run: `curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/project-slippi/Ishiiruka/slippi/Data/install_smashenabler.sh | sh`
    * Follow the prompts, pay attention to the output.

## Step 3:
1. Boot your Mac into recovery mode by restarting and holding CMD + R until the Apple logo appears.
1. Open a terminal (Utilities in menu bar -> Terminal)
1. Run: `csrutil enable --without kext`
    * This will say unsupported configuration. This command re-enables SIP, but leaves you the ability to load unsigned kernel extensions on-demand, which is what the adapter requires.  
1. Reboot into normal macOS.

### Testing/Post Reboot Ritual
Your kext should now be installed. If Slippi still fails to read your controller, close it, open a terminal and run the following - this is needed more often on Catalina post-reboot, or on Mac models post-2018 that have a T2 security chip:

`sudo kextutil /Library/Extensions/SmashEnabler.kext`

### If you still have issues

1. In a terminal, run:  
`ioreg | grep WUP-028 -A6`
1. Copy the output into PasteBin (www.pastebin.com)
1. Paste the link, MacOS version, Mac model, and adapter model to **\#mac-support** in [Slippi Discord](http://discord.gg/pPfEaW5) 

### WHY IS THIS SO DIFFICULT?!
It's an Apple-specific issue that nobody here has control over. We're all in the same boat.

## _**Still having trouble?**_  

If for whatever reason you're unable to install the kext, an alternate approach that @vamus found is below but it's input latency will be slightly higher:  
1. Close Slippi  
1. Switch the adapter into "PC Mode" using the hardware switch on the adapter  
1. Open Slippi, open `Controller` settings  
1. Change `Gamecube Controller Port 1` from `Gamecube Adapter for WiiU` to `Standard Controller`  
1. Click `configure` next to `Standard Controller`  
1. In the `Device` list in the top left of the new window, you should see 2-4 devices named like `DInput/0/MAYFLASH GameCube Controller Adapter`  
1. Select the port your controller is plugged into.
    * This list starts at 0, which is the first port on the adapter.  
1. Go through each button and map it to your GameCube Controller.

> NOTE: As this method doesn't use the kext to handle controller recognition, it may perform differently. If you experience issues (input lag in particular) with this method, sounding off in the chat would be helpful.