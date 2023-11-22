# Use Volatility with the DLL plugin And ClamScan to scan Infected Memory Dump

## Description
A memory image of a live system infected with Stuxnet malware is provided. The objective is to analyze and identify IOC.
- I will use Volatility 2.6 to analyze stuxnet.vmem file on Power Shell inside a Windows computer.

## Solution
First of all, I will explain some special words.
- .dll: stands for Dynamic link library, some files with the .dll extension are similar to the libraries/frameworks that you import to run code more easily. 
- dlldump: dlldump is a plugin used to dump files with the .dll extension. 
- ClamScan: ClamScan is ClamAV but runs in the Windows version.

Firstly, I run the command to scan the info of the file.
```bash
PS C:\Users\annial\Downloads\Project_IAM\volatility_2.6_win64_standalone\volatility_2.6_win64_standalone> .\volatility_2.6_win64_standalone.exe -f .\stuxnet.vmem imageinfo
Volatility Foundation Volatility Framework 2.6
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : WinXPSP2x86, WinXPSP3x86 (Instantiated with WinXPSP2x86)
                     AS Layer1 : IA32PagedMemoryPae (Kernel AS)
                     AS Layer2 : FileAddressSpace (C:\Users\annial\Downloads\Project_IAM\volatility_2.6_win64_standalone\volatility_2.6_win64_standalone\stuxnet.vmem)
                      PAE type : PAE
                           DTB : 0x319000L
                          KDBG : 0x80545ae0L
          Number of Processors : 1
     Image Type (Service Pack) : 3
                KPCR for CPU 0 : 0xffdff000L
             KUSER_SHARED_DATA : 0xffdf0000L
           Image date and time : 2011-06-03 04:31:36 UTC+0000
     Image local date and time : 2011-06-03 00:31:36 -0400
```
Syntax:
- .\volatility_2.6_win64_standalone.exe: running Volatility
- -f: importing a file
- .\stuxnet.vmem: imported file
- imageinfo: plugins to check information of a memory file in Volatility 2.6

It has tons of information but you just taking care of the Suggested Profile(s) line. It has 2 profiles but it is the same so I will analyze the WinXPSP2x86 profile in deep.
