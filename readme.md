# EFI Lock Bypass (Intel Macs with T2)

⚠️ **Read this at your own risk!**

The information here is based on my own research and limited reverse engineering skills.

It may contain mistakes, be partially or completely wrong — **DYOR** before trusting anything!

## What is EFI Lock?

EFI lock is a restriction that appears when a Mac is marked as **Lost** via Apple’s *Find My* protocol or when a firmware password is set.

In this state, the Mac will boot only into recovery mode and display a **6-digit passcode screen** (Lost mode) or the boot device selection will be locked with the firmware password.

## Why This Works

On Intel Macs with a T2 chip, EFI configuration and boot policies are stored in **NVRAM**.

By removing the stored NVRAM snapshot and forcing regeneration, the lock state is cleared.

This effectively removes the EFI lock, allowing macOS to boot normally (given you have the user password).

## How to

1. Boot into a T2 SSH ramdisk
2. Mount the T2 subsystem disks
3. Delete the file:
    
    ```bash
    rm -rf /var/db/NVRAM_NEW.snapshot
    # or 
    rm -rf /mnt2/db/NVRAM_NEW.snapshot
    ```
    
4. Trigger regeneration:
    
    ```bash
    MacEFIUtil -r
    ```
    
5. Reboot.

After reboot, the system will no longer be stuck in recovery mode.

## Disclaimer

- This guide is for **educational purposes only**.
- Do **not** use this for illegal activities.
- Apple may patch this behavior at any time.

© 2025 \~ Hana Kim
