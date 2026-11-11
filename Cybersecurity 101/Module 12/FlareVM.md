# Tools inside FLareVM
## 1. Reverse Engineering and Debugging
Reverse engineering is like solving a puzzle backward: you take a finished product apart to understand how it works. Debugging is identifying errors, understanding why they happen, and correcting the code to prevent them.

1. **Ghidra-** NSA-developed open-source reverse engineering suite.
2. **x64dbg-**  Open-source debugger for binaries in x64 and x32 formats.
3. **OllyDbg** - Debugger for reverse engineering at the assembly level.
4. **Radare2** - A sophisticated open-source platform for reverse engineering.
5. **Binary Ninja** - A tool for disassembling and decompiling binaries.
6. **PEiD** - Packer, cryptor, and compiler detection tool.

## 2. Disassemblers and Decompilers
Disassemblers and Decompilers are crucial tools in malware analysis. They help analysts understand malicious software’s behaviour, logic, and control flow by breaking it into a more understandable format. The tools mentioned below are commonly used in this category.

1. **CFF Explorer** - A PE editor designed to analyze and edit Portable Executable (PE) files.
2. **Hopper Disassembler** - A Debugger, disassembler, and decompiler.
3. **RetDec** - Open-source decompiler for machine code.

## 3. Static and Dynamic Analysis
Static and dynamic analysis are two crucial methods in cyber security for examining malware. Static analysis involves inspecting the code without executing it, while dynamic analysis involves observing its behaviour as it runs. The tools mentioned below are commonly used in this category.

1. **Process Hacker -** Sophisticated memory editor and process watcher.
2. **PEview -** A portable executable (PE) file viewer for analysis.
3. **Dependency Walker -** A tool for displaying an executable’s DLL dependencies.
4. **DIE (Detect It Easy) -** A packer, compiler, and cryptor detection tool.

## 4. Forensics and Incident Response
Digital Forensics involves the collection, analysis, and preservation of digital evidence from various sources like computers, networks, and storage devices. At the same time, Incident Response focuses on the detection, containment, eradication, and recovery from cyberattacks. The tools mentioned below are commonly used in this category.

1. **Volatility -** RAM dump analysis framework for memory forensics.
2. **Rekall -** Framework for memory forensics in incident response.
3. **FTK Imager -** Disc image acquisition and analysis tools for forensic use.

## 5. Network Analysis 
Network Analysis includes different methods and techniques for studying and analysing networks to uncover patterns, optimize performance, and understand the underlying structure and behaviour of the network.

1. **Wireshark -** Network protocol analyzer for traffic recording and examination.
2. **Nmap -** A vulnerability detection and network mapping tool.
3. **Netcat -** Read and write data across network connections with this helpful tool.

## 6. File Analysis
File Analysis is a technique used to examine files for potential security threats and ensure proper file permissions.

1. **FileInsight -** A program for looking through and editing binary files.
2. **Hex Fiend -** Hex editor that is light and quick.
3. **HxD -** Binary file viewing and editing with a hex editor.

## 7. Scripting and Automation
Scripting and Automation involve using scripts such as PowerShell and Python to automate repetitive tasks and processes, making them more efficient and less prone to human error.

1. **Python -** Mainly automation-focused on Python modules and tools.
2. **PowerShell Empire -** Framework for PowerShell post-exploitation.

## 8. Sysinternals Suite
The Sysinternals Suite is a collection of advanced system utilities designed to help IT professionals and developers manage, troubleshoot, and diagnose Windows systems.

1. **Autoruns -** Shows what executables are configured to run during system boot-up.
2. **Process Explorer -** Provides information about running processes.
3. **Process Monitor -** Monitors and logs real-time process/thread activity.

# Commonly used Tools for Investigation

