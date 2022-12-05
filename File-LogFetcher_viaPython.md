# Starting a File transfer service using Python on server

As a part of PROD support we always come across a situation where we wanted to transfer file from one machine to other.
We can leverage SFTP or other FTP services however Python provides a better way where we can use http module to download the required files.
This method will help to download (only allowed) files from Servers to your own local machine and vice-versa

## Here is the sample code

_nohup python -m http.server 12345 >/dev/null 2>&1 &_

###### **Caution**: HTTP server will start on the same dir where you fire this command, so make sure you fire this command only from the required and permitted location like /log.
