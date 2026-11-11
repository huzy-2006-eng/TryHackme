CAPA is an open-source tool developed by the Mandiant FLARE team. It is designed to identify the capabilities present in executable files like Portable Executables (PE), ELF binaries, .NET modules, shellcode, and even sandbox reports.

It does so by analyzing the file and applying a set of rules that describe common behaviors, allowing it to determine what the program is capable of doing, such as network communication, file manipulation, process injection, and many more.

The beauty of CAPA is that it encapsulates years of reverse engineering knowledge into an automated tool, making it accessible even to those who may not be experts in reverse engineering. This can be incredibly useful for analysts and security professionals, allowing them to quickly understand potentially malicious software's functionality without manually reverse engineering the code.

This tool is useful in malware analysis and threat hunting, where understanding a binary's capabilities is important for incident response and defensive measures.

# MITRE ATT&CK
The MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge) framework is a global knowledge base that documents the tactics and techniques threat actors use at every stage of a cyberattack. It works like a playbook of attacker methods, from gaining initial access to maintaining a presence, escalating privileges, evading defenses, moving laterally within a network, and much more.

CAPA writes each ATT&CK entry in one of the formats below. Every entry carries a technique identifier, and only some also have a sub-technique.

| Format | Sample | Explanation |
| :--- | :--- | :--- |
| ATT&CK Tactic::ATT&CK Technique [Technique Identifier] | `Defense Evasion::Obfuscated Files or Information [T1027]` | Defense Evasion is the ATT&CK tactic, Obfuscated Files or Information is the ATT&CK technique, and T1027 is the technique identifier. |
| ATT&CK Tactic::ATT&CK Technique::ATT&CK Sub-Technique [Technique Identifier.Sub-Technique Identifier] | `Defense Evasion::Obfuscated Files or Information::Indicator Removal from Tools [T1027.005]` | Defense Evasion is the ATT&CK tactic, Obfuscated Files or Information is the ATT&CK technique, and Indicator Removal from Tools is the ATT&CK sub-technique. T1027 is the technique identifier and 005 is the sub-technique identifier. |

# MAEC
Malware Attribute Enumeration and Characterization (MAEC) is a structured language for encoding and sharing information about malware. It covers a wide range of attributes, including behaviors, artifacts, and relationships between malware samples.

This gives analysts a standard way to track and analyze the details of malware.

| MAEC Value | Description |
| :--- | :--- |
| Launcher | Set when the `write and execute a file` rule matches: the same function writes a file to disk and creates a process. |
| Downloader | Set when the `download and write a file` rule matches: the file receives data and writes it to disk. MAEC describes a downloader as malware programmed to download and execute other files, usually more complex malware. |

1. When CAPA tags a file with the "launcher" MAEC value, the file writes something to disk and then runs it. In a real sample, that step is often part of behavior like:

Dropping additional payloads
Activating persistence mechanisms
Connecting to command-and-control (C2) servers
Executing specific functions
This is interesting! Some of these behaviors are also present in the Malware Behavior Catalog (MBC) and Capability blocks

2. When CAPA tags a file with the "Downloader" MAEC value, the file receives data and writes it to disk. That step is often part of behavior like:

Fetching additional payloads or resources from the internet
Pulling in updates
Executing secondary stages
Retrieving configuration files

# Malware Behavior Catalogue (MBC)
MBC is designed to support malware analysis use cases such as labeling, similarity analysis, and standardized reporting. It serves as a catalog of malware objectives and behaviors.

MBC links to ATT&CK techniques where they apply and captures all behaviors and code characteristics discovered during malware analysis. Keep in mind that the names of MBC behaviors may or may not match the related ATT&CK techniques.

The information on behavior pages adds to the content on ATT&CK pages. In other words, when recording malware behaviors, MBC users will reference ATT&CK, but MBC does not duplicate ATT&CK information.

