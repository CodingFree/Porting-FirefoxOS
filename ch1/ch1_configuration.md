# Prerequisites #
- An Android device supported in CyanogenMod 12.1.
- A computer or **virtual machine** with Ubuntu 14.04 LTS (or later) installed. You will need a **64-bit version of Ubuntu**. Ubuntu 14.04 is recommended.

# Set up your Ubuntu 14.04 LTS (or later) build system #
Since both Firefox OS and CyanogenMod use an AOSP base, it is (almost) enough to follow the [guide for AOSP](https://source.android.com/source/initializing.html) provided by Google.

For Gingerbread (2.3.x) and newer versions, including the master branch, a 64-bit environment is required. Since **Firefox OS requires at least Jelly Bean**, that means that you must not use 32 bits.

## Java 7: For the latest version of Android ##


    sudo apt-get update

    sudo apt-get install openjdk-7-jdk

## Installing required packages  ##


    sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip android-tools-fastboot android-tools-adb python

# Configuring GIT
Just remember to configure your user and email for Github:

    git config --global user.name "John Doe"
    git config --global user.email johndoe@example.com
    
## Configuring USB Access ##

### Configuration ###

Under GNU/Linux systems (and specifically under Ubuntu systems), regular users can't directly access USB devices by default. The system needs to be configured to allow such access.

The recommended approach is to create a file at /etc/udev/rules.d/51-android.rules (as the root user).

To do this, run the following command to download the [51-android.rules file](https://source.android.com/source/51-android.rules) attached to this site, modify it to include your username, and place it in the correct location. The following command will do it automatically:


    wget -S -O - http://source.android.com/source/51-android.rules | sed "s/<username>/$USER/" | sudo tee >/dev/null /etc/udev/rules.d/51-android.rules; sudo udevadm control --reload-rules

### Troubleshoots ###

If you want to test it, connect your Firefox OS:

Set the device to use USB Debug. First, you need to enable "Developer Options Menu":

1. Click Menu button to enter into App drawer.
2. Go to "Settings".
3. Scroll down to the bottom and tap "About phone" or "About tablet",
4. Scroll down to the bottom of the "About phone" and locate the "Build Number" field.
5. Tap the Build number field seven times to enable Developer Options. Tap a few times and you'll see a countdown that reads "You are now 3 steps away from being a developer."
6. When you are done, you'll see the message "You are now a developer!".
7. Tap the Back button and you'll see the Developer options menu under System on your Settings screen

s

- **Android 2.0-2.3.x**: Settings > Applications > Development > USB Debugging.
- **Android 3.0- 4.1.x**: Settings > Developer Options > USB Debugging.
- **Android 4.2.x and higher**: In Android 4.2 and higher versions, the Developer Options menu and USB Debugging option have been hidden. In former 4.X versions of Android, USB Debugging option is under Developer Options menu.
- **Android 5.0**: To enable USB Debugging on Android 5.0 Lollipop is the same as Android 4.2.x.


And run:


    adb shell

If you get a "**device not found**" error, your device is not included in that  51-android.rules file. To fix this, after connecting your device to a USB port throw the following command:

    lsusb

You will get something like this, with different name and values:

Bus 002 Device 059: ID 18d1:4e42 Google Inc.

For this example, 18d1 is the Manufacturer ID and 4e42 is the Model ID. Modify the file **/etc/udev/rules.d/51-android.rules** and add your device in a new line like this:

    SUBSYSTEM=="usb", ATTR{idVendor}=="18d1", ATTR{idProduct}=="4e42", MODE="0666", GROUP="plugdev"

**Change the idVendor and idProduct** with the values that you had in your lsusb command.

Eventually, to apply those rules to the system you have to restart the udev service:

    sudo service udev restart

### Warning ###
USB Debugging should only be enabled when you need it. Leaving it enabled all the time is kind of a security risk for that this mode grants you high-level access to your device. Say if you connect your Android phone to a USB charging port in a public location, the port could use the USB access to your phone to access data on your phone or install malware.

