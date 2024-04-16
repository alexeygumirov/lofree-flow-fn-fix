# Fix for the Lofree Flow keyboard Fn keys on Linux

The issue with the Lofree Flow keyboard is that it cannot recognize Linux system correctly.
This causes Fn keys behave only like media keys and switching to the Fn mode (Fn + Lock) does not work.

This little script allows to fix this issue every time it occures. In my case every time I switch off and switch on the Lofree Flow keyboard, it forgets the settings and I have to run this script again.

Script content:
```sh
#!/bin/sh

echo "Fixing Lofree Fn Mode"
echo
echo "Please swtich keyboard into the MacOS/iOS mode: Press Fn + M"
echo 
read -p "Press any key to continue... " PRESSKEY
echo
echo "Setting Lofree Fn Mode to 2"
sudo sh -c 'echo 2 > /sys/module/hid_apple/parameters/fnmode'
echo "Done!"
echo
echo "You can set keyboard back to Windows/Android mode by pressing Fn + N"
```