| Format | Sample | Explanation |
| :--- | :--- | :--- |
| OBJECTIVE::Behavior::Method [Identifier] | `ANTI-STATIC ANALYSIS::Executable Code Obfuscation::Argument Obfuscation [B0032.020]` | Anti-Static Analysis is the OBJECTIVE, Executable Code Obfuscation is the BEHAVIOR, Argument Obfuscation is the METHOD, and B0032.020 is the IDENTIFIER. |
| OBJECTIVE::Behavior [Identifier] | `COMMUNICATION::HTTP Communication [C0002]` | COMMUNICATION is the OBJECTIVE, HTTP Communication is the BEHAVIOR, and C0002 is the IDENTIFIER. |

## Objectives

| Objective | Explanation |
| :--- | :--- |
| Anti-Behavioral Analysis | Malware attempts to avoid detection by hindering behavioral analysis using tools like sandboxes or debuggers. |
| Anti-Static Analysis | Malware attempts to obstruct or add complexity to static analysis, making it more challenging for security professionals to identify and understand its malicious behaviors and intentions. |
| Collection | Malware focuses on identifying and gathering information from the targeted machine or network. |
| Command and Control | Malware typically establishes communication with compromised systems through various methods such as command and control servers, peer-to-peer networks, or other means. This communication allows the malware to control the compromised systems, enabling the attackers to execute commands, exfiltrate data, or carry out other malicious activities. |
| Credential Access | Malware aims to steal account credentials, such as usernames and passwords. |
| Defense Evasion | Malware aims to bypass and circumvent the various detection and security mechanisms present within the system to avoid being detected or mitigated. |
| Discovery | Malware seeks to collect detailed information about the configuration and setup of the system or network environment, including hardware, software, and network infrastructure. |
| Execution | Malware aims to execute commands or code on the targeted system. |
| Exfiltration | Malware aims to steal and extract sensitive data. This can include personal information, financial details, and any other valuable data stored on the targeted system or network. |
| Impact | Malware aims to manipulate, disrupt, or damage computer systems and data, leading to financial loss, privacy breaches, and system instability. |
| Lateral Movement | Malware seeks to spread through the network, either actively through machine access or passively, such as via malicious emails. |
| Persistence | Malware aims to remain on a computer system and stay operational. |
| Privilege Escalation | Malware seeks to gain elevated permissions or control on a computer system or network. With higher privileges, it can access sensitive information or take control of system resources for malicious purposes. |

### Micro-Objective

| Micro-Objective | Description |
| :--- | :--- |
| PROCESS | Exhibiting behaviors related to processes, such as, but not limited to, Creating Process, Setting Thread Context, Terminating Process, and Checking Mutex. |
| MEMORY | Exhibiting behaviors such as, but not limited to, Allocating Memory, Changing Memory Protection, and Freeing Memory. |
| COMMUNICATION | Exhibiting behaviors related to network traffic, such as, but not limited to, DNS, FTP, HTTP, ICMP, and SMTP. |
| DATA | Exhibiting behaviors such as, but not limited to, checking strings, compressing, decoding, and encoding data. |
| FILE SYSTEM | Exhibiting behaviors that manipulate files or directories, such as creating directories and reading, writing, or deleting files. |

final output of CAPA, both Objective and Micro-Objective are shown under the **MBC Objective** column.

## MBC Behaviour

| Objective | Behavior | Identifier | Explanation |
| :--- | :--- | :--- | :--- |
| ANTI-BEHAVIORAL ANALYSIS | Virtual Machine Detection | B0009 | The malware checks to see if it is running in a virtual environment. During its system reconnaissance, the malware examines various user and system artifacts. |
| ANTI-STATIC ANALYSIS | Executable Code Obfuscation | B0032 | Executable code has been intentionally obscured to prevent static code analysis. This is a specific behavior related to the executable code of a malware sample, including its data and text sections. |
| EXECUTION | Command and Scripting Interpreter | E1059 | Malware can abuse command and script interpreters to run malicious commands, scripts, or binaries. It targets built-in interpreters like cmd.exe or PowerShell on Windows or Bash on Unix-like systems. Attackers may also use other scripting languages like Python, Perl, or JavaScript. |
| DISCOVERY | File and Directory Discovery | E1083 | Malware can search for specific files in particular locations by enumerating files and directories. |
| ANTI-STATIC ANALYSIS, DEFENSE EVASION | Obfuscated Files or Information | E1027 | Malware can obfuscate files or information by encoding, encrypting, or otherwise making them hard to analyze. The malware sample itself can also be encoded or encrypted. |

