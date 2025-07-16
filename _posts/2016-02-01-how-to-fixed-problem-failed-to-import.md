---
title: 'HOW TO: Fixed Problem Failed To Import Volatility.plugins.* When Running Volatility'
date: '2016-02-01T20:32:00.000+07:00'
author: arief
tags: [Volatility, Failed Import, Fixed Volatility]
categories: [Linux, Forensic Tools]
---

![memory forensic, volatility, linux, linux-command, command line interface](https://2.bp.blogspot.com/-lw5B72dKDuU/Vq9atlP6k1I/AAAAAAAAC8s/PrJ9qgYjwgc/s1600/Screenshot_20160201_200523.png)

Recently i has installed a memory forensic tools on my Slackware, actually i really need this memory forensic for my little experiment be called learning on home.  

But after i installed volatility, i got message _"failed to import volatility.plugins.* etc"_. Like above screenshot or can see this message below:

bash-4.3$ vol.py -h  
Volatility Foundation Volatility Framework 2.4  
\*\*\* Failed to import volatility.plugins.malware.svcscan (ImportError: No module named Crypto.Hash)  
\*\*\* Failed to import volatility.plugins.registry.shellbags (ImportError: No module named Crypto.Hash)  
\*\*\* Failed to import volatility.plugins.registry.auditpol (ImportError: No module named Crypto.Hash)  
\*\*\* Failed to import volatility.plugins.ssdt (NameError: name 'distorm3' is not defined)  
\*\*\* Failed to import volatility.plugins.registry.registryapi (ImportError: No module named Crypto.Hash)  
\*\*\* Failed to import volatility.plugins.mac.apihooks (ImportError: No module named distorm3)  
\*\*\* Failed to import volatility.plugins.envars (ImportError: No module named Crypto.Hash)  
\*\*\* Failed to import volatility.plugins.evtlogs (ImportError: No module named Crypto.Hash)  
\*\*\* Failed to import volatility.plugins.registry.lsadump (ImportError: No module named Crypto.Hash)  
\*\*\* Failed to import volatility.plugins.malware.threads (NameError: name 'distorm3' is not defined)  
\*\*\* Failed to import volatility.plugins.mac.apihooks_kernel (ImportError: No module named distorm3)  
\*\*\* Failed to import volatility.plugins.getservicesids (ImportError: No module named Crypto.Hash)  
\*\*\* Failed to import volatility.plugins.registry.shimcache (ImportError: No module named Crypto.Hash)  
\*\*\* Failed to import volatility.plugins.timeliner (ImportError: No module named Crypto.Hash)  
\*\*\* Failed to import volatility.plugins.malware.apihooks (NameError: name 'distorm3' is not defined)  
\*\*\* Failed to import volatility.plugins.linux.apihooks (ImportError: No module named distorm3)  
\*\*\* Failed to import volatility.plugins.getsids (ImportError: No module named Crypto.Hash)  
\*\*\* Failed to import volatility.plugins.mac.check\_syscall\_shadow (ImportError: No module named distorm3)  
\*\*\* Failed to import volatility.plugins.tcaudit (ImportError: No module named Crypto.Hash)  
Usage: Volatility - A memory forensics analysis platform.  

Options:  
  -h, --help            list all available options and their default values.  
                        Default values may be set in the configuration file  
                        (/etc/volatilityrc)  
  --conf-file=/home/slackerzone/.volatilityrc  
                        User based configuration file  
  -d, --debug           Debug volatility  
  --plugins=PLUGINS     Additional plugin directories to use (colon separated)  
  --info                Print information about all registered objects  
  --cache-directory=/home/slackerzone/.cache/volatility  
                        Directory where cache files are stored  
  --cache               Use caching  
  --tz=TZ               Sets the timezone for displaying timestamps  
  -f FILENAME, --filename=FILENAME  
                        Filename to use when opening an image  
  --profile=WinXPSP2x86  
                        Name of the profile to load  
  -l LOCATION, --location=LOCATION  
                        A URN location from which to load an address space  
  -w, --write           Enable write support  
  --dtb=DTB             DTB Address  
  --shift=SHIFT         Mac KASLR shift address  
  --output=text         Output in this format (format support is module  
                        specific)  
  --output-file=OUTPUT_FILE  
                        write output in this file  
  -v, --verbose         Verbose information  
  -g KDBG, --kdbg=KDBG  Specify a specific KDBG virtual address  
  -k KPCR, --kpcr=KPCR  Specify a specific KPCR address  
  
        Supported Plugin Commands:  
  
                atoms           Print session and window station atom tables  
                atomscan        Pool scanner for atom tables  
                bigpools        Dump the big page pools using BigPagePoolScanner  
                bioskbd         Reads the keyboard buffer from Real Mode memory  
                callbacks       Print system-wide notification routines  
                clipboard       Extract the contents of the windows clipboard  
                cmdline         Display process command-line arguments  
                cmdscan         Extract command history by scanning for \_COMMAND\_HISTORY  
                connections     Print list of open connections \[Windows XP and 2003 Only\]  
                connscan        Pool scanner for tcp connections  
                consoles        Extract command history by scanning for \_CONSOLE\_INFORMATION  
                crashinfo       Dump crash-dump information  
                deskscan        Poolscaner for tagDESKTOP (desktops)  
                devicetree      Show device tree  
                dlldump         Dump DLLs from a process address space  
                dlllist         Print list of loaded dlls for each process  
                driverirp       Driver IRP hook detection  
                driverscan      Pool scanner for driver objects  
                dumpcerts       Dump RSA private and public SSL keys  
                dumpfiles       Extract memory mapped and cached files  
                eventhooks      Print details on windows event hooks  
                filescan        Pool scanner for file objects  
                gahti           Dump the USER handle type information  
                gditimers       Print installed GDI timers and callbacks  
                gdt             Display Global Descriptor Table  
                handles         Print list of open handles for each process  
                hibinfo         Dump hibernation file information  
                hivedump        Prints out a hive  
                hivelist        Print list of registry hives.  
                hivescan        Pool scanner for registry hives  
                hpakextract     Extract physical memory from an HPAK file  
                hpakinfo        Info on an HPAK file  
                idt             Display Interrupt Descriptor Table  
                iehistory       Reconstruct Internet Explorer cache / history  
                imagecopy       Copies a physical address space out as a raw DD image  
                imageinfo       Identify information for the image  
                impscan         Scan for calls to imported functions  
                joblinks        Print process job link information  
                kdbgscan        Search for and dump potential KDBG values  
                kpcrscan        Search for and dump potential KPCR values  
                ldrmodules      Detect unlinked DLLs  
                machoinfo       Dump Mach-O file format information  
                malfind         Find hidden and injected code  
                mbrparser       Scans for and parses potential Master Boot Records (MBRs)  
                memdump         Dump the addressable memory for a process  
                memmap          Print the memory map  
                messagehooks    List desktop and thread window message hooks  
                mftparser       Scans for and parses potential MFT entries  
                moddump         Dump a kernel driver to an executable file sample  
                modscan         Pool scanner for kernel modules  
                modules         Print list of loaded modules  
                multiscan       Scan for various objects at once  
                mutantscan      Pool scanner for mutex objects  
                notepad         List currently displayed notepad text  
                objtypescan     Scan for Windows object type objects  
                patcher         Patches memory based on page scans  
                poolpeek        Configurable pool scanner plugin  
                printkey        Print a registry key, and its subkeys and values  
                privs           Display process privileges  
                procdump        Dump a process to an executable file sample  
                pslist          Print all running processes by following the EPROCESS lists  
                psscan          Pool scanner for process objects  
                pstree          Print process list as a tree  
                psxview         Find hidden processes with various process listings  
                raw2dmp         Converts a physical memory sample to a windbg crash dump  
                screenshot      Save a pseudo-screenshot based on GDI windows  
                sessions        List details on \_MM\_SESSION_SPACE (user logon sessions)  
                sockets         Print list of open sockets  
                sockscan        Pool scanner for tcp socket objects  
                strings         Match physical offsets to virtual addresses (may take a while, VERY verbose)  
                symlinkscan     Pool scanner for symlink objects  
                thrdscan        Pool scanner for thread objects  
                timers          Print kernel timers and associated module DPCs  
                unloadedmodules Print list of unloaded modules  
                userassist      Print userassist registry keys and information  
                userhandles     Dump the USER handle tables  
                vaddump         Dumps out the vad sections to a file  
                vadinfo         Dump the VAD info  
                vadtree         Walk the VAD tree and display in tree format  
                vadwalk         Walk the VAD tree  
                vboxinfo        Dump virtualbox information  
                verinfo         Prints out the version information from PE images  
                vmwareinfo      Dump VMware VMSS/VMSN information  
                volshell        Shell in the memory image  
                windows         Print Desktop Windows (verbose details)  
                wintree         Print Z-Order Desktop Windows Tree  
                wndscan         Pool scanner for window stations  
                yarascan        Scan process or kernel memory with Yara signatures

After i trace one by one, evidently pycrypto and distorm3 installed not yet. So for installing, quite simply type command with pip:

> \# pip install pycrypto && pip install distorm3

After installed pycrypto and distorm3, and i see this problem has solved. Like below screenshot:  

![](https://4.bp.blogspot.com/-knKR-7Mkaz0/Vq9e66dOKWI/AAAAAAAAC84/32lmGrzq-1M/s1600/Screenshot_20160201_201259.png)

If you want installing pip, you can find or each repository. In there i'm using Slackware as OS, you can find volatility from slackbuilds.org or using third party with sbopkg.  

For Ubuntu/Debian or RedHat/Fedora, simply just type command:

> $ sudo apt-get install pip \[Ubuntu/Debian\]  
> Or,  
> $ sudo yum install pip \[RedHat/Fedora\]

So these tutorial about [**Fixed Problem Failed To Import Volatility.plugins.***](https://arief-jr.blogspot.com/search/label/Linux-command).  
Next, if i have time i will share to using volatility for analysis memory forensics.

#### Happy Using and Good Luck! Arief