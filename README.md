PKGBUILDs for I-PIPE and Xenomai
=================================

I'm totally unsure about any behavior of this installation procedure, but my
Xenomai app CAN compile with these PKGBUILDs.

The `PKGBUILD` (for I-PIPE patched kernel) is a fork of https://aur.archlinux.org/packages/linux-git/

### Installation Procedure
```sh
# build and install ipipe patched kernel
# change NN to the desired number of concurrent jobs
MAKEFLAGS='-jNN' makepkg -sri

# boot entry for xenomai kernel
# change NNNNN to your gid
cat - > sudo tee /boot/loader/entries/xenomai.conf << EOF
title	I-PIPE patched kernel
linux	/vmlinuz-linux-xenomai
initrd	/intel-ucode.img
initrd	/initramfs-linux-xenomai.img
options	root=PARTUUID=0d83a5cd-2827-408f-bfa1-4ab1e7e9ceb3 rw xenomai.allowed_group=NNNNN
EOF

reboot # into new kernel

# build and install xenomai library
# change NN to the desired number of concurrent jobs
MAKEFLAGS='-jNN' makepkg -p PKGBUILD.xeno -sri
```
