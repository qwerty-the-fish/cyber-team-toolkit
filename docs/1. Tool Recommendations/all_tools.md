# Our Favourite Tools

With so many useful tools out there, it can be challenging to know where to begin. The following recommendations are broken down by purpose/category.

!!! note "**Adding a new tool?**"
    If the existing categories don't quite fit the tool - why not add a new one?

---

## General
- [CyberChef](https://gchq.github.io/CyberChef/) - a toolkit with a host of options, from cryptography tools to image editing tools to networking tools
- [SecLists](https://github.com/danielmiessler/SecLists/) - "a wordlist for everything"
- [ImHex](https://github.com/WerWolv/ImHex) - free hex editor (colourful UI)
- [010Editor](https://www.sweetscape.com/010editor/) - paid (with free trial) hex editor that has some really great scripts for identifying countless file types
- [msfvenom](https://github.com/rapid7/metasploit-framework) - part of metasploit, generates one-liner commands for reverse shell creation
    - documentation: https://www.offsec.com/metasploit-unleashed/msfvenom/
- [GTFOBins](https://gtfobins.github.io/) - a curated list of Unix binaries that can be used to bypass local security restrictions in misconfigured systems
- [Android Debug Bridge](https://developer.android.com/tools/adb) - CLI tool that lets you communicate with an Android device
    - [additional information](https://github.com/qwerty-the-fish/cyber-team-toolkit/blob/main/tools/adb.md)
- [Frida](https://frida.re/) - dynamic instrumentation toolkit for interacting with black box processes

---

## Web Exploitation
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/) - an amazing collection of payloads and bypasses for web exploitation
- [fuff](https://github.com/ffuf/ffuf) - a web fuzzer for discovering elements/content within web applications and servers (FUFF stands for "Fuzz Faster yoU Fool")
    - As correctly titled, a guide to everything you need to know about fuff: https://codingo.io/tools/ffuf/bounty/2020/09/17/everything-you-need-to-know-about-ffuf.html
- [PHP Reverse Shell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php) - (note: some recent comments regarding this no longer working) - script for triggering a reverse shell setup
- [BrowserBruter](https://github.com/netsquare/BrowserBruter) - web form fuzzing automation tool

---

## Binary Exploitation
- [Ghidra](https://ghidra-sre.org/) - really useful for reverse engineering a binary
- [apktool](https://apktool.org/) - for reverse-engineering Android APKs
    - a useful tip pointed out to me recently: `unzip someapkfile.apk` sort of works as well
    - converts `classes.dex` into the intermediary language `smali`
- [gdb](https://sourceware.org/gdb/) - CLI GNU-project debugger
- [checksec](https://github.com/slimm609/checksec) - bash script to check the properties of executables (like PIE, RELRO, Canaries, ASLR, Fortify Source)
- [jadx-gui](https://github.com/skylot/jadx) - dex to java decompiler
    - [feature overview](https://github.com/skylot/jadx/wiki/jadx-gui-features-overview)
- [dex2jar](https://github.com/pxb1988/dex2jar) - tools to work with Android `.dex` files and Java 
- [Bytecode Viewer](https://bytecodeviewer.com/) - open-source java reverse engineering suite (lets you see the Java and smali code side-by-side)

---

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

---

## Forensics
- [exiftool](https://exiftool.org/) - read, edit, and write metadata
- [bkcrack](https://github.com/kimci86/bkcrack/tree/master) - exploiting password protected ZIP files
    - uses Biham and Kocher's known plaintext attack on the PKZIP stream cipher ([paper outlining the attack](https://doi.org/10.1007/3-540-60590-8_12))
    - useful tutorial page: https://github.com/kimci86/bkcrack/blob/master/example/tutorial.md
- [binwalk](https://github.com/ReFirmLabs/binwalk) - analyse a file and search for potential embedded files

---

### Images / Audio
- [Aperi'Solve](https://aperisolve.fr/) - great tool for image analysis
- [Image Magick](https://imagemagick.org) - incredible collection of image-related tools
    - `identify` is particularly useful for identifying the correct format of a file (similar to `file` command)
- [SilentEye](https://achorein.github.io/silenteye/) - audio and image steganography
- [DTMF Decoder](https://dtmf.netlify.app/) - takes an audio file and converts the dial tones to their values 
- [MP3Stego](https://www.petitcolas.net/steganography/mp3stego/) - audio steganography
- [Split a GIF](https://ezgif.com/split) - sometimes you might need to split a GIF into its individual frames

---

### Memory
- [Volatility](https://github.com/volatilityfoundation/volatility3) - framework for extracting digital artifacts from volatile memory (RAM) samples
    - additional information: https://github.com/volatilityfoundation/volatility/wiki/Command-Reference

---
 
## Cryptography / Encoding
- [base64decode](base64decode.org) - can also just use CyberChef but this makes charcode conversion easier
- [dcode: cipher identifier](https://www.dcode.fr/cipher-identifier) - attempts to identify the cipher used with varying success
- [Cipher Identifier](https://www.boxentriq.com/code-breaking/cipher-identifier) - also attempts to identify the cipher used with varying success
- [dcode: Caesar cipher solver](https://www.dcode.fr/caesar-cipher) - tries all possible shifts and highlights the most likely ones
- [Crackstation](https://crackstation.net/) - password hash cracker

---

## OSINT
- [OSINT Framework](https://osintframework.com/) - an incredible collection of OSINT tools
- [Sherlock](https://github.com/sherlock-project/sherlock) - find usernames across a range of sites (social media)
- [TinEye](https://tineye.com/) - really good reverse image lookup tool
- [WhoIs](http://whois.domaintools.com/) - domain lookup tool, for availability and ownership details
- [Shodan](https://www.shodan.io/) - search engine for Internet-connected devices
- [OSINT Start.me](https://start.me/p/p6Noje/osint) - a comprehensive collection of OSINT tools covering data breaches, social media, and public records
- [Mailinator](https://www.mailinator.com/) - temporary email service, allowing for one-time communication and registration
- [Hootsuite](https://www.hootsuite.com/), [Buffer](https://buffer.com/), and [TweetDeck](https://github.com/dimdenGD/OldTweetDeck) - all provide centralised social media management, allowing you to monitor comments/DMs/interactions and schedule posts in one-place
- [ThisPersonDoesNotExist](ThisPersonDoesNotExist.com) - AI-generated profile pictures to use for creating profiles
- [Fake Name Generator](https://www.fakenamegenerator.com/) - creates entire fake personalities with names, addresses, login details, DOBs, physical descriptors, and much much more...
- Fake likes/follows/shares tools - with the increased focus on bot identification, these are becoming less popular and more unreliable - you run the risk of having your account deactivated for having fake followers, or someone might become suspicious and use one of many tools available to check if you have fake followers
- [Ivory - RIP TweetBot](https://tapbots.com/ivory/) - can be used to mimic human behaviour when it comes to running a Twitter (X) account - still in early development however, and currently only available for use on Apple products
