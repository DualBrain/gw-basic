## Download GW-BASIC Software

---

[Download](Download.md) | [Games](Games.md) | [Tutorials](Tutorials.md) | [KindlyRat](KindlyRat.md) | [Mouse Support](MouseSupport.md) | [Links](Links.md) | [Is BASIC best?](IsBasicBest.md)

---

### GW-BASIC 3.23, The Last Official Release

Microsoft created GW-BASIC version 3.23 in 1987 and that was the last official, commercial one. It is unsurprisingly unsupported, but still under copyright so it can't be sold or distributed without permission.

- gwbasic.exe.zip: GW-BASIC executable for DOS
- gw-man.zip: GW-BASIC manual; official documentation and full command reference
- gw-man.pdf: GW-BASIC User's Guide and Reference for Kindle and other e-readers

Thomas Shaffner released *Microsoft GW-BASIC User's Guide and User's Reference* to the web and you can easily [find copies of it](http://www.google.com/search?q=gw-basic+user+guide).

---

### GW-BASIC on Windows 7+

*aka "Where do I download GW-BASIC for Windows 7, 8, 10 ... ?"*

GW-BASIC was last released in 1988 as you can see from any screenshot of its start screen. It's a 16-bit DOS executable that uses processor instructions no longer supported in modern, 64-bit CPU's / operating systems. Simply put: GW-BASIC.EXE cannot run directly on Windows!

Don't lose hope, because this is where emulators come in.

[DOSBox](http://dosbox.com) is the premier DOS emulator with the best support and works on multiple platforms. You'll just need a passing knowledge of DOS and how a filesystem works, but otherwise running in an emulator is straight forward, like running a virtual PC from ye olden times inside your fancy new toy.

*[Carlos Vazquez](http://laislapr.tk/) adds: The closest thing there is to a 64 bit gw basic is qb64 (a 64 bit clone of quick basic) i havent tested if qb64 runs gwbasic programs (quickbasic could run them and even save them in binary form) ([QB64](http://www.qb64.net))*

---

### Compiling GW-BASIC Programs

*aka "How to convert gw-basic programs to exe extension?"*

What you're talking about is compiling the BAS file to an executable.

There are three immediate and essentially free options:

1. BASCOM is a program intended to compile BAS to EXE for BASICA, IBM's version of BASIC for DOS and the precursor to GW-BASIC. It will handle both the binary and ASCII format BAS files and supports pretty much everything except EGA (certain SCREEN modes).  
2. QuickBASIC 4.5 is the direct successor to GW-BASIC and can handle probably 95% of all GW-BASIC programs with the exception of those that rely on more esoteric features.  
3. FreeBASIC has little development going on but it theoretically handles almost all QB programs and so will handle GW-BASIC programs as well.  

Backstory: I keep seeing this question, [asked on Yahoo! Answers](http://web.archive.org/web/20160412174036/https://answers.yahoo.com/question/index?qid=20080929193512AADtsZ0), come up in search results. It's two years too late and the question is set to resolved, but I had to add some more information.

---

### GW-BASIC 3.23, The Last Official Release

Microsoft created GW-BASIC version 3.23 in 1987 and that was the last official, commercial one. It is unsurprisingly unsupported, but still under copyright so it can't be sold or distributed without permission.

- gwbasic.exe.zip: GW-BASIC executable for DOS
- gw-man.zip: GW-BASIC manual (official documentation)
- gw-man.pdf: GW-BASIC User's Guide and Reference for Kindle and other e-readers

---

### QBASIC.EXE in OLDDOS.EXE

Microsoft OLDDOS.EXE contains QBasic (which can run most GW-BASIC programs saved as ASCII) and several other "old DOS" utilities.

This was mirrored from http://support.microsoft.com/kb/135315.

---

### PC-BASIC 3.23

GW-BASIC for modern incarnations of Windows and Linux? Yes! Here is an email from the project's creator Rob.

Hi, I thought you might enjoy my newly released project PC-BASIC 3.23.

It's essentially an open source clone of the GW-BASIC 3.23 interpreter; since it's python-based, it runs on most OSes including Windows and Linux.
It is largely feature complete (including sound, graphics, file I/O, and loading and saving 'protected' programs) though still under active development. Have fun!

---

### SilverLight BASIC Interpreter

You can play with the work-in-progress version at http://www.addressof.com/basic/

For the most part, all keywords that are not machine language specific should be working to one degree or another. All graphics modes circa GW-BASIC should be working as well. You can drag/drop .BAS files directly to the editing surface to ease getting something up and working right away. All files are stored in your browser sand-box. Contact the author, Cory Smith, directly by visiting http://addressof.com.

---

### BASIC-80 Interpreter for Windows

- basic-80.zip: This comes from the pleasant Steve Pagliarulo who has graciously given me permission to attach a copy of this wonderful software he has developed. If you have any comments or questions, you can email him at s_pagliarulo AT hotmail.com.

I too share your fondness of GW-BASIC and its father BASIC-80. I got my start on a TRS-80 with Microsoft's LEVEL II BASIC. In any case, I'd like to share with you my BASIC-80 compatible interpreter that I finished late last year. It's very close to GW-BASIC but without the graphics commands. It can also load/run many GW-BASIC programs.

I've been fooling with the interpreter for about 10 years. I finally finished it because when I moved to 64-bit Windows, the 16-bit GW-BASIC .exe is no longer spported. The interpreter is about 20 thousand lines of C++ code. It is portable for the most part. Some of the OS specific APIs have to be changed for other platforms. For right now, I have it working as a 32-bit .exe on Windows. I'm thinking of porting it next to Raspberry pi.

I've attached a link to a zip file with BASIC.EXE interpreter and a few sample programs including a chess program writthn for GW-BASIC. Unlike GW-BASIC, this interpreter does not have a full-screen editor. It uses the original editor from BASIC-80. To edit a line you have to use the EDIT command.

---

### GW-BASIC vs FreeBASIC

There are, I'm finding, significant differences between GW-BASIC and FreeBASIC. For the first, you actually have to specify -lang deprecated in order to even support line numbers. So the compatibility goal of FreeBASIC being equivalent to QBasic is immediately suspect. What I'm looking for is a compiler to create modern operating system executables (Windows XP+, Ubuntu, OS X, etc.) with full support for GW-BASIC's language, or even QB.

KEY OFF not supported, for obvious reasons. QB ignores this command but FBC (FreeBASIC compiler) blows up with an error. If I can't tell it to ignore certain statements then right away I have to fork my code for a FBC version.

KEY (#) ON/OFF and ON KEY (#) GOSUB not supported. This is really annoying, but I already made changes to support INKEY$ polling in QB so that will supposedly work in FBC.

DEF FNname() not supported. You can create full-blown functions but not simple one-liners in the GW style. For me this is another indication I'll have to fork. I don't think this would be difficult for them to implement, perhaps I'll post it on their forum.

EXTERR() not supported. I'm not using this, but how hard would it be to support?

GOSUB # ... RETURN doesn't work unless you specify "-lang qb". The line number support can be enabled with "-lang deprecated" and yet if you try to call RETURN it reports "Illegal outside blah blah blah or SUB block".

SCREEN() isn't supported. For this I don't mean the routine to switch screen modes but rather the function that returns the value at a location in the text screen buffer. It seems to think I'm declaring a variable by this name.

Perhaps the FreeBASIC team would be interested in fixing these, though probably not. Development appears to have slowed down and why would support extend so far back? Still, I wish there was something I could use without having to roll my own (which I'm considering).
