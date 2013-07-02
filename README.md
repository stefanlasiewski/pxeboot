pxeboot

This is a test repo.

This repo provides configuration files to provide a pxeboot environment on Enterprise Linux, using either:
- dnsmasq to provide DHCP & TFTP services
- dhcpd for DHCP services and in.tftpd (e.g. tftpd using xinetd) 

If using dnsmasq, remember to disable dhcpd & xinetd/in.tftpd; and visa-versa.

Two things to remember:
- Configure iptables to allow access to the DHCP & TFTP ports
- selinux may interfere with tftp, so be aware. For testing, you may want to disable selinux.

My test environment is using VMWare Fusion.
