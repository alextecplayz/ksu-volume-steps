# ksu-volume-steps
KernelSU module OR script. Don't use both at the same time.

## How it works:
It simply changes the number of steps used by Android to calculate how much the volume will be changed, akin to this formula: `100 / step = volume changed %`, where 100 is the total number of steps for that stream type (e.g. max call volume), which is divided by one step, which results in how much the volume is changed.

So, if you give vc_call_vol 20 steps, the volume will change by 5%. I don't recommend you go over 50 for most of these values, except for media_vol_steps, which can go as high as 99 from my testing, perhaps even 100.

But this **may depend on the OEM / ROM used by the device!** Some OEMs and ROMs may limit the amount of steps, or deny modification of the steps altogether, returning back to default values. Unless I can see the source code of the [AudioService.java](https://android.googlesource.com/platform/frameworks/base.git/+/master/services/core/java/com/android/server/audio/AudioService.java) file, I can't help you, unfortunately.

## How to use:
#### KernelSU Module
1. Download the [repository](https://github.com/alextecplayz/ksu-volume-steps/archive/refs/heads/main.zip) or the .zip file from the [Releases](https://github.com/alextecplayz/ksu-volume-steps/releases) tab, which might not always be up-to-date\
   1.1 IF you downloaded the repository, unarchive it, and archive only module.prop and system.prop as a .zip file, with normal compression.
2. Open the KernelSU app, tap on the Module tab, and tap on the Install button
3. Select the .zip file from Releases or the .zip archive you created
4. KernelSU will flash the archive. It should be nearly instantaneous, since it's a very small module.
5. After flashing is complete, you may restart the device.

#### Script
1. Download the [repository](https://github.com/alextecplayz/ksu-volume-steps/archive/refs/heads/main.zip) or the [script](https://github.com/alextecplayz/ksu-volume-steps/blob/main/volume-steps.sh)
2. Move ONLY the script (volume-steps.sh) to /data/adb/service.d/
3. Change the file permissions to 0755 (rwx r-x r-x) and set the owner and group to root\
   3.1. Start the ADB shell with `adb shell`\
   3.2. Gain Superuser access with `su`\
   3.3. Change file permissions with `chmod 0755 /data/adb/service.d/volume-steps.sh`\
   3.4. Change ownership and group to root with `chown root:root /data/adb/service.d/volume-steps.sh`
5. Restart the device

## Quirks, Issues
- It seems that any device restarts while the module is active may glitch out or set the volume levels for certain stream types to maximum, such as notifications, calls and system streams.
