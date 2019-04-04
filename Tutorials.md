## GW-BASIC Tutorials

---

[Download](Download.md) | [Games](Games.md) | [Tutorials](Tutorials.md) | [KindlyRat](KindlyRat.md) | [Mouse Support](MouseSupport.md) | [Links](Links.md) | [Is BASIC best?](IsBasicBest.md)

---

### Mouse Support By Daryl Dubbs

Howdy! Just thought you might be interested in sharing a simple program I wrote, perhaps a lifetime ago, which allows GW-Basic programmers to access mouse functions in their own programs. The code works by way of an absolute call to a machine code routine, which polls the mouse and then returns it's button status, and of course, it's X & Y co-ordinates.

The mouse sub-routine provides 3 simple functions; 1. Display the mouse cursor, 2. Hide the mouse cursor and, 3. Read the mouse button status and X/Y co-ordinates.

Calling the mouse sub-routine works like this:

1. Set the "FUNK" variable to either 1,2 or, 3 to tell the mouse routine which function to perform.
2. Call the mouse sub-routine via a gosub to the routine, at line number 200.
3. Read the "B", "H" and, "V" variables to get the mouse button status, horizontal co-ordinate and vertical co-ordinate, respectively.

As I alluded to earlier, "FUNK=1" displays the mouse cursor, while "FUNK=2" hides it and, "FUNK=3" reads the mouse data. The variable "B" returns the following values for a 2-button mouse:

- 0 = no buttons pressed
- 1 = left button pressed
- 2 = right button pressed
- 3 = both buttons pressed

Naturally, the variables "H" and "V" simply return the mouse co-ordinates directly.

I have included the full code for a simple demo program, which just draws a yellow dot at the mouse cursor when the left button is pressed, while pressing the right button clears the screen and, pressing both buttons (or any key) ends the program. The program itself is of little use, but to demonstrate how the mouse sub-routine is used. Once a programmer is familiar with how the code operates, he/she can simply copy the mouse routine into their own program, and begin accessing the mouse immediately.

The full code is as follows:

```
1 KEY OFF: CLS
2 SCREEN 9
3 FUNK = 1: GOSUB 200
4 FUNK = 3: GOSUB 200
5 LOCATE 1,1: PRINT B,H,V
6 IF B = 1 THEN PSET(H,V),14
7 IF B = 2 THEN CLS
8 IF B = 3 OR INKEY$ <>"" THEN GOTO 10
9 GOTO 3
10 FUNK =2: GOSUB 200: END

199 'Start of Mouse Sub-routine
200 POKE 0,184: POKE 1,FUNK: POKE2,0
201 POKE 3,205: POKE 4,51: POKE 5,137
202 POKE 6,30: POKE 7,170: POKE 8,10
203 POKE 9,137: POKE 10,14: POKE 11,187
204 POKE 12,11: POKE 13,137: POKE 14,22
205 POKE 15,204:POKE 16,12: POKE 17,203
206 AB = 0: CALL AB
207 B=PEEK(&HAAA)
208 H=PEEK(&HBBB) + PEEK(&HBBC) * 256
209 V=PEEK(&HCCC) + PEEK(&HCCD) * 256
210 RETURN
```

That's all there is to it! Next time I've got a few moments, I'll submit another program which plays digital audio through GW-Basic. (low-resolution, 8-bit, mono audio, but digital audio none the less!) Hope you and your readers will enjoy my code & so long for now!

1. The program requires a Microsoft or compatible mouse driver program, which must be loaded and running before it will work.
2. Function "2" (hide the mouse cursor) should be called before performing any graphics functions on screen, or else any graphics underneath the cursor itself will be garbled. And, finally,
3. If function "2" is called more than ONCE before calling function "1" to display the cursor again, then function "1" must be called THE SAME NUMBER OF TIMES to make the cursor visible. However, function "2" will ALWAYS hide the cursor! This is due to a quirk in the Microsoft mouse driver and cannot be changed, thus calling function "2" more than once should be avoided.

For comments and questions, contact Daryl via email: flurng AT gmail.com.

---

### Convert GW-BASIC to QBasic

The BASCOM compiler specified by KindlyRat and others works for most GW-BASIC and BASICA programs, but in particular it doesn't support EGA which made me look to Q-Basic for making an EXE of SPACESC.BAS. QuickBASIC 4.5, release in 1988, has the capability to do this but there's some things you need to be aware of.

