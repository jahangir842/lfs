The command sudo update-grub (or sudo grub-mkconfig in some distributions) is used to regenerate the GRUB configuration file. This process updates the list of bootable operating systems and kernels available for selection during the boot process. Here's what happens step by step:


---

Step-by-Step Process

1. Find the GRUB Configuration File:

The command updates the GRUB configuration file, typically located at:

/boot/grub/grub.cfg (for legacy BIOS systems)

/boot/efi/EFI/grub/grub.cfg (for UEFI systems)




2. Scan for Bootable Entries:

The system scans all partitions for:

Installed Linux kernels in /boot (e.g., vmlinuz files).

Other operating systems (e.g., Windows, macOS).

Custom entries defined in /etc/grub.d/.




3. Parse Configuration Scripts:

GRUB uses scripts located in /etc/grub.d/ to build the configuration:

00_header: Sets up global GRUB settings (e.g., timeout, default entry).

10_linux: Detects Linux kernels on the system.

30_os-prober: Detects other operating systems like Windows.

Custom Scripts: Any user-defined scripts.




4. Generate a New GRUB Menu:

Based on the scan and parsed scripts, a new grub.cfg file is generated.



5. Apply Custom Settings:

Any customizations in /etc/default/grub are applied, such as:

Default boot entry (GRUB_DEFAULT).

Timeout duration (GRUB_TIMEOUT).

Boot parameters (e.g., quiet, splash).




6. Update Bootloader Behavior:

GRUB now reflects changes in boot entries, kernel updates, or configuration.





---

Common Scenarios for Running update-grub

1. Kernel Updates:

When a new kernel is installed, update-grub ensures it is added to the GRUB menu.



2. Installing Another OS:

After installing another operating system, running update-grub detects and includes it in the menu.



3. Custom GRUB Settings:

When you modify /etc/default/grub, running update-grub applies the changes.



4. Troubleshooting:

If the GRUB menu is missing or incorrect, update-grub can regenerate it.





---

Verifying GRUB Configuration

1. View Generated GRUB Menu:

cat /boot/grub/grub.cfg


2. Check Boot Entries:

grep -i menuentry /boot/grub/grub.cfg


3. Test GRUB Menu:

Reboot the system and verify the updated GRUB menu.





---

Potential Errors

1. os-prober Not Detecting Other OS:

Ensure the os-prober package is installed:

sudo apt install os-prober



2. No New Kernels Found:

Check if the kernel is properly installed in /boot.



3. Permission Denied:

Ensure you use sudo with the command.





---

Command Alternatives

Directly use:

sudo grub-mkconfig -o /boot/grub/grub.cfg

This is the underlying command update-grub invokes.



---

Summary

Running sudo update-grub regenerates the GRUB configuration to reflect the current state of the system's bootable kernels and operating systems. It is a crucial step after installing or removing kernels, modifying GRUB settings, or installing additional operating systems.

