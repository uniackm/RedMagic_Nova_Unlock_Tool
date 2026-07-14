 RedMagic Nova Tablet (NP03J) Bootloader Unlock Tool

A clean, self-contained tool package to unlock the bootloader of the **RedMagic Nova (NP03J)** gaming tablet. This tablet is equipped with the Snapdragon 8 Gen 3 Leading Version (`sm8650_v2`) processor.

## Prerequisites

Ensure the following tools are installed on your Linux system:
*   `adb` and `fastboot` (Android Platform Tools)
*   `edl` (Qualcomm Sahara/Firehose EDL client, typically `bkerler/edl`)
*   `lsusb` (to verify device connection state)
*   `pkexec` (PolicyKit helper used to execute the EDL client with root permissions for direct USB device bus communication)

## Directory Structure

```
RedMagic_Nova_Unlock_Tool/
├── bin/
│   ├── abl_eng_v2.img                         # Patched engineering ABL v2 image
│   ├── frp_unlock.img                         # Partition configuration for FRP bypass
│   ├── misc_wipedata.img                      # Command payload to trigger wipe
│   └── prog_ufs_firehose_sm8650_v2_ddr.elf    # Authentic Qualcomm Firehose loader for SM8650 v2
├── backups/                                   # Partitions backed up during Step 1 are stored here
├── unlock_tool.sh                             # Interactive script script
└── README.md                                  # Instructions manual
```

## How to Use

Run the interactive menu script from the root directory:
```bash
./unlock_tool.sh
```

### Step 1: Flash Engineering ABL
1. Turn off your tablet.
2. Hold **Volume Up + Volume Down + Power** simultaneously, and connect the USB cable to your PC. The screen will remain black (EDL Mode).
3. Select **Option 1** (`Step 1: Backup and Flash Engineering Bootloader (EDL Mode)`) in the script menu.
4. The tool will:
   * Backup your stock `abl_a`, `abl_b`, and `frp` partitions to the `backups/` directory.
   * Write the patched engineering bootloader to the device.
   * Reboot your tablet into Fastboot mode automatically.

### Step 2: Confirm Bootloader Unlock
1. Once the tablet reboots and displays the Fastboot menu screen, select **Option 2** (`Unlock Command (Fastboot Mode)`) in the script menu.
2. Confirm the bootloader unlock on the tablet's screen by using the physical volume keys to navigate to **"Unlock the bootloader"** and pressing the Power key.

### Step 3: Restore Stock Bootloader (Recommended)
Running the engineering bootloader permanently can cause stability or OTA update issues. Once unlocked, it is recommended to restore your stock partitions.
1. Turn off the tablet or boot it back to EDL mode (Volume Up + Volume Down + Power while plugging in USB).
2. Select **Option 3** (`Step 2: Restore Stock Bootloader and Wipe Data (EDL Mode)`) in the script menu.
3. The tool will:
   * Restore your original stock `abl_a`, `abl_b`, and `frp` partitions from your backups.
   * Flash the factory reset instruction to your `misc` partition to finalize the unlock process.
   * Reboot the tablet. It will boot into Android with a fully unlocked bootloader.
