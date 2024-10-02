# Connecting to Portenta X8 via USB

### 1. Download `adb` (Android Debug Bridge)

This tool, available for download [at this link](https://developer.android.com/tools/releases/platform-tools#downloads), will allow you to connect to the Portenta X8 over a USB connection. The download will contain a compiled binary program, so no installation is necessary.

### 2. Navigate into the folder downloaded

The downloaded folder should have a name like `platform-tools`. Using your operating system's terminal application (Windows: `PowerShell`, macOS & Linux: `terminal`), navigate into your `Downloads` folder, if that is where you keep your downloads, then into the `platform-tools` folder that you just downloaded in step 1.

[!TIP]
On most operating systems, terminal applications usually open in the home directory, which usually contains the `Downloads` folder. If you are new to using the terminal, try to open the terminal application and type in `cd Downloads`, followed by hitting the `ENTER` key on your keyboard. If this works, you will be able to also do `cd platform-tools`.

To verify that you have made it into the target directory, name the directory you are in with `pwd`, and see if the output ends with "[...]/platform-tools". Then, list the items in the directory you are in with `ls`, and make sure one of the items listed is called "adb".