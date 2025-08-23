Disable dedicated GPU and run on internal graphics to prevent BSOD when unplugged.

How to use script:
1. Download both bat files and place them somewhere safe.
2. Go to device manager, find your dedicated GPU (eg. RTX 3080), right click > details > device instance path > copy the value (eg. PCI\XXXXXXXXXXXXXXXXXXXX)
3. Edit each bat file with notepad, replace existing "PCI\XXXXXXXXXXXXXXXXXXXX" with the one that matches your device that you copied.
4. You will need to attach each of the bat scripts to automatically run when power is connected or disconnected, check this article for how to use Task Scheduler to do that: https://dev.to/muhammedziyad/automatically-disable-and-enable-your-gpu-or-any-other-device-when-your-laptop-power-state-changes-hf5
   PS: The Article will say to use powershell and also at one of the steps add additional arguments, that method is outdated and doesnt work, at the add program part instead of wrting powershell.exe and the additional argument simply click browse and add the .bat script directly.
5. The disable/enable script should now automatically run when power state is changed, however it does not take into account what state pc is after waking up (for example laptop was plugged in, then shutdown and plugged out, then started up, so the script doesnt now that it should disable the GPU because the power state changed while turned off, to fix that follow my additional steps)
6. In Task Scheduler go to Event Viewer Tasks where you have your 2 created tasks and create 2 more, first one to automatically disable the GPU Device at startup no matter what, and then add a second one that will automatically enable the GPU Device at startup but ONLY if device has AC power, and add a 10 second timer so it only runs after the first one has finished.
   The logic is like this: PC Wakes up, PC doesnt know if power state changed so automatically disables GPU, 10 seconds after startup check if PC is plugged or not, if plugged go ahead and enable the GPU Device, if unplugged keep it disabled. 
