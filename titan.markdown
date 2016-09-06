% TITAN(1) Titan Installation Manual
% Matteo Ragni
% September 6, 2016

# Name

sci-titan.unitn.it - workstation for deep learning

# Installation

**sci-titan.unitn.it** is a workstation built for Deep Learning GPU algorithms.
It is configured with:

 * Asus x99-E WS Motherboard
 * i7-59xxk processor liquid cooled
 * 2 x NVIDIA GeForce Titan X 12GB DDR5
 * 32GB DDR4 High Performance RAM kit
 * 512GB V-NAND SSD drive (with OSes) - on M.2 SATA connection
 * 250GB SSD drive (raid caching) - on SATA0_GRAY port
 * 2 x 2TB HDD in RAID0 (4TB total) with Intel Rapid Storage caching - on SATA1_GRAY and SATA2_GRAY port

and the availabel OSes are:

 * Windows 10 Pro
 * Gnome Ubuntu 16.04 LTS (default)

# Installation

The trickiest part of the workstation is for sure the installation of the
Intel Rapid Storage Technology drivers and the configuration of the
RAID0 with the acceleration enabled.

If you are going to install the system from scratch you will need:

 * a UEFI compatible USB stick with Windows 10 Setup
 * a UEFI compatible USB stick with Ubuntu 16.04 LTS

## Preparing Windows 10 Installer Drive

There are plenty of guides on-line on how to create an installation drive
for Windows. When you have created your drive, please download the **f6flpy-x64.zip**
driver from the Intel Rapid Storage Technology web site
(https://downloadcenter.intel.com/product/55005/Tecnologia-Intel-Rapid-Storage).
You have to unzip the driver directly in the root of the stick, since it must be
loaded during partitioning.

All HDDs and SSDs partitions must be cleared (uninitialized space).

Failing this will lead to an un-bootable Windows.

## Configuring UEFI (BIOS)

UEFI must be configured for support the Intel Rapid Storage Technology (RST) **before**
intalling OSes. This configurations allows also to install Windows 7 instead of Windows 10 (not tested).

Access UEFI configuration utility with _DEL_ key, select the **Optimized Defaults** preset in EZ-view. and access the advanced configuration interface (_F7_):

 * Advanced / PCH Storage Configurations / SATA Mode = **RAID** (if Windows was installed with this configuration set to AHCI, it must be installed again)
 * Boot / SATA Support / **All Devices**
 * Boot / Secure Boot / **Disable**
 * Boot / Secure Boot / **Other OS**
 * Boot / Secure Boot / Boot Keys / **Clear Secure Keys**
 * Boot / CSM / **Enable**
 * Boot / CSM / Boot Device control / **UEFI only**
 * Boot / CSM / Boot From Network Devices / **UEFI driver first**
 * Boot / CSM / Boot From Storage Devices / **UEFI driver first**
 * Boot / CSM / Boot From PCI-E/PCI Expansion Devices / **UEFI driver first** (fundamental to boot from M.2 drives)

Press _F10_ to save and exit UEFI setup. Insert the Windows 10 Installer drive before reboot.

## Configuring RAID0

UEFI setup has enabled Intel Raid Setup Utility, advertised with a blank screen with all connected drive listed. To access the interactive menu press the combination _CTRL+I_. Using menu of configuration utility, build a new drive volume:

 * Name: **Storage**
 * RAID Level: **RAID0**
 * Disks: Select using _Space_ the two 2TB HDDs, confirm with _Enter_
 * Strip size: 128KB
 * Capacity: (auto configured)
 * Sync: (not available)

Create the volume, and continue with the boot process to Windows installation. Do not worry about the Acceleration grayed link. It will be activated later.

## Installing Windows 10

**Remember to boot always from UEFI partition of the installation drives**. Configure the languages of the installation and the regional settings, then proceed to drive partitioning.

**Before initialize** the volumes, select 512GB drive and click on **Driver** link. This will lead to a procedure to select the Intel RAID driver (select the Intel F6 extracted directory, click Next, select the only voice available and Continue). Failing this procedure will lead to an un-bootable system.

Create a **1GB uninitialized partition** (will be used for boot of Ubuntu later). Create another partition for windows installation (suggested **100GB**). Windows will automatically create other partitions for recovery and boot purposes. Complete the installation. **Do not initialize RAID volume and 256GB volume**.

## Configuring Caching in RST

Once completed Windows setup, login and complete driver installation, using:

 * MEI Chipset Driver (https://www.asus.com/Motherboards/X99E_WS/HelpDesk_Download/)
 * Turbo Boost Driver (https://www.asus.com/Motherboards/X99E_WS/HelpDesk_Download/)
 * Chipset Driver (https://www.asus.com/Motherboards/X99E_WS/HelpDesk_Download/)
 * nVidia GeForce Driver - series 10 (http://www.nvidia.com/Download/index.aspx)

and install the RST utility (**SetupRST.zip**) from https://downloadcenter.intel.com/product/55005/Tecnologia-Intel-Rapid-Storage. If everything was setup correctly, in the utility it is possible to enable the performance option: _accelerate using solid state driveres:_ **Enable**. The acceleration will use **64GB** from the 256GB SSD on SATA0_GRAY channel. To actually see the interface reflect the settings **a reboot is mandatory**.

After the reboot, the RST utility will reflect the acceleration state. Also, in the RAID setup, the acceleration menu will finally be enabled.

## Installing Ubuntu 16.04 LTS

Now it is time to install the main operating system.