### Micro-Behavior

The term "low-level behaviors" in malware analysis refers to actions exhibited by malware that aren't necessarily malicious and may serve various objectives. MBC captures these behaviors as "micro-behaviors" because they're often noted during malware analysis.

Examples of such low-level behaviors include creating a TCP socket and checking a string for some condition. Keep in mind that just because a behavior is low-level does not mean it is harmless, as it may still be part of a larger malicious scheme.

| Micro-Objective | Micro-Behavior | Identifier | Explanation |
| :--- | :--- | :--- | :--- |
| MEMORY | Allocate Memory | C0007 | Malware frequently uses memory allocation as part of its strategy to unpack itself and execute its malicious activities. |
| PROCESS | Create Process | C0017 | Malware creates a process, for example via WMI or shellcode. It can also create a suspended process. |
| COMMUNICATION | HTTP Communication | C0002 | Malware is capable of initiating HTTP communications. |
| DATA | Check String | C0019 | Malware can inspect a string to identify specific characteristics, such as ASCII content, credit card numbers, and string length. |
| DATA | Encode Data | C0026 | Malware has the capability to encode data using base64 and XOR. |
| FILE SYSTEM | Create Directory | C0046 | Malware can create a directory. |
| FILE SYSTEM | Delete File | C0047 | Malware has the capability to delete a file. |
| FILE SYSTEM | Read File | C0051 | Malware can read a file. |
| FILE SYSTEM | Writes File | C0052 | Malware has the capability to write to a file. |

## Methods
Lastly, let's check the METHODS. Below are the methods included in the results from our sample. Methods are tied to behaviors, so to see all the methods of a behavior or micro-behavior, check its own page in MBC.

| Behavior | Method or Sub-Technique | Identifier | Explanation |
| :--- | :--- | :--- | :--- |
| Executable Code Obfuscation | Argument Obfuscation | B0032.020 | Simple number or string arguments to API calls are calculated at runtime, making analysis more difficult. |
| Executable Code Obfuscation | Stack Strings | B0032.017 | Build and decrypt strings on the stack at each use, then discard to avoid obvious references. |
| HTTP Communication | Read Header | C0002.014 | HTTP read header. |
| Encode Data | Base64 | C0026.001 | Malware may encode data using Base64. |
| Encode Data | XOR | C0026.002 | Malware may use XOR to encode data. |
| Obfuscated Files or Information | Encoding-Standard Algorithm | E1027.m02 | A standard algorithm (for example, base64) is used to encode a malware sample, file, or other information. |

## Example
┌─────────────────────────────┬──────────────────────────────────┐
│ MBC Objective               │ MBC Behavior                     │
├─────────────────────────────┼──────────────────────────────────┤
│ DATA                        │ Encode Data::Base64 [C0026.001]  │
└─────────────────────────────┴──────────────────────────────────┘

| Label | Value | Explanation |
| :--- | :--- | :--- |
| MBC Objective | DATA | Exhibiting behaviors such as, but not limited to, checking strings, compressing, decoding, and encoding data. |
| MBC Behavior | Encode Data | Malware has the capability to encode data using base64 and XOR. |
| Method | Base64 | Malware may encode data using Base64. |
| Identifier | C0026.001 | The identifier's letter relays information about the entry: B is an MBC behavior, C is a micro-behavior, and E is an ATT&CK technique enhanced with malware-specific details. It also serves as a tag. |

# Namespaces

| Part | Sample | Explanation |
| :--- | :--- | :--- |
| Capability | reference anti-VM strings | The capability, or rule name |
| TLN | anti-analysis | The Top-Level Namespace |
| Namespace | anti-vm/vm-detection | The namespace inside the TLN |