First, you must save your BAS file as ASCII using ,a:

```
SAVE "myfile",a
```

The reason for this is by default GW-BASIC uses its own binary format that subsequent versions of BASIC do not understand. QuickBASIC also has a binary "quick" format, but it is not the same thing and they are not compatible with one another. Once you've done this you can load your program and note that QuickBASIC will go out of its way to standardize a lot of your white space around variables and stuff.

From this point your program will probably run, but may have some strange bugs. Here's the ones that I encountered:

SCREEN() **returns 32 instead of 0** for uninitialized parts of the text screen buffer. Presumably this is an optimization and honestly it's what I initially expected in GW-BASIC. That is, in GW-BASIC it will only return 32 if you explicitly put a space, e.g. CHR$(32), on that location. Thus QuickBASIC does not differentiate between cleared and undefined/not-set.

ON KEY([11,12,13,14]) **trap presses on number pad arrows** and not the main arrow keys. This was a real annoying bug to fix because it meant I had to add INKEY$ checking to my game-loop which I had hoped to avoid entirely. You'd think that adding a custom key trap would work, but it doesn't. The arrow keys simply will not be trapped with ON KEY which appears to me to be a colossal bug.

**Duplicate line numbers cause it to complain.** This is actually a good thing and helped me find a problem I introduced by editing my source outside of GW-BASIC. It always pays to double-check your work, even if it's a single line! I made this change and like an insane idiot, checked it in thinking I couldn't possibly have done anything wrong. GW-BASIC, when I tried it, simply overwrites the first occurrence with the second and off you go thinking all is swell.

CHAIN **no longer has** ALL, DELETE, **or** MERGE **options** in QB. Bummer if you used GW-BASIC's reliance on line numbers to your advantage with several modules.

BLOAD **and** BSAVE **work the same but** QB and GW-BASIC use different memory locations for similar functions so the result might be unexpected.

CALL **calls a subprogram in QB and not an assembly language routine**. So those fancy machine codes you POKE'd into memory no longer work. Doh!

And finally, **all the editor-specific commands no longer exist**: AUTO, CONT, DELETE, EDIT, LIST, LLIST, LOAD, MERGE, NEW, RENUM, RUN, and SAVE.

