# How it Works

## The Windows Portion

- Run the executable

- Check for saved progress (Probably in appdata directory)

- Check if running UEFI, if not then exit

- Collect Disk, partitions, their free space, and if bitlocker encrypted

- Ask if the user would like to wipe any disks that are not the primary one and/or reduce any including the primary

- After the changes does the user have a spot somewhere to add a partition of adequate size (we will say 500Mib for now), if not then exit

- Check for SecureBoot and TPM

  - If SecureBoot and/or TPM is enabled save progress up until before the check

  - Provide instructions on how to disable (Unless we can get shim to work)

- Attempt to make changes to the drives, if the changes fail then revert and exit

- On the ESP partition rename boot/bootx64.efi to /boot/bootx64.efi.bak

- Write new bootx64.efi file to ESP partition

- Create new fat partition (500Mib) with label ddi

- Write linux image/initramfs to ddi partition

- Reboot

It will then use the new bootloader to boot the new kernel/initramfs and begin the installer  
