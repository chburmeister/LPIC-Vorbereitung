# Wichtige Dateien, Verzeichnisse, Anwendungen

## Verzeichnisse und Dateien

### /lib/modules 
* Ablage des/der Kernels
```
cb@w3qh:~$ ll /lib/modules/
insgesamt 28
drwxr-xr-x  7 root root 4096 Mai 19 08:01 ./
drwxr-xr-x 23 root root 4096 Mär 31 14:46 ../
drwxr-xr-x  5 root root 4096 Feb 15 21:35 4.8.0-36-generic/
drwxr-xr-x  6 root root 4096 Apr  2 19:37 4.8.0-45-generic/
drwxr-xr-x  6 root root 4096 Apr  6 08:31 4.8.0-46-generic/
drwxr-xr-x  6 root root 4096 Apr 26 09:59 4.8.0-49-generic/
drwxr-xr-x  6 root root 4096 Mai 19 08:02 4.8.0-52-generic/
```

### /usr/src 
* Ablage der Kernel-Sources
```
cb@w3qh:~$ ll /usr/src/
insgesamt 52
drwxr-xr-x 13 root root 4096 Mai 19 08:01 ./
drwxr-xr-x 12 root root 4096 Mär 31 14:46 ../
drwxr-xr-x 27 root root 4096 Feb 15 21:29 linux-headers-4.8.0-36/
drwxr-xr-x  7 root root 4096 Feb 15 21:29 linux-headers-4.8.0-36-generic/
drwxr-xr-x 27 root root 4096 Mär 31 13:36 linux-headers-4.8.0-45/
drwxr-xr-x  7 root root 4096 Mär 31 13:37 linux-headers-4.8.0-45-generic/
drwxr-xr-x 27 root root 4096 Apr  6 08:30 linux-headers-4.8.0-46/
drwxr-xr-x  7 root root 4096 Apr  6 08:30 linux-headers-4.8.0-46-generic/
drwxr-xr-x 27 root root 4096 Apr 26 09:58 linux-headers-4.8.0-49/
drwxr-xr-x  7 root root 4096 Apr 26 09:58 linux-headers-4.8.0-49-generic/
drwxr-xr-x 27 root root 4096 Mai 19 08:01 linux-headers-4.8.0-52/
drwxr-xr-x  7 root root 4096 Mai 19 08:01 linux-headers-4.8.0-52-generic/
```

### /lib/modules/<kernel-version>/modules.dep
Abhängigkeiten zwischen Kernel-Modulen
```
cb@w3qh:~$ cat /lib/modules/4.8.0-52-generic/modules.dep
kernel/arch/x86/events/intel/intel-rapl-perf.ko:
kernel/arch/x86/events/intel/intel-cstate.ko:
kernel/arch/x86/kernel/cpu/mcheck/mce-inject.ko:
kernel/arch/x86/kernel/msr.ko:
kernel/arch/x86/kernel/cpuid.ko:
kernel/arch/x86/crypto/glue_helper.ko:
kernel/arch/x86/crypto/aes-x86_64.ko:
kernel/arch/x86/crypto/des3_ede-x86_64.ko: kernel/crypto/des_generic.ko
kernel/arch/x86/crypto/camellia-x86_64.ko: kernel/crypto/lrw.ko kernel/arch/x86/crypto/glue_helper.ko
kernel/arch/x86/crypto/blowfish-x86_64.ko: kernel/crypto/blowfish_common.ko
```

### /proc/sys/kernel
* Kernel legt zur Laufzeit seine Konfig-Informationen in /proc ab
* Änderungen an diesen Dateien überstehen keinen Neustart -> lediglich Abbildung von Informationen aus dem RAM
```
cb@w3qh:~$ cat /proc/sys/kernel/version 
#55~16.04.1-Ubuntu SMP Fri Apr 28 14:36:29 UTC 2017

cb@w3qh:~$ cat /proc/sys/kernel/secure_boot 
0

cb@w3qh:~$ cat /proc/sys/kernel/threads-max 
61557
```

### /proc/interrupts
* enthält Informationen über System-Interrupts

### /proc/ioports
* enthält Informationen über System-I/O-Adressen

### /proc/dma
* enthält Informationen über System-DMA-Kanäle

### /proc/pci
* enthält Informationen über PCI (aktuelle Linuxe: /proc/bus/pci)

## Festplatten

* IDE: /dev/hdXY
* SCSI/SATA: /dev/sdXY
* bei Ubuntu/Linux-Mint werden aber auch IDE-Platten mit sdXY angesprochen!

