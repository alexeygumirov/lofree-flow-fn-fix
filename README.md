# Fix for the Lofree Flow keyboard Fn keys on Linux

The issue with the Lofree Flow keyboard is that it cannot recognize Linux system correctly.
This causes Fn keys behave only like media keys. And it does not allow switching to the Fn mode (Fn + Lock).

## Fix 1: persistent

This method provides you ability to keep this config persistent on your Linux system.
If you use Lofree via USB cable or via Bluetooth connection - this configuration fixes both.

What is needed - to create a file in the `/etc/modprobe.d` directory and add an option to set for the keyboard. This option will be applied on every system boot.
E.g. file name is `20_lofree_fn_mode_fix.conf`

```sh
echo "options hid_apple fnmode=2" | sudo tee /etc/modprobe.d/20_lofree_fn_mode_fix.conf
```

## Fix 2: script (non-persistent)

This script fixes issue but only for the current connection. You shall run this script every time you boot your system or connect/reconnect your keyboard.

This script just changes the Fn mode directly in the keyboard parameters file: `/sys/module/hid_apple/parameters/fnmode`.
- Value **1** means Fn lock is off: default action of the F1, F2, ... keys is media control.
- Value **2** means Fn lock is on: default action of the function keys is a standard function key action (F1, F2...F12). And media control works by pressing Fn + F1, Fn + F2, and so on.

## How to use

1. Download script file: `wget https://raw.githubusercontent.com/alexeygumirov/lofree-flow-fn-fix/main/lofreemodefix`
2. Make it executable `chmod +x lofreemodefix`.
3. Run it: `./lofreemodefix`

Or just make your own script file with the same content:

```sh
#!/bin/sh

echo "Fixing Lofree Fn Mode"
echo
echo "Please switch keyboard into the MacOS/iOS mode: Press Fn + M"
echo 
read -p "Press any key to continue... " PRESSKEY
echo
echo "Setting Lofree Fn Mode to 2"
sudo sh -c 'echo 2 > /sys/module/hid_apple/parameters/fnmode'
echo "Done!"
echo
echo "You can set keyboard back to Windows/Android mode by pressing Fn + N"
```

Make it executable and run it.
