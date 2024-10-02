# Connecting to Portenta X8 via USB

### 1. Download `adb` (Android Debug Bridge)

This tool, available for download [at this link](https://developer.android.com/tools/releases/platform-tools#downloads), will allow you to connect to the Portenta X8 over a USB connection. The download will contain a compiled binary program, so no installation is necessary.

If you are on Windows or Linux, you may need to extract the compressed file downloaded. On macOS this is usually automatic. If you extract this file to a different location than where you downloaded it, take note of the folder's location before heading into the next step.

### 2. Navigate into the folder downloaded

The downloaded folder should have a name like `platform-tools`. Using your operating system's terminal application (Windows: `PowerShell`, macOS & Linux: `terminal`), navigate into your `Downloads` folder, if that is where you keep your downloads, then into the `platform-tools` folder that you just downloaded in [step 1](#1-download-adb-android-debug-bridge).

>[!TIP]
>On most operating systems, terminal applications usually open in the home directory, which usually contains the `Downloads` folder. If you are new to using the terminal, try to open the terminal application and type in `cd Downloads`, followed by hitting the `ENTER` key on your keyboard. If this works, you will be able to also do `cd platform-tools`.

To verify that you have made it into the target directory, name the directory you are in with `pwd`, and see if the output ends with "[...]/platform-tools". Then, list the items in the directory you are in with `ls`, and make sure one of the items listed is called "adb".

### 3. Connect the Portenta X8 to your computer using a USB-C cable

The Portenta X8 will power on even if the USB-C connection is not entirely complete, so be sure the male USB-C connector to the Portenta is completely inside the female connector.

### 4. Use `adb` to access the Portenta X8
With steps [2](#2-navigate-into-the-folder-downloaded) & [3](#3-connect-the-portenta-x8-to-your-computer-using-a-usb-c-cable) completed, you should now be inside the folder you downloaded in [step 1](#1-download-adb-android-debug-bridge). That means, when you do `ls` to list the contents of the folder you are "in" in the terminal application, you see `adb` as one of the listed items.

Run this command to enter the Portenta X8 in your terminal application:

```bash
./adb shell
```

A successful connection will return output in the terminal, something like:

```bash
fio@dev-portenta-x8-123adbcd123:/home/fio $
```
This output means you are successfully logged into the Portenta X8's [shell](https://en.wikipedia.org/wiki/Unix_shell), where you can enter commands similar to how you do on your computer. If you do not get the above output, see [the troubleshooting for this section](#troubleshooting-step-4)

# Connecting the Portenta X8 to WiFi

### 1. Connect to the Portenta X8 from your computer
Connect to the Portenta X8 using `adb`, as seen in [this section](#connecting-to-portenta-x8-via-usb) of this file.

>[!NOTE]
> The Portenta X8's login shell has some odd text wrapping behavior when connected via `adb`. Text will jump behind other text when you are typing and format very odd. If you just type slowly and surely, the correct command, while not appearing quite right on the screen, will be executed properly. 

### 2. List the WiFi networks available.
Enter the following command, followed by `ENTER` on the keyboard, to view a list of the available WiFi networks as seen by the Portenta:

```bash
sudo nmcli dev wifi
```

>[!INFO]
>You may be prompted for a password, which by default, is `fio`.

You will then see the following:
```bash
WARNING: terminal is not fully functional
Press RETURN to continue 
```

After pressing return, the list will display like:
```bash
IN-USE  BSSID              SSID                              MODE   CHAN  RATE >
        30:23:03:FD:46:47  TelosAir                          Infra  3     130 M>
        32:23:03:FD:46:47  TelosAir-guest                    Infra  3     130 M>
        C4:41:1E:16:E9:1D  Potsdam Sensors 3rd Floor 2.4ghz  Infra  9     130 M>
        1A:47:3D:54:70:92  DIRECT-92-HP M182 LaserJet        Infra  9     130 M>
        6C:8B:D3:E9:A0:62  Ichor                             Infra  11    195 M>
        6C:8B:D3:E9:A0:60  eduroam                           Infra  11    195 M>
        6C:8B:D3:E9:A0:61  Ichor-Guest                       Infra  11    195 M>
        70:79:B3:80:72:62  Ichor                             Infra  6     195 M>
        70:79:B3:80:72:60  eduroam                           Infra  6     195 M>
        70:79:B3:80:72:61  Ichor-Guest                       Infra  6     195 M>
        78:0C:F0:39:5D:01  Ichor-Guest                       Infra  6     195 M>
        78:0C:F0:39:5D:02  Ichor                             Infra  6     195 M>
        20:3A:07:38:9F:C0  nexid                             Infra  11    130 M>
        78:0C:F0:39:5D:00  eduroam                           Infra  6     195 M>
        20:3A:07:38:9F:C1  pb_guest                          Infra  11    130 M>
        78:72:5D:B8:21:82  Ichor                             Infra  6     195 M>
        78:72:5D:B8:21:81  Ichor-Guest                       Infra  6     195 M>
        78:72:5D:B8:21:80  eduroam                           Infra  6     195 M>
        A0:93:51:9A:56:A2  Ichor                             Infra  1     195 M>
        00:5D:73:6B:64:40  eduroam                           Infra  11    195 M>
        00:5D:73:6B:64:42  Ichor                             Infra  11    195 M>
        A0:93:51:9A:56:A0  eduroam                           Infra  1     195 M>
```

Pressing `enter` will advance the list forward.
To exit the list, you can do `CTRL`+`C` or `q` `Enter`. 

If you do not see the `SSID` for the WiFi network you were looking for, you can ask the WiFi card to rescan the networks with this command:

```bash
sudo nmcli dev wifi rescan
```

Then, wait a moment before listing the networks again.

### 3. Connect to your WiFi network

To connect to your WiFi network, for example, `TelosAir`, with password `mypassword`, you will need to enter the command:

```bash
sudo nmcli dev wifi conn 'TelosAir' password mypassword
```

If this is unsuccessful, please check your spelling, wait a moment and try again. You may need to `rescan` again if you get an error regarding the SSID not being found.

You can exit the shell with this command:

```bash
exit
```


# Troubleshooting
## Connecting to Portenta X8 via USB
#### Troubleshooting Step 4
__1. "No devices/emulators found"__

If `adb` fails to find the device it is looking for, it will give this output when you run the `./adb shell` command in your terminal application:

```bash
adb: no devices/emulators found
```

This could happen for a variety of reasons:

__The Portenta X8 is not connected to your computer.__

Double check that the USB connection is completely made on both ends of the cable. Sometimes it helps to unplug the cable and try again.

__The Portenta X8 is not recognized by your computer.__

First, double check that you can see a USB device connected to your computer. You will need to find where you would see that sort of info on your computer.

For Windows:
>Open `Device Manager` on your computer and find the drop down regarding `COM Ports`.

For macOS:
>In the `terminal` app, do `ls /dev/cu.*` to list all of the potential devices recognized by your computer.

For Linux:
>In the `terminal` app, do `ls /dev/tty*` to list all of the potential devices. The Portenta would probbably be of the form `/dev/ttyACM*` or `/dev/ttyUSB*`.

Using one of the above methods for seeing a list of connected devices to your laptop, check with the Portenta X8 connected and again with it disconnected. If your laptop is able to recognize the Portenta X8 connection, you will see a device appear and disappear from the list when you do this.

If you do not see a device that appears and reappears with connection and disconnection of the USB-C cable to the Portenta X8, then your computer does not recognize the Portenta, either due to a lack of physical contact or something drivers related.

__The Portenta is in USB Mass Storage Mode__

Check to see in your operating system's file explorer application if you see a removable drive, like a USB flash drive. If so, the Portenta X8 is in USB mass storage mode, so you will not be able to use `adb`.

__2. Developer cannot be validated__

If the `adb` program's code-signing certificate is not recognized by your OS, it may not let you run the command, giving a warning about an inability to validate the program.

For macOS:

Un-quarantine the `adb` executable file with the following command, from within the folder containing `adb`:

```bash
xattr -d com.apple.quarantine ./adb
```
