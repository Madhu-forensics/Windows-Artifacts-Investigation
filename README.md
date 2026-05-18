# Windows-Artifacts-Investigation
A complete, documented Windows disk and memory forensic investigation built from scratch including hash-verified evidence acquisition, artifact analysis, timeline reconstruction, and a court-admissible style forensic report with full chain-of-custody log.

What This Project Is


This project simulates a real digital forensic investigation on a Windows system. Starting from a forensic disk image, I performed the same workflow a forensic analyst would use in a law enforcement case:
Verified evidence integrity before any analysis
Used Autopsy to extract Windows artifacts (Prefetch, Registry, browser history, deleted files)
Ran Volatility3 on a memory dump to identify suspicious processes and network connections
Documented all findings in a court-admissible forensic report
Maintained a chain-of-custody log throughout
Built to demonstrate forensic skills for roles in digital forensics and cybercrime investigation.

Tools Used
Tool	Version	Purpose
Autopsy	4.21	Disk image analysis and artifact extraction
Volatility3	2.7.0	Memory dump analysis
PowerShell	Built-in	File hashing (MD5 / SHA256)

Evidence Source
Image type: CTF forensic disk image (.E01)
Source:  NIST CFReDS
OS on image: Windows 10
Memory dump: CyberDefenders.org — Blue Team Forensics challenge
> All evidence is from a publicly available CTF challenge, used for educational purposes.

Methodology

Step 1 — Evidence Integrity (Pre-Analysis Hashing)
Before opening the image, I generated SHA256 hashes to create a verifiable baseline.
powershell
Get-FileHash .\\2020JimmyWilson.E01 -Algorithm SHA256
hash values were recorded in the chain-of-custody log before any analysis began.


Step 2 — Case Setup in Autopsy
Created a new case in Autopsy 4.21 and loaded the disk image as a data source.
Ingest modules enabled:
Recent Activity (browser history, downloads, recently opened files)
Hash Lookup
File Type Identification
Keyword Search
Extension Mismatch Detector
Autopsy completed the scan in approximately 12 minutes. All findings were reviewed


Step 3 — Prefetch File Analysis
Prefetch files record every program execution on Windows including programs that were later deleted.
Autopsy path: `Results → Extracted Content → Run Programs`
Key findings:
Program	Last Executed	Run Count
WMIADAP.EXE	20-02-2014	48
WMIPRVSE.EXE	20-02-2014	83
WUAUCLT.EXE	19-02-2014	22


Step 4 — Registry Analysis
The Windows Registry records USB device history, recently opened files, and installed software — even after deletion.
Autopsy path: `Results → Extracted Content → Devices Attached / Recent Documents`


Step 5 — Deleted File Recovery
Autopsy scans unallocated disk space and orphaned MFT entries to recover deleted files.
Autopsy path: `Views → Deleted Files` 
Method: File carving — Autopsy identifies file headers and footers in raw disk space to reconstruct files even without directory entries.
Finding: Three documents were recovered from unallocated space. File names and partial content were recovered and documented 


Step 6 — Browser Artifact Analysis
Firefox and Edge browsing history is stored as a SQLite database at:
`AppData\\Local\\Google\\Chrome\\User Data\\Default\\History`
Autopsy path: `Results → Extracted Content → Web History / Web Downloads / Web Search`
Findings documented: URLs visited, search terms used, files downloaded, timestamps of activity.


Step 7 — Memory Forensics with Volatility3
A memory dump was analysed using Volatility3 to identify what was running at the time of capture.
Commands used:
OS identification
python vol.py -f memory.raw windows.info
Running processes
python vol.py -f memory.raw windows.pslist
Process family tree
python vol.py -f memory.raw windows.pstree
Processes hiding from OS (rootkit detection)
python vol.py -f memory.raw windows.psscan
Active network connections
python vol.py -f memory.raw windows.netscan

What I Learned

How Windows Prefetch files prove program execution even after deletion

How the USBSTOR registry key records every USB device ever connected

How to recover deleted files by scanning unallocated disk space in Autopsy

How to detect hidden/rootkit processes by comparing `pslist` vs `psscan` in Volatility3

How to structure forensic findings for legal admissibility

The importance of pre- and post-analysis hashing for evidence integrity


Author
Madhumitha M
MSc Cyber Forensics & Information Security — Dr. M.G.R. Educational and Research Institute, Chennai
madhumithamas@gmail.com 


Disclaimer
This project uses publicly available CTF challenge images for educational purposes only. All analysis was performed in an isolated environment. No real personal data was used.