| Top-Level Namespace (TLN) | Explanation |
| :--- | :--- |
| anti-analysis | Contains rules that detect behaviors malware uses to evade analysis. These behaviors include obfuscation, packing, and anti-debugging techniques. |
| collection | Contains rules for data that malware may enumerate and collect for exfiltration or other purposes. Think of it as the "data-gathering" side of malware behavior. |
| communication | Contains rules for the different ways malware communicates. This covers how malware interacts with networks, such as HTTP and TCP traffic, sending and receiving data, and command and control (C2) communication. |
| compiler | Contains rules that recognize the build environment or compiler used to create an executable, such as MSVC, Delphi, or AutoIt. They work as a "signature" of how the program was built. |
| data-manipulation | Contains rules for how a program transforms data, such as encryption, hashing, and encoding. Think of it as the "data transformation" side of malware behavior. |
| executable | Contains rules for the attributes of executable files. These attributes include PE sections or debug info associated with the executable. |
| host-interaction | Contains rules for how a program accesses or changes resources on the host system. This covers files and directories (reading, writing, creating, and deleting them), processes, the Registry, services, and more. |
| impact | Contains rules for the end goal of a program and the harm it can cause. Examples include deleting volume shadow copies, wiping the disk, and the cryptocurrency strings found in our sample. |
| internal | Contains rules used internally by CAPA to guide its analysis. These rules aren't meant for direct use by analysts or for reporting. |
| lib | Contains library rules, the building blocks used to create other rules. CAPA doesn't show these rules as results. |
| linking | Contains rules that detect how a program links to external code. Malware often depends on external libraries (such as OpenSSL or Zlib) to carry out specific tasks, or resolves functions at runtime, and detecting these dependencies helps analysts understand the malware's capabilities. |
| load-code | Contains rules for loading or running code while the program executes, such as an embedded PE file, shellcode, .NET code, or PowerShell. In our sample, "parse PE header" and "run PowerShell expression" fall under this TLN. |
| malware-family | Contains rules for behaviors linked to particular malware families or groups. It identifies the distinct characteristics or "signatures" of known malware families, allowing for more accurate detection and classification. |
| nursery | A staging ground for rules that are not quite polished yet. |
| persistence | Contains rules for behaviors associated with maintaining access or persistence within a compromised system. This namespace focuses on how malware can establish and maintain a presence within a compromised environment, allowing it to carry out malicious activities over an extended period. |
| runtime | Contains rules that identify the language runtime or platform the program runs on, such as the .NET platform or Go. |
| targeting | Contains rules for programs that give special handling to specific systems, such as ATMs. |

Let's see how this works by checking the table below:

| Top-Level Namespace (TLN) | Namespaces | Rule YAML File | Explanation |
| :--- | :--- | :--- | :--- |
| anti-analysis | anti-vm/vm-detection | `reference-anti-vm-strings-targeting-virtualbox.yml`, `reference-anti-vm-strings-targeting-virtualpc.yml` | The anti-vm/vm-detection namespace contains rules to detect virtual machine (VM) environments. These rules look for strings that malware commonly uses to detect a VM, such as VMware driver names, VMware Tools registry keys, or the `vmtoolsd.exe` process. |
| anti-analysis | obfuscation | `obfuscated-with-dotfuscator.yml`, `obfuscated-with-smartassembly.yml` | Malware often uses obfuscation to make analysis more difficult and to conceal the true purpose of its code and strings. The obfuscation namespace holds rules for known obfuscators, such as the .NET obfuscators Dotfuscator and SmartAssembly, and the `string/stackstring` namespace for strings built on the stack. Packing and anti-debugging tricks have their own namespaces under anti-analysis (`packer` and `anti-debugging`). |

# Capabilities

