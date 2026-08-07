# Powershell Log Analysis
This summer, I finally completed TryHackMe’s SOC Level 1 course – a task I’ve procrastinated for 
months. The _Windows Security Monitoring_ and _Linux Security Monitoring_ modules serve as the inspiration for this project.

Both operating systems are relevant to most enterprises, Windows for workstations and laptops, and Linux (particularly Ubuntu, Apache, nginx) for file servers or web-servers. 
And because they are two different systems, the methods used to analyze logs on each system are not the same.
Linux simply requires a security analyst to access the files, 
conveniently stored in text-based `.log` file formats, and use tools like `grep`, `awk` `sed` or `auditd` to extract required IoCs.


Windows, on the other hand, requires Event Viewer. And using Event Viewer on a cloud-hosted virtual machine from TryHackMe is a mind-numbing experience that I never want to replicate again. 
However, I found a Medium article that taught a console-based way to extract logs. I can’t find the specific article, but if you can tell based on the following code snippet, I’ll appreciate the lead:
```
$Events = Get-WinEvent -Path 'C:\Users\user\Desktop\Incident Files\sysmon.evtx' 
| Where-Object {$_.Properties.Value -like "*doc*"} 
| Select-Object TimeCreated, ID, @{Name="Message";Expression={ $_.Properties.Value }} 
ForEach($Event in $Events)
{Write-Host " "
$Event.TimeCreated
$Event.ID
$Event.Properties.Value
Write-Host " "
}
```
So, this is the objective of this project – a space to report on the syntax used to analyze `.evtx` log files, preceeded by an executive summary, and the IoCs that I’m trying to look for.
