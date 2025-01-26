# Networks

A CTF challenge might give you a network address (port optional) and ask you to find the flag. So where do you begim?

## I have a port number
If the port provided is one of the commonly used ones, this might give a hint as to your next steps - lookup the common uses for the port provided (https://www.geeksforgeeks.org/50-common-ports-you-should-know/).

However, the port number may not be a commonly used one and therefore not give us any hints.

Some examples might be:
- port 80/8080/443: these ports are used for HTTP/HTTPS services and so we can use a web browser to access the website being hosted (i.e. search for `http://[IP_ADDRESS]:[PORT]` (or https depending on the port provided) and you should be able to see the website).
- port 21: this port is used for the File-Transfer Protocol (FTP) service so we can use commands such as `ftp [IP ADDRESS]` to connect
    - if anonymous login is allowed, when asked for the user we can simply provide `anonymous`
    - once connected, to get a known file we can use the command `get [FILE NAME]` 

## I don't have the port number
The tool `nmap` comes into play here, as we can use it to scan the provided IP address and get information about any open ports.