For more information, see also the Microsoft Support knowledge base article 72502 ([Converting Programs from GW-BASIC to QBasic](http://web.archive.org/web/20161121073821/http://support.microsoft.com/kb/72502)) and 73084 ([Differences Between GW-BASIC and QBasic](http://web.archive.org/web/20161121073821/http://support.microsoft.com/kb/73084)).

---

### How to Sleep, Wait, or Pause

GW-BASIC has no facility to pause the program for a set amount of time, blocking further interpretation of the code. The processor in the DOS days wasn't sharing itself with other applications, at least in the dustier darker days. You can wait for INPUT or INKEY$ and that'll give the CPU a chance to breath, but both of those require user interaction. Thus the prescribed method of waiting some span of moments fell to tight loops of dummy calculation to keep the interpreter busy.

Here's an enlightening passage of such a technique from page 158 of the GW-BASIC Self-Teaching Guide:

"You may have to use a loop to make the program pause; keys can be trapped while waiting for INKEY$ input. Or you could use a FOR...NEXT loop that does nothing several thousand times to pause the program briefly, then continue if nothing occurs."

Yikes, huh? I couldn't figure out a much better way, though. The ON TIMER event would be fantastic to use for a game loop, but it only accepts seconds (no milliseconds). Imagine, though, if it could take a fractional amount of seconds. You could have your main game loop hit a specific number of times per second, assuming the processor is fast enough to keep up. Then you could block the main "thread" with a simple A$ = INKEY$ line (trapping keys with ON KEY causes them not to get pushed to the input buffer).

No sense in dreaming, though. Since I'm working in relatively tight loops with very little wiggle room in terms of performance, I use the following syntax to keep the framerate sane:

```

1000 ' Main loop
1010 WHILE KL = 1
1020 T! = TIMER + (1 / FPS)
...
2000 WHILE TIMER < T!: WEND

```

You can even test this sort of thing out directly, Try entering this line into GW-BASIC:

```
T! = TIMER + 1: WHILE TIMER < T!: WEND
```

That will delay for precisely one second; or at least as close as you can get to it. However, I'm not sure about the precision of the TIMER even though it returns partial seconds. That is, you can delay for one and a half seconds with:

```
T! = TIMER + 1.5: WHILE TIMER < T!: WEND
```

Anyway, back to work ... just thought I'd make a note of this. Maybe I'll figure out a better way later. And no, GW-BASIC does not have the SLEEP command like was later added in QuickBASIC and Q-Basic.

---

** IF ... THEN ... Compound Statement

When I recently retook the helm of GW-BASIC programming, I found some things very restrictive and they forced me to invent relatively strange ways of solving simple flow problems. For instance, it wasn't until just this past week that I found you could cram more than one statement for the result of an IF/THEN!

```
IF condition THEN statement1 : statement2
```

The second statement will only be executed if the first is. I found this out when I had tried to cram two IF statements on the same line for bounds checking too small and too large, but only the too small check was working. Internally, the interpreter is literally stepping through your code and it will continue executing after THEN until it reaches ELSE.

Also, you can put an ELSE after a compound statement like this and even do an ELSE IF! Again, the interpreter skips ahead to see if an ELSE exists and then it executes the rest of the line as if it were its own line. Some confusing bugs can pop-up, though, and remember you can only have a line up to 255 characters long (not that you'd want such a hideous thing in your program).

---

### Interrupt and Stop a Running Program

An intrepid programmer named Don wrote to ask how to stop a running program:

    What I want to do is permanently assign a key to end a running program. Im finding that on some keyboards ctrl C works on others ctrl break and on my logitech ex100 there is a fn key next to the right ctrl key . using those two keys plus the break key also works on some programs where neither other combination works.

I didn't know the answer, and so gave him a bit of the run around with my meager knowledge, but later he came back with it himself:

    I have found the solution for stopping a running program. As i mentioned the ctrl+c and Ctrl+break combinations dont work. The solution i found after reading the source code preparing to apply patches is so simple i should have thought of it.

    The key combo that works in every instance i have tried is ctrl + scroll lock
    
I've tried this myself on DOSbox in Ubuntu and sure enough it interrupts the program every time. All this time I've simply given up if a program hit an infinite loop that I couldn't break out of and re-coded what I'd neglected to save after killing the process. Thanks Don, what a time saver!

Today I was still curious about this and did a quick search, coming up with this post on VOGONS:

   I have a little trick for those interested: use Ctrl-ScrollLock, it behaves like Ctrl-Break with many BASIC interpreters running within DOSBox. It works with GW-BASIC, BASICA (often bundled with compatible DOSes like Compaq's), QBasic, QuickBasic, and possibly other development "workbench" interfaces.

   The reason this works is a little complicated, so only read on if you're interested in knowing. DOSBox does not have true Ctrl-Break handling like real DOS, which is a combination of hardware and software interrupts and internal flags. However, the DOS Ctrl-Break handler is only a default handler that all starts with INT 9, the keyboard hardware interrupt. Many of the program development apps hook INT 9 and intercept keys before DOS sees them, so they can do their own processing. After all, the DOS default behavior for Ctrl-Break is to terminate the app, and that is often not what is wanted. The INT 9 handler code looks for the Control key being depressed by checking the shift status byte in BIOS data, and then reads scancodes from the keyboard data port 60h. The scancode for ScrollLock is 46h, and the scancode for Ctrl-Break is a 2-byte "escaped" sequence of E0h 46h, where E0h is the escape code. It seems the handler routines are often not very rigorous in their processing of the escape code, and just drop it, so Ctrl-ScrollLock ends up working the same as Ctrl-Break.

   A lucky break for us!

---

### Convert to Integer (avoid CINT/INT)

GW-BASIC is a strongly-typed language but it favors single-precision floats and will automatically convert numeric values between floating-point and integer without requiring casting (as would be the case in C-style languages). Additionally there are three explicit functions for this purpose: FIX(), INT(), and CINT(). What are the differences between them, when would you use one over the others or not at all? Lastly, I'll discuss converting a string to an integer using VAL() in concert with the other techniques.

First, let's talk implicit conversion. This is what happens when you assign a numeric value, possibly a real number stored as floating point, to an integer without any special function. For example in the following snippet, integer I% is given the value of float N! and the result is printed to the screen:

```
N! = 3.14
I% = N!
PRINT I%
```

3 is displayed, which isn't all that surprising. However, what if you had a fractional value over half of one?

```
I% = 9.95
PRINT I%
```

The output is 10, which can be quite a shock to long-term programmers but probably less to the newly initiated. Outside of computers we tend to round one way or the other and GW-BASIC does this for implicit conversions, but many languages truncate the result instead. That is, in C or Java the output would be 9. This is a really important snarl that has caused me no few amount of bugs, especially in conjunction with RND!

CINT() is the functional corollary, that is it does exactly the same thing. I suppose you'd use it when you want to show, for readability in your program, that you really do want rounding to occur, but otherwise I believe it's unnecessary. Generally I've used CINT without realizing what it did, thinking it merely "Casted to INTeger" as one would do in C and erroneously assuming the fractional portion would be cut off and not used for rounding. My recommendation: just don't use it, since it's what GW-BASIC does automagically.

What about FIX() and INT()? These two appear identical in that they perform truncation from fractional to whole, but there is a tiny but significant difference that could also cause numerous programming flaws. The manual states "FIX does not round off numbers, it simply eliminates the decimal point and all characters to the right of the decimal point" whereas for INT() it comments "Negative numbers return the next lowest number". In CINT it mentions both with "See the FIX and INT functions, both of which return integers".

So we know that they both truncate, but then INT() also does that extra magic of making a negative number even more negative. Why? I don't know the answer to this offhand, but it's likely to cause grief when merely expecting truncation. For example:

```
PRINT INT(-3.14), INT(-9.95)
```

The output is -4 and -10, so basically it's going to round to the next whole number no matter what is after the decimal point if the number is negative. I don't understand the logic here and thus my recommendation, like with CINT(), is to avoid INT() altogether.

Finally, note that all of these accept numeric parameters only. In order to convert from a string, you can use VAL(). The important point I want to make is that this function returns a real number, e.g. floating-point, not an integer. So if you assign the result to an integer without calling FIX(), it will round.

```
I% = VAL("9.95")
PRINT I%
I% = FIX(VAL("9.95"))
PRINT I%
```

After running the above you'll see 10 and 9. So remember to call FIX() to truncate your numeric values for integer variables and use the implicit conversion when you want them rounded up or down.

One last note about INT(): there is a bug with it and PRINT whereby you can pass in a string to it and it will do some funky stuff. Give this a try, but don't cry to me when you see a bunch of psuedo-random garbage (e.g. memory dump) printed on your screen:

```
PRINT INT("9.95")
```

---

### EGA Lighting Effects

Yes, I've come upon a method for doing a sort of lighting effect in GW-BASIC's SCREEN 7 (EGA mode). It makes use of PUT/XOR and a custom PALETTE to allow sprites to be fully or partially "lit" and otherwise remain a shadow color (dark gray).

The graphics command PUT has an action verb parameter which determines how all the pixel values are combined between the sprite and the background. There are five such options: PSET, PRESET, AND, OR, and XOR. This last is an abbreviation for "exclusive or" which switches all the bits. It is commonly used to non-destructively place a sprite and then remove it, but has the odd side-effect of discoloring overlapping graphics.

--missing image--

Since the pixel value is actually being changed in a predictable manner, you can draw your graphics with one set of values (say 4, 5, 6, 7) and when a "light" pixel is XOR'ed it will change them to a new set (11, 10, 9, 8). Thus you can set the first set to gray, the second to the actual colors, and then they'll show up when the light sprite is PUT on top with XOR.

---

### BASCOM and ON ERROR

By default BASCOM does not support ON ERROR; apparently this is for optimization purposes. Thus if you compile your program and it contains anything that passes syntax but is not supported, it will crash at runtime. Thankfully, it will at least tell you that ON ERROR is ... well ... an error, but I initially thought that was just because it didn't know what it was at all.

Let's take the following example program called SCREEN7.BAS:

```
10 ON ERROR GOTO 50
20 SCREEN 7
30 WHILE INKEY$ = "": WEND
40 SCREEN 0: WIDTH 80: END
50 PRINT "SCREEN 7 is not supported"
```

Trying to compile this without any arguments to BASCOM.EXE results in the following:

```
IBM Personal Computer BASIC Compiler
(C) Copyright IBM Corp. 1982, 1983, 1984, 1985 Version 2.00
(C) Copyright Microsoft Corp. 1982, 1983, 1984, 1985

Object filename [SCREEN7.OBJ]:
Source listing [NUL.LST]:
003A 0006 10 ON ERROR GOTO 50
^ /E

50434 Bytes Available
50161 Bytes Free

0 Warning Error(s)
1 Severe Error(s)
```

The shrewd among you may have already picked up on what it's trying to say, but I just didn't get it. I commented out line 10, compiled fine, linked, and ran to get the following result:

```
Illegal function call in module SCREEN7 at address 018B:0040

Hit any key to return to system
```

The fix? Add /E when you compile; like so:

```
BASCOM.EXE SCREEN7.BAS /E
```

Voila!

With this capability you can detect that your program is running under BASCOM and react accordingly (fallback to SCREEN 1, etc.).

Thanks goes to na_th_an for his [Compiling and Linking with BASCOM 1.0 and 2.0](http://web.archive.org/web/20161121073821/http://www.ojodepez-fanzine.net/network/qbdl/bascom-compiling-and-linking.html) page.

Also, use /X for RESUME NEXT support. So when I compile, here's what I use:

```
BASCOM.EXE PROGRAM.BAS /E /V /O /X
```

---

### Saving EGA Video Pages

Recently I've been messing with saving off the EGA video pages to disk files for later retrieval, specifically those from SCREEN 7 which is a 320x200 resolution with 16 colors. Check out EGAPGSV.BAS for my ongoing code quest for this purpose.

Initially I remembered from my VGA days that 0xA000 is usually the graphics screen address, so in my first attempt I BSAVE'd that like so:

```
10 SCREEN 7
20 LOCATE 1,1: PRINT "Blah blah"
30 DEF SEG = &HA000
40 BSAVE "TEST.IMG", 0, 32000
```

The DEF SEG statement is used to tell GW-BASIC what memory you're interested in. Then the BSAVE says to create the file TEST.IMG, starting at offset zero, with 32,000 bytes (320 x 200 = 64,000 / 2 = 32,000). For 16 colors each pixel would be 4 bits or half a byte. 

This does and doesn't work. Sure the EGA screen mode starts at the same address as its successor VGA modes, but SCREEN 7 (mode 0x0D, 13 decimal) stores the pixels on 4 planes.as explained by Dan Rollins on [Video Memory Layouts](http://web.archive.org/web/20161121073821/http://webpages.charter.net/danrollins/techhelp/0089.HTM). Thus my short example, if you were to BLOAD the result, has only white pixels. When I first tried this, since I was using only text, it appeared to work due to this. However, if you use any additional colors, you'll note they don't show up except as either white or black. 

One additional problem is that this only works for the first (indexed by zero) video page and you can have 8 (with [256k](http://web.archive.org/web/20161121073821/http://support.microsoft.com/kb/58567) of graphics memory) 

A couple days ago I hit pay dirt with Microsoft Knowledge Base article 45699: [Complete Instructions to BLOAD and BSAVE EGA and VGA Screens](http://web.archive.org/web/20161121073821/http://support.microsoft.com/kb/45699). The problem is that you can't save a single file; again due to the four planes you must save four files. So this won't replace a decent, portable file format like GIF, but it's a good start for my purposes with small games and a fatbit graphics editor.

---

### Print to USB Port

Debbie writes:

    I was hoping I could find someone on line to help me with an old GW Basic program I have. I need it to print to a usb port. A few years ago with the help of a very kind man on line He helped me make the program print from a dot matrix to a laser. But all the new computers have only usb ports for printers. I do have one parrellell port on one computer but I cannot get it to work probably because it going thru windows. any advice would be very much appreciated

Neil comments:

    I'm not sure, but printing isn't a direct function of GW-BASIC, rather it's handled by the underlying operating system. If you haven't looked into DOSbox, an emulator that will run on Windows, then I would start there and maybe ask on their forums. What you want is to map the old DOS printer port somehow and GW-BASIC itself won't "know" the difference.

Ron comments

    Printfil will do what you want.

    Easier yet is to just send your text to a file using BASIC, then open that file using NOTEPAD and print it out in WINDOWS.

Anthony comments

    I have tried dos2usb and good for me

Hank comments

    Under the printer properties, if you select the ports and enable printer pooling, you should be able to print from the dos window without any special driver to the default printer. You may need to check the LPT1 port for the dos window to print to it and the pooling will redirect it to the other selected port.

Mike comments

    Dos2Prn and Dos2Usb. The 1st works best 4 me in all cases. http://www.dosprn.com/

Edward Bronson comments

    Go to windows printer setup. Choose the share all printers option. (or it's equivalent) Then all printers become available. windows will automatically associate the first available printer with LPT1: at the time of printing. All printers become global.
