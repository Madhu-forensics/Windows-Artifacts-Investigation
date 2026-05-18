Windows Artifact \& Memory Forensics Investigation Report



Case Information



Examiner: Madhumitha M

Investigation Type: Windows Artifact \& Memory Forensics Investigation

Evidence Types: Windows Memory Dump (.dmp) and Disk Image (.E01)

Tools Used: Volatility3, Autopsy, PowerShell, 7-Zip







1\. Executive Summary



A forensic investigation was conducted on a Windows memory dump and forensic disk image to identify evidence of system activity, user actions, and potentially suspicious behavior. Evidence integrity was verified using SHA256 hashing prior to analysis. Memory forensic analysis was performed using Volatility3 to enumerate active processes, inspect process relationships, review network activity, and analyze command-line execution. Disk artifact analysis was performed using Autopsy to examine browser history, recent documents, deleted files, USB attachment history, and operating system artifacts.



The investigation identified PowerShell execution associated with explorer.exe within the process hierarchy, multiple active and listening network connections, browser activity artifacts, execution traces, and user activity records. The findings demonstrate a structured forensic workflow involving evidence preservation, artifact correlation, and investigative documentation.







2\. Case Background \& Scope



This investigation was conducted as an independent forensic laboratory exercise focused on Windows artifact analysis and volatile memory investigation. The objective of the analysis was to:



* Verify forensic evidence integrity
* Analyze volatile memory artifacts
* Identify active and suspicious processes
* Review network connection activity
* Examine Windows user activity artifacts
* Review browser history and recent document access
* Document investigative findings and methodology



The investigation involved analysis of:



\-A Windows memory dump (.dmp)

\-A forensic disk image (.E01)





The scope of the investigation focused on forensic acquisition validation, memory analysis, process enumeration, network analysis, artifact examination, and documentation of findings.









3\. Tools Used





|Tools|Purpose|
|-|-|
|Volatility3|Memory forensic analysis|
|Autopsy|Disk image and artifact analysis|
|PowerShell|Hash generation and verification|
|Windows Command Prompt|Command-line forensic operations|
|7-Zip|Extraction of forensic evidence archives|









4\. Methodology



4.1 Evidence Preservation \& Hash Verification



The forensic evidence files were preserved in a structured project directory prior to analysis. SHA256 hashing was performed using PowerShell to verify evidence integrity before examination.



Hash Verification Command



Get-FileHash .\\2020JimmyWilson.E01 -Algorithm SHA256



The resulting hash values were documented and retained as part of the investigation records.









4.2 Memory Forensic Analysis



Volatile memory analysis was performed using Volatility3 against the provided Windows memory dump.



The following Volatility3 plugins were executed:



Plugin	                                 Purpose



windows.info	             Operating system identification

windows.pslist	             Running process enumeration

windows.pstree	             Parent-child process analysis

windows.netscan              Network connection analysis

windows.cmdline	             Command-line investigation

windows.filescan	     File object enumeration





Example Command



vol.exe -f 192-Reveal.dmp windows.pslist



Memory analysis focused on identifying suspicious process behavior, command-line execution, network activity, and relationships between active processes.









4.3 Disk Artifact Analysis



The Windows forensic disk image was loaded into Autopsy for artifact analysis.



The following artifact categories were reviewed:



1. Operating System Information
2. Recent Documents
3. Deleted Files
4. Recycle Bin Artifacts
5. Web History
6. Web Searches
7. USB Device Attachment History
8. Run Program Artifacts





Autopsy ingest modules used during analysis included:



1. Recent Activity
2. Web Artifacts
3. File Type Identification
4. Keyword Search
5. Embedded File Extractor





The investigation focused on reconstructing user activity and identifying system artifacts relevant to forensic examination.







5\. Findings



Finding 1 — Evidence Integrity Verification



The forensic evidence was verified using SHA256 hashing prior to analysis. Evidence integrity verification ensured that the forensic images remained unmodified during the investigation process.



Finding 2 — Active Process Enumeration



Memory analysis identified multiple active processes within the Windows environment using the Volatility3 windows.pslist plugin.



The process listing included:

explorer.exe

powershell.exe

RuntimeBroker.exe

SearchProtocolHost.exe

Thunderbird.exe



The analysis established baseline visibility into active system processes during memory acquisition.



Finding 3 — Process Tree Correlation



Parent-child process analysis performed using the windows.pstree plugin identified PowerShell execution associated with explorer.exe.



This process relationship was considered relevant because PowerShell is commonly used for administrative scripting, automation, and, in some cases, malicious or fileless execution techniques.



No definitive malicious payload was confirmed during analysis; however, the process chain was documented as an investigative observation.



Finding 4 — Network Connection Analysis



Network analysis conducted using the windows.netscan plugin identified multiple listening and established network connections.



Observed activity included:



TCP and UDP connections



Established connections associated with normal application activity



Internal/private IP address activity in the 192.168.x.x range



Application-related network activity associated with Skype





The analysis did not identify confirmed malicious outbound connections during the investigation.



Finding 5 — Command-Line Analysis



The windows.cmdline plugin was used to review command-line execution details associated with active processes.



The analysis identified:



powershell.exe



explorer.exe



RuntimeBroker.exe



SearchProtocolHost.exe





The command-line review assisted in correlating active processes with execution behavior and system activity.



Finding 6 — Windows Artifact Examination



Autopsy artifact analysis identified multiple Windows user activity artifacts including:



Recent document activity



Browser history entries



Web search artifacts



USB device attachment records



Deleted file artifacts



Installed program records



Operating system information





These artifacts contributed to reconstruction of user activity within the forensic image.







6\. Timeline Reconstruction



The investigation reconstructed portions of system and user activity through memory and disk artifact analysis.



The following investigative sequence was documented:



Activity	                                   Description



Evidence Acquisition	     Memory dump and disk image preserved for analysis

Hash Verification	     SHA256 integrity verification completed

Memory Analysis	             Active processes and network connections reviewed

Process Correlation	     PowerShell activity examined within process tree

Artifact Analysis	     Browser and system artifacts reviewed in Autopsy

Documentation	             Screenshots and findings documented





7\. Conclusion



The investigation successfully demonstrated a structured digital forensic workflow involving both volatile memory analysis and Windows artifact examination.



The forensic process included:



Evidence preservation



Hash verification



Memory forensic analysis



Process investigation



Network connection review



Browser artifact examination



User activity reconstruction



Investigative documentation





The analysis identified active PowerShell execution, process relationships, network activity, browser artifacts, deleted file artifacts, and user activity traces within the forensic evidence.



This investigation provided practical experience in evidence handling, forensic methodology, artifact correlation, and structured reporting using industry-standard forensic tools.





8\. Appendix — Chain of Custody Log



CHAIN OF CUSTODY LOG



═══════════════════════════════



Evidence Description: Windows forensic evidence set consisting of memory dump (.dmp) and disk image (.E01)

Received From: Public forensic training datasets and CyberDefenders challenge materials

Acquired By: Madhumitha M





Hash Verification



SHA256: Documented separately within investigation records.



Action Log



Date \& Time	Action



15-May-2026 18:40	Evidence downloaded and preserved

15-May-2026 18:50	SHA256 hash verification completed

15-May-2026 19:20	Memory dump analyzed using Volatility3

15-May-2026 20:10	Disk image loaded into Autopsy

15-May-2026 20:45	Browser and system artifact analysis completed

15-May-2026 21:00	Investigation screenshots documented

15-May-2026 21:20	Findings compiled and investigation notes finalized



