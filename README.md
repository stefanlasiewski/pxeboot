pxeboot

This is a test repo.

This repo provides configuration files to provide a pxeboot environment on Enterprise Linux, using either:
- dnsmasq to provide DHCP & TFTP services
- dhcpd for DHCP services and in.tftpd (e.g. tftpd using xinetd) 

If using dnsmasq, remember to disable dhcpd & xinetd/in.tftpd; and visa-versa.

Both dnsmasq & dhcpd/in.tftpd can with with either iPXE or pxelinux.0 . Just drop or modify the appropriate configuration files.

Two things to remember:
- Configure iptables to allow access to the DHCP & TFTP ports
- selinux may interfere with tftp, so be aware. For testing, you may want to disable selinux.

My test environment is using VMWare Fusion and Parallels on a Mac. I disabled the native DHCP server for the 'Host-only' network for each VM provider, and am using dnsmasq or dhcpd on a Virtual Machine to provide DHCP services for the 'Host-only' network.

# Instructions (DRAFT)

## dnsmasq instructions:

dnsmasq requires the newer syntax changes provided in dnsmasq 2.53 and above, which is newer then the default version provided with RHEL6, CentOS6, SL6. Many solutions that I found on the internet use the older syntax, or a hybrid of the older & newer syntax.

1. Install dnsmasq

This test system runs Scientific Linux 6.x (Similar to RHEL6) on a Parallels or VMware FUsion VM. You'll see the standard Parallels & VMware networks down below.

1. Install dnsmasq 2.53 or newer. For Enterprise Linux-based distros, Repoforge provides a newer version. Install Repoforge per the instructions at http://repoforge.org/use/

2. (optional) Make a quick edit to /etc/dnsmasq.conf to 'include' files under /etc/dnsmasq.d/ .

Old:
	# Include a another lot of configuration options.
	#conf-file=/etc/dnsmasq.more.conf
	#conf-dir=/etc/dnsmasq.d

New:

	# Include a another lot of configuration options.
	#conf-file=/etc/dnsmasq.more.conf
	conf-dir=/etc/dnsmasq.d

3. Drop the files dnsmasq-global-settings.conf & ipxe.conf into /etc/dnsmasq.d , or else append the changes ot /etc/dnsmasq.conf . Modify the files to suit your needs. In particular, you will probably need to change the IP addresses to suit your environment.

## DHCP & in.tftpd instructions:


To be written:

## For either dnsmasq or DHCP/in.tftpd: 

1a. If using iPXE, drop undionly.kpxe into /var/lib/tftpboot , and be sure the permissions are correct. Follow the instructions for 'chainloading' at ipxe.org
2b. If using pxelinux, install the pxelinux RPM, and copy pxelinux.0 and menu.c32 (for menus) into /var/lib/tftpboot. Then create the menu file under /var/lib/tftpboot/pxelinux.cfg/default . See  http://wiki.centos.org/HowTos/PXE/PXE_Setup

