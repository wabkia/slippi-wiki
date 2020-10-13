# MacOS Gamecube Controller Adapter Install

# Adapter Kext Installation
If you have a official Nintendo adapter, or a Mayflash adapter, follow the below steps exactly for Gamecube controller support under macOS. When entering terminal commands, pay attention to the output: if it says no such file, failure, or anything of the sorts, start from step 1. Third party offbrand adapters may or may not work.

## Step 1:
1. Boot your Mac into recovery mode by restarting and holding CMD + R until the Apple logo appears.
1. Open a terminal (Utilities in menu bar -> Terminal)
1. Run csrutil disable. Don't worry - you'll re-enable this in a bit. It is required for loading the kernel extension for the adapter.
1. Reboot into normal macOS.

## Step 2:
1. Open a terminal. (This can be found in Applications -> Utilities -> Terminal).
2. Run: curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/project-slippi/Ishiiruka/slippi/Data/install_smashenabler.sh \| sh
3. Follow the prompts.

## Step 3:
1. Boot your Mac into recovery mode by restarting and holding CMD + R until the Apple logo appears.
2. Open a terminal (Utilities in menu bar -> Terminal)
3. Run: csrutil enable --without kext
    1.1. Note: This will say unsupported configuration. This command re-enables SIP, but leaves you the ability to load unsigned kernel extensions on-demand, which is what the adapter requires.
4. Reboot into normal macOS.

## Testing/Post Reboot Ritual
Your kext should now be installed. If Slippi still fails to read your controller, close it, open a terminal and run the following - this is needed more often on Catalina post-reboot, or on Mac models post-2018 that have a T2 security chip:

> sudo kextutil /Library/Extensions/SmashEnabler.kext

## If you still have issues, run the following report it in here with your macOS version/model/adapter model:

> ioreg \| grep WUP-028 -A6

## WHY IS THIS SO DIFFICULT?!
It's an Apple-specific issue that nobody here has control over. We're all in the same boat. 