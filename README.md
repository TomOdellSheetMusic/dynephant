#Dynephant 

I didn't manage to compile the autoit file, so you have to download [autoit](https://www.autoitscript.com/cgi-bin/getfile.pl?autoit3/autoit-v3-setup.exe) to edit and run the script. I will make a new release if I manage to figure that out.
Chriv said dynephant was brolen right now, but i noticed that it still updated my ip address but would bother me every 30 seconds about how it didn't work. All I did was replace the error message and set the timer that used to be for the error message to the daemon timer for waiting between checks.


Dynephant is a simple, open-source Dynamic DNS (DDNS) client for
Windows. It is intended to have as few dependencies as possible. It
was written, because, at the time of it's creation, very few DDNS
services had support for IPv6. More specifically, dynv6.com, a DDNS
service, had support for IPv6, but no real Windows client.

Currently, Dynephant only supports dynv6.com, but could easily be
adapted to work with other DDNS services as well.

Dynephant should run on most reasonably current versions of Windows
(and even some not so reasonably current). It requires valid IPv4 and
IPv6 TCP/IP stacks. To work correctly, it requires a working Internet
connection with support for IPv4 and IPv6. It contacts the dynv6.com
service via HTTPS (depending on Internet Explorer 3 or greater, which
should be present in all reasonably current versions of Windows).

It can be run either as an AutoIt3 script (requiring AutoIt3 to be
installed), or a pre-compiled executable (requiring no runtime not
already part of Windows). The dependency on IE for HTTPS creates
some intrinsic limitations on reporting of errors (namely, that
errors are known, but the cause is not automatically).

CLI and GUI, 32-bit and 64-bit versions are provided. Use the CLI
version if you want to monitor or redirect the stderr stream into
a log file. Use the GUI version if you want the program to run
without leaving a Command Prompt open.

##Table of Contents

* [Prerequisites](#prerequisites)
* [License](#license)
* [Usage](#usage)

##Prerequisites

* A relatively current version of Windows
* Internet Explorer 3 or higher installed

##Build requirements (if you want to build .exe from source)

* AutoIt3 (https://www.autoitscript.com)
* AutoIt3Wrapper (part of AutoIt3 by default)
* Au3Check (part of AutoIt3 by default)
* Tidy (part of AutoIt3 by default)
* GnuWin32's sed utility (http://gnuwin32.sourceforge.net/packages/sed.htm)
* Optional: Valid Code-signing certificate / key
* Optional: Windows 10 SDK's signtool (https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk)
* Optional: Working internet connection (needed to have signed timestamp on .exe files)
* Optional: NSIS's makensis (http://nsis.sourceforge.net/Download) (needed to build setup)

##License

Dynephant is licensed using the (extremely permissive) MIT license.
See the LICENSE.txt file.

The included icon is courtesy of http://www.how-to-draw-funny-cartoons.com
(link back required by author if used)

##Usage

First, you need an account with dynv6.com, with at least one host.

Once you have an account with dynv6.com, find your host name and
authentication token.

The command line arguments are:
currently irrelevant since there is now to execute the script using command line

You have to edit $host and $token on line 92 in the autoIT script.
Not setting $daemon results in only one update (or attempt) occurring.
Setting $daemon to less than 300 seconds (5 minutes) results in the default
of 1800 seconds (30 minutes) being used.
-host takes only the host name (leave off the dynv6.net part), not the FQDN.


The following example assumes your Fully Qualified Domain Name (FQDN)
for your host name is foobar.dynv6.net, and your authentication token
is randomtextforfoobarhere:

If you want Dynephant to automatically periodically set the AAAA
(IPv6 Address) record, but not the A (IPv4 Address) record for your host
every 10 minutes (600 seconds), you would run the autoIT script with lines 92-95 
like this:
```bat
$host = "foobar"
$token = "randomtextforfoobarhere"
$daemon = 600

