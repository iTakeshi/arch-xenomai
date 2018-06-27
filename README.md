PKGBUILD for I-PIPE and Xenomai
=================================

Automated installation of I-PIPE kernel and Xenomai-3.

The `PKGBUILD` is a fork of https://aur.archlinux.org/packages/linux-git/.

### Installation Procedure
```sh
# build and install ipipe patched kernel
# change NN to the desired number of concurrent jobs
MAKEFLAGS='-jNN' makepkg -sri

# boot entry for xenomai kernel
# change NNNNN to the gid for `xenomai` group
cat - > sudo tee /boot/loader/entries/xenomai.conf << EOF
title	I-PIPE patched kernel
linux	/vmlinuz-linux-xenomai
initrd	/intel-ucode.img
initrd	/initramfs-linux-xenomai.img
options	root=PARTUUID=0d83a5cd-2827-408f-bfa1-4ab1e7e9ceb3 rw xenomai.allowed_group=NNNNN
EOF

reboot # into new kernel
```