| Tool | Investigative Value |
| :--- | :--- |
| Procmon | A helpful tool for tracking system activity, especially regarding malware research, troubleshooting, and forensic investigations. |
| Process Explorer | Allows you to see the Process of the Parent-child relationship, DLLs loaded, and its path. |
| HxD | Malicious files can be examined or altered via hex editing. |
| Wireshark | Observing and investigating network traffic to look for unusual activity. |
| CFF Explorer | Can generate file hashes for integrity verification, authenticate the source of system files, and validate their validity. |
| PEStudio | Static analysis or studying executable file properties without running the files. |
| FLOSS | Extracts and de-obfuscates all strings from malware programs using advanced static analysis techniques. |

# 1. Process Monitor (Procmon)
A powerful Windows tool designed to help you record issues with your system's apps. It lets you see, record, and keep track of system and Windows file activity in real-time. Process Monitor is helpful for tracking system activity, especially regarding malware research, troubleshooting, and forensic investigations. It keeps real-time tabs on the file system, registry, and thread/process activity.

1. According to this log entry, the Local Security Authority Subsystem Service (LSASS)- related process lsass.exe has successfully read a file. LSASS handles authentication and frequently communicates with crucial system files such as lsasrv.dll (Local Security Authority Server Service).

2. Although this is a standard system process, LSASS may be the target of credential dumping attacks if you are examining logs for indications of malicious activity. Mimikatz and other tools frequently try to access LSASS memory. In these situations, you should watch for any additional suspicious activity related to LSASS, such as odd access patterns or processes reading or writing to lsass.exe.

# 2. Process Explorer(Procexp)
1. Process Explorer offers in-depth insights into the active processes running on your computer. It allows you to delve into the inner workings of your system, providing a comprehensive list of currently running processes and their linked user accounts. If you've ever been curious about which program is accessing a specific file or folder, Process Explorer can provide us with that information.

2. Using Process Explorer(procexp), located on the desktop, we identified the process and its parent process. This is usually pretty useful when we want to monitor what other processes are being spawned, such as from a Word document, an LNK file, or even an ISO file, as threat actors typically abuse these.

# 3. HxD
1. HxD is a quick and flexible hex editor for editing files, memory, and drives of any capacity. It can be applied to forensic investigation, data recovery, debugging, and exact manipulation of binary data. Important features include viewing file and memory contents, editing, searching, and comparing hex data. 

2. This HxD hex editor snapshot shows the binary file possible_medusa.txt. The hex data on the left indicates the file's contents in hexadecimal, and the ASCII interpretation appears on the right. Interestingly, the file starts with 4D 5A (Little Endian), indicating it is executable.

3. The Data Inspector on the right allows you to examine individual bytes by displaying their values in many data types (e.g., integer, float), facilitating a more straightforward data evaluation.

4. By permitting in-depth examination of a file's unprocessed hexadecimal data, HxD facilitates inquiry by identifying file kinds, structures, and possible corruption. Its Data Inspector feature helps by offering insights into particular byte values.

# 4. CFF Explorer
1. With the help of CFF Explorer's comprehensive file information, investigators can generate file hashes for integrity verification, authenticate the source of system files, and validate their validity (e.g., by looking for unusual alterations). This is important to know when analyzing malware since dangerous code may be hidden in altered system files.

2. The cryptominer.bin file's details are displayed in the sample. On September 23, 2024, a 64-bit Portable Executable file was generated. The file's information can be verified by its hashes (SHA-1 and MD5). During investigations, this tool aids in confirming file information lookup and locating possible problems.

# 5. Wireshark
1. Regarding network traffic analysis, Wireshark is a powerful tool that investigators may use to hunt down dubious connections, examine protocols, and spot possible assaults or data exfiltration. In this case, TLSv1.2 suggests a secure, encrypted connection that can mask harmful activity or safeguard legitimate traffic.

2. This Shows captured packets with details about the protocol, source, destination, and other information. Most packets show that TLSv1.2 and TCP are being used for encrypted transmission. The raw packet data is shown in ASCII and hexadecimal forms, with a significant chunk encrypted using TLSv1.2.

# 6. PEStudio
1. Static analysis, or studying executable file properties without running the files, is done with PEstudio. This feature is beneficial in several situations. PEstudio offers a variety of information about a file without putting users in danger of execution, which aids in identifying executables that seem suspect or harmful.

