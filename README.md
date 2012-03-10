# Maven Android Scala Prototype #
This setup works. We use it with multiple clients.

## Setup ##
- Install JDK 1.5+.
- Install the Android SDK.
- Install Maven 3.0.3+.
- Set the ennvironment variable `$ANDROID_HOME` to the path of your Android SDK.
- Add `$ANDROID_HOME/tools` and `$ANDROID_HOME/platform_tools` to your `$PATH`.
- Launch the SDK Manager with `android` and install the "SDK Platform" under Android 2.2 ("Froyo"). Restart the SDK manager if prompted.
- Launch SDK Manager with `android` and create an emulator. Start the emulator.

## Compile & Run on Attached Device or Running Emulator ##

    $ git clone https://github.com/comb/maven-android-scala-prototype.git
    $ cd maven-android-scala-prototype
    $ mvn clean install android:deploy
    
Once that is done, open the app drawer on the emulator and launch the "Maven Android Scala Prototype" app.

## Help ##

    $ mvn android:help

## Improvement ##
I'm trying to figure out how to:

- Avoid running ProGuard during development mode
- Reduce the jar search path to avoid all the duplicate jars that ProGuard wastes time on
- Integrate ProguardCache (banshee/ProguardCache)
- Introduce multiple modes, one for development and one for deploy
- Specify the key to sign with

If you can do any of these things, please send me a pull request on GitHub.

## Troubleshooting ##

### Device permissions ###
On recent versions of Ubuntu you may get a permission denied error 
trying to develop with a physical phone. You will also see this in sbt:

     $ adb devices
     List of devices attached 
     ????????????    no permissions

To solve this problem, create the file `/etc/udev/rules.d/51-android.rules` and
paste these contents:

    SUBSYSTEM=="usb", SYSFS{idVendor}=="0bb4", MODE="0666"
    SUBSYSTEM=="usb", SYSFS{idVendor}=="22b8", MODE="0666"
    SUBSYSTEM=="usb", SYSFS{idVendor}=="18d1", MODE="0666"
    SUBSYSTEMS=="usb", ATTRS{idVendor}=="18d1", ATTRS{idProduct}=="0c01",
    MODE="0666", OWNER="[me]"
    SUBSYSTEM=="usb", SYSFS{idVendor}=="19d2", SYSFS{idProduct}=="1354", MODE="0666"
    SUBSYSTEM=="usb", SYSFS{idVendor}=="04e8", SYSFS{idProduct}=="681c", MODE="0666"

Then run `sudo service udev reload`, unplug and replug the device, and things should work:

     $ adb devices
     List of devices attached 
     015A7A370900601C         device

## Contact ##

- If you have questions, I suggest you email the scala-on-android Google group (https://groups.google.com/forum/?fromgroups#!forum/scala-on-android) and CC me.
- yuvi@combinatory.net
- http://combinatory.net
- http://yuvimasory.com