Bsp: 
* vier IDE-Festplatten (4 sind möglich: primary ide master/slave + secondary ide master/slave):

* erste Platte: primary IDE Master, zwei primäre Partitionen (4 primäre sind max möglich)
    * /dev/hda1
    * /dev/hda2
* zweite Platte: primary IDE Slave, eine primäre Partition
    * /dev/hdb1 
* dritte Platte: secondary IDE Master, eine primäre Partition, 1 erweiterte Partition (nur eine mögliche), 5 logische Partitionen (60 sind möglich pro erweiterte)
    * /dev/hdc1 erste primäre Partition
    * /dev/hdc2 die erweiterte Partition
    * /dev/hdc5 (erste logische Partition bekommt immer die Ordungszahl 5 zugewiesen)
    * /dev/hdc6 zweite logische Partition
    * /dev/hdc7 dritte logische Partition
    * /dev/hdc8 vierte logische Partition
    * /dev/hdc9 fünfte logische Partition
* vierte Plattte: secondary IDE Slave, eine primäre Partition
    * /dev/hdd1
    
### /boot/grub/grub.conf
* Hier kann man Parameter persistieren, die der Bootloader beim Starten des Betriebssystems verwenden soll


## Anwendungen
### uname

* Ausgabe von System-Informationen

```
cb@w3qh:~$ uname -r # Ausgabe Kernel-Version
4.8.0-52-generic
```


modprobe

### lsmod
* Anzeige des Status der Module des laufenden Kernels (liest /proc/modules aus und gibt das hübsch formatiert aus)
```
cb@w3qh:~$ lsmod
Module                  Size  Used by
rfcomm                 77824  2
ip6table_filter        16384  0
ip6_tables             28672  1 ip6table_filter
iptable_filter         16384  0
ip_tables              24576  1 iptable_filter
x_tables               36864  4 ip_tables,iptable_filter,ip6table_filter,ip6_tables
pci_stub               16384  1
vboxpci                24576  0
vboxnetadp             28672  0
vboxnetflt             28672  0
[...]
```

### lsinfo
* Gibt genauere Infos über Module aus:
```
cb@w3qh:~$ modinfo rfcomm
filename:       /lib/modules/4.8.0-52-generic/kernel/net/bluetooth/rfcomm/rfcomm.ko
alias:          bt-proto-3
license:        GPL
version:        1.11
description:    Bluetooth RFCOMM ver 1.11
author:         Marcel Holtmann <marcel@holtmann.org>
srcversion:     BEEEA8F96C2AB26C52296F6
depends:        bluetooth
intree:         Y
vermagic:       4.8.0-52-generic SMP mod_unload modversions 
parm:           disable_cfc:Disable credit based flow control (bool)
parm:           channel_mtu:Default MTU for the RFCOMM channel (int)
parm:           l2cap_mtu:Default MTU for the L2CAP connection (uint)
parm:           l2cap_ertm:Use L2CAP ERTM mode for connection (bool)
```
Parameter: 
* a: Autor
* d: Description
* l: Lizenz
* p: Parameter
* n: Dateinamen des Modules

### insmod
* Module in den laufenden Kernel integrieren
* Erwartet Pfadangabe und Optionen
* automatische Abhängigkeitsprüfung
* keine automatische Auflösung
* Im Erfolgsfall keine Bestätigungsmeldung

### rmmod
* Entfernung nicht mehr benötigter Module aus dem RAM
* keine Pfadangabe notwendig
* Im Erfolgsfall keine Bestätigungsmeldung

### modprobe
* optimierte Kombi nvon insmod und rmmod
* Abhängigkeiten werden tatsächlich aufgelöst
* bei modernen Linux-Versionen gibt es Parameter a (all), t (type) und l (list) nicht mehr
* Parameter -r : remove Module

### depmod
* erstellt /lib/modules/<kernel-version>/modules.dep-Datei
* Sammelt Abhängigkeiten zwischen Modulen
* -n : Trockenlauf, Ausgabe nach stdout
* -A : Schnelldurchlauf



### lspci
* Arbeitet mit Verzeichnis /proc/bus/pci zusammen 

### lsusb
* OHCI: open host controller interface (Treiber: usb-ohci.o) --> USB 1.1
* UHCI: universal host controller interface (Treiber: usb-uhci.o) --> USB 1.1
* EHCI: enhanced host controller interface (Treiber: usb-ehci.o) --> USB 2.0

### dmesg
* Anzeige der System-Start-Protokollierung


