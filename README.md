# fix-bricked-redmi-note-9

A how-to guide of restoring a completely bricked Redmi Note 9​

Hi, In this guide, I will teach you how to fix a hard-bricked Redmi Note 9 (merlin) and bring it back to its original state.
How does a hard-bricked Redmi Note 9 look like? it's stuck in an infinite boot loop showing only the Redmi logo,
Can't access recovery with power+vol down, can't enter fastboot, can't connect it to a computer either.
If this is your phone here's how you can solve it without the need for service.

Following this guide keep in mind that everything would be erased from your phone including custom Recovery or ROM obviously. Also the bootloader would get locked again.
(I mean at this point you either have a useless brick or a working phone, you are choosing).

This is tested by me, and it works as long as you follow the steps carefully and you don't skip anything.
(I did this on Windows 10 btw)

    You gonna need to download, Python and the official Xiaomi fastboot image for Redmi Note 9. Also the zip file I'm attaching bellow. the zip file contains the MTK Drivers, SP Flash Tool, and some additional scripts like MI auth bypass etc,
    Get thefastboot image from here select your version (I picked the latest global) click download scroll down where it says "type:fastboot" and click "download: full Rom" the file name should look like this "merlin_images....tgz" or "merlin_global_images....tgz", etc, NOT miui_Merlin.zip,
    Get python from the official website site, I tested it with 3.9.7 but the latest version should work fine. Now, you have all the necessary files to start.
    Let the phone's battery die so the boot looping completely ends. (else you'll get error STATUS_EXT_RAM_EXCEPTION (0xC0050005) when using SP Flash Tool). ( I also tried it with a full battery and still worked so idk for sure how necessary this step is).
    Install Python select the "add to PATH" option, you can test if it was installed correctly by opening cmd and writing "python" or "py" it should output the python version.
    Extract the attached zip file and the fastboot image each into their folders.
    Enter the MTK Driver folder Install the MTK Driver for MTK SP flash tool.MTK_Driver_Auto_Installer_SP_Drivers_20160804.exe, Reboot your computer.
    Enter the python folder, run the "install pyusb pyserial json5.bat" when it's done close the terminal.
    Enter the driver folder, this folder contains a USB to COM driver for MTK Devices, right-click the "cdc-acm.inf" click install.
    Enter the libusb folder, run the libusb-win32-devel-filter-1.2.6.0.exe file, click next,next...install, when it's done it would prompt you to launch "filter installer wizard" click finish, when the wizard shows up, select "Install a device filter" it would show you your connected USB devices,
    Get your phone and a USB cable, connect the USB cable to your computer,while holding the volume up button on your phone connect your phone to the computer (Based on community feedback you might need to hold both up and down volume buttons AND power button!) once your phone turns on you would see your phone listed as "MediaTek USB Port" at the libusb filter installer before your phone reboots click at the "MediaTek USB Port" and then click install if you don't do it on time, your phone will get disconnected because of rebooting, try again re-plugging your phone. once you click install, You should get a pop-up message saying "...device filter successfully installed for MediaTek USB port..." click ok and exit, then remove your phone from the computer.
    Enter the bypass folder (This folder contains scripts to bypasses the Mi auth) double click the "1ST RUN THIS.bat" when it says "waiting for device" hold volume up and plug your phone into the computer (btw: You can let the button when it's recognized by the script). now most likely it would say "RuntimeError: unexpected output, expected 0xfd got 0xfe", if it does close the script and disconnect your phone, Try the "2ND RUN THIS.bat" when it shows "Waiting for device" hold volume up and connect your phone to the computer, wait till the console recognizes your phone, (At this part it might take few tries to make it work, try reconnecting your phone without holding any buttons or try holding volume down while reconnecting your phone) Once it gets recognized it would output "Found port = COM3" and Protection disabled. At this part your phone has stopped boot looping which is good but, DO NOT TOUCH YOUR PHONE, DO NOT DISCONNECT IT FROM THE COMPUTER, set your phone aside, and continue with the guide.
    Enter the SP Flash Tool folder run the flash_tool.exe at the Download-Agent click choose and select the DA_6765_6785_6768_6873_6885_6853.bin file which is included in the SP flash tool folder.
    At the Authentication File, click choose and select the auth_sv5.auth included in the SP flash tool folder.
    At the Scatter-loading File, click choose, go to the fastboot image extraction folder (Step 4) then enter the images folder and select the MT6768_Android_scatter.txt file (Fastbootimage/images/MT6768_Android_scatter.txt)
    On the drop-downbox below the "Authentication File" label change the option from Download Only to Firmware Upgrade.
    At the toolbar above click Options -> Option... go to Connection check the UART option and set the Baud rate to 921600, make sure the com port option is set to com 3, then close the window.
    Click Download with the green arrow, now wait till it finished flashing your phone this would take quite of time, at this part DO NOT TOUCH ANYTHING LET IT FINISH TO AVOID ANY CURROPTION ON YOUR PHONE. (If you get "Error : STATUS_STOR_LIFE_EXHAUST" go to options-> general and uncheck Storage life cycle check).
    When it's done it would show you a pop-up window "Download Ok" with a green background and a checkmark, click the X to close, and now you can also close the SP Flash tool app.
    Disconnect your device from your computer and press the power buttonto start your phone, connect it to a charger or back to the computer since there was no charge so it won't die suddenly now.
    Your phone now should boot normally showing the MIUI logo, because its first boot it would take few minutes for the phone to boot, wait patiently and you would see the "first setup" screen.
    That's it! You successfully brought back to life a hard-bricked Redmi Note 9 (merlin). A huge weight now has lifted from you :) hf.
