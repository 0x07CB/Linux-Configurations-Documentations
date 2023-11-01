# RAID Configurations on Linux
#SECURITY #RAID #Linux #Debian #RAID0
#Debian-Based #RAID Array# #How To# #System Administration#
- - -
### **Credits:**
* **Authors:** *0x07cb* [**Rick Sanchez**](https://github.com/0x07cb)
- - -
### ⚠️ **Warning** ⚠️
> _Please note that **the availability and compatibility of these instructions inside this documentation** to make configurations and administration of computers **may vary depending on your Linux distribution/Other Platforms, architecture and version.**_ 
> _It **is recommended to consult the documentation** or **official websites of the respective modules** for more details on their **usage** and **configuration**._
> …— **R**_ick_ **S**_anchez_  [ *D-634* ]
- - -

## Made an RAID Array
1. **How To: Preparing an Disk to be used with a _Full-Disk Encryption_.**
2. **How To: Preparing an Disk to be used in an _RAID Array_.**
3. [**How To: Made an *RAID0* with madam**](%23%5B%5BMade%20an%20RAID0%20with%20madam%5D%5D)


- - -
>  **Step 3 :** ~Made an RAID Array~
### [[Made an RAID0 with madam]]

> *To make a **Debian Linux** **operating system** **bootable** on a system disk using **RAID0** with **`mdadm`** and **USB flash drives**, follow these steps:*

1. **Prepare the USB flash drives**:
> On **Debian-Based Linux**:
* Insert all three **USB flash drives** into your computer.
- **Identify** the device names assigned to **each USB driv**e (e.g., /dev/sdb, /dev/sdc, /dev/sdd). You can use the `lsblk` or `fdisk -l` command to list the devices and their partitions.
  
2. **Install mdadm**:
> On **Debian-Based Linux**:
* Open a terminal and ensure you have `mdadm` installed. If not, install it by running the command:
  ```bash
  sudo apt-get install mdadm
  ```


3. **Create the RAID Array**:
> On **Debian-Based Linux**:
* Run the following command to create the **RAID0** array:
  ```bash
  sudo mdadm --create /dev/md0 --level=0 --raid-devices=3 /dev/sdXX
  ```
  
  Replace `/dev/sdXX` with the actual device names of your **USB flash drives**. This command creates a **RAID0** array called `/dev/md0` using the three **USB drives** first partitions.

4. **Format the RAID Array:**
> On **Debian-Based Linux**:
- Format the newly created **RAID** array with a file system of your choice (e.g., **ext4**). Run the command:
  ```bash
  sudo mkfs.ext4 /dev/md0
  ```

5. **Mount the RAID Array:**
> On **Debian-Based Linux**:
- Create a mount point directory where you want to mount the **RAID array**. For example:
  ```bash
  sudo mkdir /mnt/raid0
  ```
- Mount the **RAID array** to the mount point:
  ```bash
  sudo mount /dev/md0 /mnt/raid0
  ```

6. **Install Debian Linux:**
> On **Debian-Based Linux**:
- Proceed with the Debian **Linux installation** as you would on any other system.
- When prompted to select the installation destination, choose the manually partition option.
- Select the **RAID arra**y (/dev/md0) as the target for installation.
- Continue with the installation process, configuring partitions, etc.

7. **Install the bootloader:**
> On **Debian-Based Linux**:
- After the installation is complete, *you need to install the bootloader* (**GRUB**) on the **RAID array**. Run the command:
  ```bash
  sudo grub-install /dev/md0
  ```

8. **Update mdadm configuration:**
> On **Debian-Based Linux**:
- To ensure the **RAID array** is assembled at boot, update the **mdadm configuration file**. Run the command:
  ```bash
  sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
  ```

9. **Update initramfs:**
> On **Debian-Based Linux**:
- Update the initramfs to include the **RAID array** configuration. Run the command:
  ```bash
  sudo update-initramfs -u
  ```

10. Reboot:
> On **Debian-Based Linux**:
* Safely eject the **USB flash drives**.
* **Reboot** the system:
  ```bash
  sudo reboot
  ```

   
- - -
> Upon reboot, the system should boot from the **RAID0** array created using the **USB flash drives**. Ensure that your system's **BIOS** or **UEFI** is set _to boot from the **RAID array** as the **primary boot device**._

> **Note:** ***Booting from a RAID0 array** using **USB flash drives may not provide the best performance** and **reliability** compared to **using dedicated hard drives** or **solid-state drives**.*
- - -

- - -
