# Checking Disk Space on Windows and Linux

As a part of Automation or resolving issue we always come across situations where we need quick tools to find out the most disk space consuming files or folder so to take required action and restore environment. In this document have just listed method that can be used on Windows or Linux

**On Windows, we can use two options**

1. Use Explorer to check the folder size using Properties option on folders ( this can be tedious and requires time to check all)
2. Use Powershell to understand the top 25 files consuming the disk space

   * Get-ChildItem c:\ -r| sort -descending -property length | select -first 10 name, Length, Directory,@{Name="MB";Expression={[Math]::round($_.length / 1MB, 2)}}
   ###### _Directory_ will provide the dir name where the file located, it comes handy when to decide which file to delete
   ###### The _–r_ (Recurse) key means that all subfolder will be searched recursively. You can restrict the check to a certain depth level using –Depth parameter. If you don’t specify the path, all subfolders of the current directory will be searched.

###### More details can be found on : http://woshub.com/find-large-files-with-powershell/

**On Linux or Unix we can use below**

Options : 

_**$ du | sort –n –r**_

Here we are passing the du output to sort command so we can sort the output according to our need

**$ du  -ah | sort –h**

Here we are using -ah as a human readable format. 

**_$ find . -type f -ls | sort -n -k7_**

Here we are using _find_ command to find the file and then use _sort_ to sort them according to our need.