| Capability | Top-Level Namespace (TLN) | Namespace | Rule YAML File |
| :--- | :--- | :--- | :--- |
| reference anti-VM strings | anti-analysis | `anti-vm/vm-detection` | `reference-anti-vm-strings.yml` |
| reference anti-VM strings targeting VMWare | anti-analysis | `anti-vm/vm-detection` | `reference-anti-vm-strings-targeting-vmware.yml` |
| reference anti-VM strings targeting VirtualBox | anti-analysis | `anti-vm/vm-detection` | `reference-anti-vm-strings-targeting-virtualbox.yml` |
| reference HTTP User-Agent string | communication | `http` | `reference-http-user-agent-string.yml` |
| check HTTP status code | communication | `http/client` | `check-http-status-code.yml` |
| reference Base64 string | data-manipulation | `encoding/base64` | `reference-base64-string.yml` |
| encode data using XOR | data-manipulation | `encoding/xor` | `encode-data-using-xor.yml` |
| contain a thread local storage (.tls) section | executable | `pe/section/tls` | `contain-a-thread-local-storage-tls-section.yml` |
| get common file path | host-interaction | `file-system` | `get-common-file-path.yml` |
| create directory | host-interaction | `file-system/create` | `create-directory.yml` |
| delete file | host-interaction | `file-system/delete` | `delete-file.yml` |
| read file on Windows | host-interaction | `file-system/read` | `read-file-on-windows.yml` |
| write file on Windows | host-interaction | `file-system/write` | `write-file-on-windows.yml` |
| get thread local storage value | host-interaction | `process` | `get-thread-local-storage-value.yml` |
| allocate or change RWX memory | host-interaction | `process/inject` | `allocate-or-change-rwx-memory.yml` |
| create process on Windows | host-interaction | `process/create` | `create-process-on-windows.yml` |
| reference cryptocurrency strings | impact | `cryptocurrency` | `reference-cryptocurrency-strings.yml` |
| link function at runtime on Windows | linking | `runtime-linking` | `link-function-at-runtime-on-windows.yml` |
| parse PE header | load-code | `pe` | `parse-pe-header.yml` |
| resolve function by parsing PE exports | load-code | `pe` | `resolve-function-by-parsing-pe-exports.yml` |
| run PowerShell expression | load-code | `powershell` | `run-powershell-expression.yml` |
| schedule task via at | persistence | `scheduled-tasks` | `schedule-task-via-at.yml` |
| schedule task via schtasks | persistence | `scheduled-tasks` | `schedule-task-via-schtasks.yml` |

# Examples
1. To further explain this, let's check the first capability in the table, reference anti-VM strings:

The related rule file is reference-anti-vm-strings.yml
It sits under the namespace anti-vm/vm-detection
That namespace is under the Top-Level Namespace anti-analysis
This tells us that capa found strings in the file that malware commonly uses to detect a virtual machine or sandbox, using the reference-anti-vm-strings.yml rule. These include registry paths that reveal the BIOS or disk vendor, hypervisor names like Hyper-V and KVM, and DLL names of known sandboxes and security tools.

Malware typically does this to avoid being analyzed: if it sees it's running in a VM, it can stop or hide what it really does. That is why capa flagged this one.

2. Let's have another example and look at schedule task via schtasks:

The related rule file is schedule-task-via-schtasks.yml
It sits under the namespace scheduled-tasks
That namespace is under the Top-Level Namespace persistence
This tells us that capa identified behaviors related to scheduled tasks within the Windows operating system. The rule matches a function that creates a process and references schtasks with /create (or the PowerShell Register-ScheduledTask command), which suggests the executable registers a scheduled task to maintain persistence.

# Real example

┌───────────────────────────────────────────┬───────────────────────────────────────────┐
│ Capability                                │ Namespace                                 │
├───────────────────────────────────────────┼───────────────────────────────────────────┤
│ reference Base64 string                   │ data-manipulation/encoding/base64         │
└───────────────────────────────────────────┴───────────────────────────────────────────┘

| Label | Value | Explanation |
| :--- | :--- | :--- |
| Capability | `reference Base64 string` | The file contains the Base64 alphabet string, which suggests the malware encodes or decodes data using Base64. |
| Top-Level Namespace | `data-manipulation` | Contains rules for behaviors that transform data, such as encryption, hashing, and encoding. This can be considered the "data transformation" component of malware behavior, covering actions such as string encryption and data encoding. |
| Namespace | `encoding/base64` | This namespace contains the rules for encoding and decoding data using Base64. XOR encoding has its own namespace, `encoding/xor`. |
| Rule YAML File Matched | `reference-base64-string.yml` | Remember that the rule file is the capability's name in lowercase, with a dash (-) in place of each space. |


