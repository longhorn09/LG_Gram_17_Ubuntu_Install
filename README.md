# Installing Ubuntu on LG Gram 17 (2019)
Setup instructions to facilitate installation of Ubuntu on LG Gram 17.

Performed with Ubuntu Budgie 19.10 on a [LG 17Z990-R.AAS7U1](https://www.lg.com/us/laptops/lg-17Z990-RAAS7U1-ultra-slim-laptop) installed on a SATA SSD.

1. At boot, spam F2 to enter BIOS
2. Find security settings in the BIOS under the Security tab and click on Secure Boot Configuration
![security_secure_boot](https://user-images.githubusercontent.com/11417589/68453883-76648500-01bc-11ea-8323-b20f4b9d9f0c.jpg)
3. Disable secure boot
![secure_boot_disabled](https://user-images.githubusercontent.com/11417589/68453931-998f3480-01bc-11ea-9168-485868cc6579.jpg)
4. Modify boot order to prioritize USB drive. This step assumes you've made a bootable USB drive with an Ubuntu distribution. If you haven't made a bootable USB drive from an ISO, try [Rufus](https://rufus.ie/).
![boot_priority](https://user-images.githubusercontent.com/11417589/68453882-75cbee80-01bc-11ea-8eb1-7fd458d1bf73.jpg)
5. Save and exit the BIOS, upon reboot spam e, and make sure to add 
```pci=nommconf```  before ```quiet nosplash```
![edit_nom](https://user-images.githubusercontent.com/11417589/68453881-75cbee80-01bc-11ea-8ca3-ccc04aed4624.jpg)
6. At this point, you should be in the normal Ubuntu installation sequence. Install Ubuntu. 
7. Upon reboot after initial Ubuntu installation, to get back into the OS you will likely need ```pci=nommconf``` by spamming e
![edit_nomm2](https://user-images.githubusercontent.com/11417589/68453880-75cbee80-01bc-11ea-9da0-28ab7c39fb15.jpg)

8. Finally once logged into Ubuntu, modify the boot permanently with your editor (vim, nano, etc)

```bash
vim /etc/default/grub
```
```bash
GRUB_DEFAULT=0
GRUB_TIMEOUT_STYLE=hidden
GRUB_TIMEOUT=0
GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
GRUB_CMDLINE_LINUX_DEFAULT="pci=nommconf quiet splash"
GRUB_CMDLINE_LINUX=""
```

After adding `pci=nommconf` before `quiet splash` then save changes and afterwards run

```bash
sudo update-grub
```

At this point, you should be good to go and never have to bother with the ```pci=nommconf``` setting again. 

# References
[Useful reference](https://zieba.dev/linux/laptop/lg/gram/2019/07/27/lggram17.html)
