 RedMagic Nova Tablet (NP03J) Bootloader Unlock Tool

 DISCLAIMER OF LIABILITY AND USE AT YOUR OWN RISKBy choosing to modify the operating system, firmware, or internal software of your smartphone or tablet, you acknowledge and agree to the following terms:No Liability for Damages: You assume total responsibility and all risks associated with any modifications performed on your device. The provider/author of these instructions shall not be held liable for any direct, indirect, incidental, or consequential damages—including, but not limited to, bricked devices (permanent hardware failure), boot loops, or software malfunction.Warranty Voidance: Modifying your device's core software will almost certainly void your manufacturer and carrier warranties. Any repairs, whether hardware or software-related, may be refused or subject to out-of-pocket costs.Risk of Data Loss: Modifying software can require wiping user data. You are solely responsible for securely backing up all your personal data, contacts, photos, and files prior to attempting any modifications.Loss of Functionality: Certain security-sensitive features (such as banking applications, digital wallets, secure corporate email, or biometric authentications) may cease working, even after a successful modification. You may also lose access to official over-the-air (OTA) software updates from your manufacturer.Modifications are performed strictly AT YOUR OWN RISK. If you are uncomfortable with the risks or do not fully understand the procedures, it is highly recommended to seek professional assistance or refrain from making alterations to your device.

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
