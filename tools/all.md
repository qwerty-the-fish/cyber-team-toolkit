# Toolkit Overview

With so many useful tools out there, it can be challenging to know where to begin. The following recommendations are broken down by purpose/category.

> Adding a new tool? Add it to the appropriate category if it exists - but feel free to add another category if something else would be more suitable!

## General
- [CyberChef](https://gchq.github.io/CyberChef/) - a toolkit with a host of options, from cryptography tools to image editing tools to networking tools
- [SecLists](https://github.com/danielmiessler/SecLists/) - "a wordlist for everything"
- [ImHex](https://github.com/WerWolv/ImHex) - free hex editor (colourful UI)
- [010Editor](https://www.sweetscape.com/010editor/) - paid (with free trial) hex editor that has some really great scripts for identifying countless file types
- [msfvenom](https://github.com/rapid7/metasploit-framework) - part of metasploit, generates one-liner commands for reverse shell creation
    - documentation: https://www.offsec.com/metasploit-unleashed/msfvenom/
- [GTFOBins](https://gtfobins.github.io/) - a curated list of Unix binaries that can be used to bypass local security restrictions in misconfigured systems

## Web Exploitation
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/) - an amazing collection of payloads and bypasses for web exploitation
- [fuff](https://github.com/ffuf/ffuf) - a web fuzzer for discovering elements/content within web applications and servers (FUFF stands for "Fuzz Faster yoU Fool")
    - As correctly titled, a guide to everything you need to know about fuff: https://codingo.io/tools/ffuf/bounty/2020/09/17/everything-you-need-to-know-about-ffuf.html
- [PHP Reverse Shell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php) - (note: some recent comments regarding this no longer working) - script for triggering a reverse shell setup
- [BrowserBruter](https://github.com/netsquare/BrowserBruter) - web form fuzzing automation tool

## Binary Exploitation
- [Ghidra](https://ghidra-sre.org/) - really useful for reverse engineering a binary
- [apktool](https://apktool.org/) - for reverse-engineering Android APKs
    - a useful tip pointed out to me recently: `unzip someapkfile.apk` sort of works as well
- [gdb](https://sourceware.org/gdb/) - CLI GNU-project debugger

## Network Exploitation
- [Burp Suite](https://portswigger.net/burp) - analyse network traffic and intercept/inspect/alter/drop/etc. packets
- [Postman](https://www.postman.com/) - allows for easy API interaction
- [curl](https://curl.se/) - CLI tool for transferring data with URLs
- [nmap](https://nmap.org/) - network/port scanner
- [nc](https://nmap.org/ncat/) - also known as netcat, a CLI tool for reading and writing data across networks
- [FuzzHttpBypass](https://github.com/carlospolop/fuzzhttpbypass) - fuzzing to try and bypass unknown authentication methods
- [Wireshark](https://www.wireshark.org/) - network packet analysis software (filter by protocol, follow streams, etc.)
    - https://ctf101.org/forensics/what-is-wireshark/
- [tshark](https://www.wireshark.org/docs/man-pages/tshark.html) - CLI wireshark
- [NetworkMiner](https://www.netresec.com/?page=NetworkMiner) - PCAP file analyser - can be a useful first-step before using wireshark
    - note: the free version does not support `.PCAPNG` files so if you need to convert one: "open the PcapNG file in Wireshark and click “File, Save As...”. Then select the “Wireshark/tcpdump/... - pcap” option in the “Save as type” drop-down list." (https://www.netresec.com/?page=Blog&month=2012-12&post=HowTo-handle-PcapNG-files)

## Forensics
- [exiftool](https://exiftool.org/) - read, edit, and write metadata
- [bkcrack](https://github.com/kimci86/bkcrack/tree/master) - exploiting password protected ZIP files
    - uses Biham and Kocher's known plaintext attack on the PKZIP stream cipher ([paper outlining the attack](https://doi.org/10.1007/3-540-60590-8_12))
    - useful tutorial page: https://github.com/kimci86/bkcrack/blob/master/example/tutorial.md

### Images / Audio
- [Aperi'Solve](https://aperisolve.fr/) - great tool for image analysis
- [Image Magick](https://imagemagick.org) - incredible collection of image-related tools
    - `identify` is particularly useful for identifying the correct format of a file (similar to `file` command)
- [SilentEye](https://achorein.github.io/silenteye/) - audio and image steganography
- [DTMF Decoder](https://dtmf.netlify.app/) - takes an audio file and converts the dial tones to their values 
- [MP3Stego](https://www.petitcolas.net/steganography/mp3stego/) - audio steganography
- [Split a GIF](https://ezgif.com/split) - sometimes you might need to split a GIF into its individual frames

### Memory
- [Volatility](https://github.com/volatilityfoundation/volatility3) - framework for extracting digital artifacts from volatile memory (RAM) samples
    - additional information: https://github.com/volatilityfoundation/volatility/wiki/Command-Reference
 
## Cryptography / Encoding
- [base64decode](base64decode.org) - can also just use CyberChef but this makes charcode conversion easier
- [dcode: cipher identifier](https://www.dcode.fr/cipher-identifier) - attempts to identify the cipher used with varying success
- [Cipher Identifier](https://www.boxentriq.com/code-breaking/cipher-identifier) - also attempts to identify the cipher used with varying success
- [dcode: Caesar cipher solver](https://www.dcode.fr/caesar-cipher) - tries all possible shifts and highlights the most likely ones

## OSINT
- [OSINT Framework](https://osintframework.com/) - an incredible collection of OSINT tools
- [Sherlock](https://github.com/sherlock-project/sherlock) - find usernames across a range of sites (social media)
- [TinEye](https://tineye.com/) - really good reverse image lookup tool
- [WhoIs](http://whois.domaintools.com/) - domain lookup tool, for availability and ownership details
- [Shodan](https://www.shodan.io/) - search engine for Internet-connected devices