# 7. FLOSS
Using advanced static analysis techniques, the FLARE Obfuscated String Solver (FLOSS, formerly FireEye Labs Obfuscated String Solver) automatically extracts and de-obfuscates all strings from malware programs. Like strings.exe, it can enhance the basic static analysis of unknown binaries. FLOSS also includes more Python scripts in the script's directory, which can be used to load the script's output into other programs like IDA Pro or Binary Ninja.

# Analysis using PEStudio
1. For the computed MD5 9FDD4767DE5AEC8E577C1916ECC3E1D6 and SHA-1 A1BC55A7931BFCD24651357829C460FD3DC4828F hashes, comparisons with established databases like VirusTotal are recommended. If there are no known detections, there's a greater chance that it's a fresh or undiscovered malware campaign.

2. Although the file claims to be connected to the Windows Registry Editor (REGEDIT), which you can see based on the description, this is likely an attempt to trick people and evade discovery.

3. Legitimate REGEDIT tools are usually found in the C:\Windows\System32 directory rather than the user's download location.

4. "Registry Editor", "Операционная система Microsoft® Windows®") in the file’s metadata is suspicious, primarily if the user or the organization does not operate in a Russian-speaking environment. This could potentially have profound implications for our organization.

5. The absence of a rich header  indicates that the file is potentially packed or obfuscated to avoid detection by static analysis tools. This is typical behaviour of sophisticated malware that tries to evade detection by altering critical sections of its PE file.

6. The function tabs list API calls that the file has imported. This is also known as the IAT (Import Address Table). By clicking on the blacklist tab, PeStudio will sort the API by moving all the blacklisted functions to the top. This is useful because it enables us to understand how malware may behave once it compromises a host. The image below shows what API has been imported.

7. Here are the important functions that we noted.

**set_UseShellExecute:** This function allows the process to use the operating system's shell to execute other processes. This is often seen in malware that spawns additional processes to carry out malicious actions.

**CryptoStream, RijndaelManaged, CipherMode, CreateDecryptor:** These APIs indicate that the executable uses cryptographic functions, specifically Rijndael (AES encryption). Malware may use cryptography to encrypt communication and files or even implement ransomware functionality.

# Analysis using Floss
1. Open PowerShell and go to the directory where our file is, which is C:\Users\Administrator\Desktop\Sample. Note that it might take a while before the PowerShell prompt appears. Run the command FLOSS.exe .\windows.exe > windows.txt. This will run the tool floss.exe and output it to a file named windows.txt in the same directory.

2. Open the file and go to the bottom part of the result.

3. Aren't these familiar? These are the functions that we saw earlier using the PEStudio tool!

# Analyze with Process Explorer and Process Monitor
1. In this example, we will analyze the network connectivity of the file cobaltstrike.exe located in C:\Users\Administrator\Desktop\Sample.

2. We will try to figure out if the file is making any network connectivity to any possible c2 server.  Let's get started! Run the file cobaltstrike.exe and open Process Explorer on the desktop or from the taskbar. You can also search for it in the Windows search bar. If you manually click the binary Explorer.exe would be the parent process, and cobaltstrike.exe would be the child process. Let's see if that is indeed the case.

3. It is, as you can see from the screenshot above! Remember, this information is crucial, but let's focus on our goal to determine whether this process is making any network connectivity and to what destination. The process ID is 4756. Note that the Process ID might be different from your machine. Right-click on the process, select Properties and go to the TCP/IP tab. We should be able to determine the destination it connects to and the state it sends. 

4. There we have it! On another note, when we are doing analysis, it needs to be verified and precise. Therefore, we won't be relying on a single tool. We will use another tool to determine if the information is correct. Stop the process and rerun it. This time, we will use Procmon or Proces Monitor. This is also located on the desktop or in the taskbar.

5. Now, using this filter involves several steps. This includes:
Select the Process Name
Select contains
type any value containing any word related to the process. In this case, cobalt
Click include
And then Add and Click on Apply
You should be able to see the conditions added.

