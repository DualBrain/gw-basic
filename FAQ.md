## GW-BASIC FAQ

[Home](https://gw-basic.com) | [Tutorials](Tutorials.md) | [Games](Games.md) | [Resources](Resources.md) | [FAQ](FAQ.md)

---

### Where do I download GW-BASIC for Windows 7?

Nowhere, there is no such thing. There is no GW-BASIC for Windows 7!

I get this question to my contact form so often, I don't know why I haven't made a post or a page for it yet. GW-BASIC was last released in 1988 as you can see from any screenshot of its start screen. It's a 16-bit DOS executable that uses processor instructions no longer supported in modern, 64-bit CPU's / operating systems. Simply put: **GW-BASIC.EXE cannot run directly on Windows!** Don't lose hope, because this is where emulators come in. [DOSBox](http://www.dosbox.com) is the premier DOS emulator with the best support and works on multiple platforms (I use it on Lubuntu Linux). You'll just need a passing knowledge of DOS and how a filesystem works, but otherwise running in an emulator is straight forward, like running a virtual PC from ye olden times inside your fancy new toy.

With all that said, I'm particularly talking about 64-bit editions.  It is (maybe) possible to start on the 32-bit editions.

According to Jason Donahue...

*As for 32-bit Windows, though, I've just gotten GW-BASIC to run on a tablet running a 32-bit version of Windows 8.1 - when first running the executable, I was prompted to install the NTVDM, after which it opened fine.*

### How to convert gw-basic programs to "exe" extension?

What you're talking about is compiling the BAS file to an executable. There are three immediate and essentially free options:

1. BASCOM which is a program you can find on KindlyRat's GWBASIC site. This program was intended for BASICA, IBM's version of BASIC for DOS and the precursor to GW-BASIC. It will handle both the binary and ASCII format BAS files and supports pretty much everything except EGA (certain SCREEN modes).  
2. QuickBASIC 4.5 which is the direct successor to GW-BASIC and can handle probably 95% of all GW-BASIC programs with the exception of those that rely on more esoteric features. You can find it at http://phatcode.net.  
3. FreeBASIC has little development going on, but it theoretically handles almost all QB programs and so, again theoretically, will handle GW-BASIC programs as well. Find it and more information at http://www.freebasic.net/.  

Backstory: I keep seeing this question, asked on Yahoo! Answers, come up in search results. It's two years too late and the question is set to resolved, but I had to add some more information.
