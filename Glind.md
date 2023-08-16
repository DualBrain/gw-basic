## Glind's Diversions

---

[Download](Download.md) | [Games](Games.md) | [Tutorials](Tutorials.md) | [KindlyRat](KindlyRat.md) | [Mouse Support](MouseSupport.md) | [Links](Links.md) | [Is BASIC best?](IsBasicBest.md)

---

### Netspace Archive

This is a single-page reprinting of Glind's Diversions website hosted on Netspace at http://glind.customer.netspace.net.au/gw-basic.html. This site has since gone offline. This is an effort to preserve the GW-BASIC portion of that website for the future.

#### GW-Basic programs

GW-Basic is one of the earliest computer programming languages. It has fallen into disuse, having been superseded by more sophisticated user-programs. Modern programs are great to use but how they actually do what they do is unknown to their users simply because the program code is hidden. GW-Basic is different, in that the code is listed, in sequence, and so one can see the steps a program takes when it runs. When one has learnt to program in GW-Basic, programs can be written to do whatever one wants to do.

Programs written by novice programmers often reveal things that ought to have been included but were not thought of at the time. Novice programmers adjust or correct these oversights by adding in bits of code, sometimes in such an haphazard manner that it is called "spaghetti" programming, often misusing the infamous "goto" instruction.

With experience, a programmer becomes more circumspect and writes *structured* programs, where blocks of code, or modules, are set out in logical sequence. Structured, logical thinking is a useful thing to have, regardless of what one does in life, and GW-Basic, despite being old-fashioned, is a means to learn it, whilst creating one's own programs. So we see that there is a good reason for having the program code open to view rather than out of sight as happens with modern programming languages that use compiled code.

##### Morse Code

Highlight the following code and save it as a text file called `MORSE.BAS`.

```vb
10 REM Morse code - MORSE.BAS
20 CLEAR :CLS :KEY OFF
30 PRINT "Type a message and see it appear as Morse Code." :PRINT
40 DIM CODE$(122)
50 RESTORE
60 FOR A = 32 TO 122
70   READ CODE$(A)
80   PRINT CHR$(A);"  ";
90 NEXT A
100 PRINT :PRINT
110 INPUT "Use any of the above - What is your message "; MESSAGE$
120 PRINT
130 L = LEN(MESSAGE$)
140 FOR B = 1 TO L
150   PRINT CODE$(ASC(MID$(MESSAGE$,B,1)));" ";
160 NEXT B
170 PRINT :PRINT
180 END
190 DATA " ","!","|","#","$","%","&","'","(",")",".","+",",","-","   ","/"
200 DATA -----,.----,..---,...--,....-,.....,-....,--...,---..,----.
210 DATA ":",";","<","=",">","?","@"
220 DATA .-, -..., -.-., -.., ., ..-., --., ...., .., .---, -.-, .-.., --
230 DATA -., ---, .--., --.-, .-., ..., -, ..-, ...-, .--, -..-, -.--, --..
240 DATA "[","\","]","^","_","'"
250 DATA ._, -..., -.-., -.., ., ..-., --., ...., .., .---, -.-, .-.., --
260 DATA -., ---, .--., --.-, .-., ..., -, ..-, ...-, .--, -..-, -.--, --..
```

##### Is your name prime?

Highlight the following code and save it as a text file called `PRIME-ID.BAS`.

```vb
10 REM Save as PRIME-ID.BAS
20 CLEAR :CLS :KEY OFF
30 PRINT "The book 'THE CURIOUS INCIDENT OF THE DOG IN THE NIGHT-TIME'"
40 PRINT "tells how Jesus Christ, Sherlock Holmes and Doctor Watson"
50 PRINT "are prime numbers if their letters are replaced by numbers." :PRINT
60 PRINT "If you enter your name (upper or lower case, or mixed)"
70 PRINT "the program will tell you if it is a prime number." :PRINT
80 INPUT "What is your name" ;NM$
90 TOTAL=0
100 FOR K=1 TO LEN(NM$)
110   CHR=ASC(MID$(NM$,K,1))
120   IF CHR=32 THEN 160
130   IF CHR > 90 THEN LET X=96 ELSE X=64
140   N=CHR-X
150   TOTAL=TOTAL+N
160 NEXT K
170 PRINT :PRINT TOTAL
180 ROOT=INT(SQR(TOTAL))
190 FOR J=2 TO ROOT
200   FACTOR=TOTAL/J
210   IF FACTOR=INT(FACTOR) THEN PRINT "Your name is not prime." :GOTO 240
220 NEXT J
230 PRINT "Your name is a prime number!"
240 KEY ON
250 END
```

##### Acey Deucey

Highlight the following code and save it as a text file called `ACEY.BAS`.

```vb
10 ' ----------------------------------------------
20 '                 ACEY DUECEY
30 ' ----------------------------------------------
40 '
50 '       Program by G C Lindridge  27/12/90
60 '
70 CLEAR : KEY OFF : CLS : SCREEN 0 : WIDTH 80
80 DEFINT A-Z
90 GOSUB 220                                       'INPUT SCREEN
100 GOSUB 510                                      'CREATE PACK
110 GOSUB 750                                      'SHUFFLE CARDS
120 SCREEN 1                                       'LARGE DISPLAY
130 TD = 1500                                      'TIME DELAY
140 GOSUB 930                                      'PLAY THE GAME
150 WIDTH 80 : SCREEN 0
160 PRINT "END ACEY DUECEY"
170 PRINT : PRINT "Do you want to play again?  Y/N" : PRINT
180 CH$ = INKEY$ : IF CH$ = "" THEN 180
190 IF CH$ = "Y" THEN 70 ELSE SYSTEM
200 END
210 ' ----------------------------------------------
220 '                                   INPUT SCREEN
230 ' ----------------------------------------------
240 PRINT TAB(33);"ACEY DUECEY"
250 PRINT TAB(33);"-----------"
260 PRINT : PRINT
270 PRINT TAB(24);"You and the computer play the game."
280 PRINT TAB(24);"You both start with 1000 units."
290 PRINT TAB(24);"Bets are from 1 to 200 units."
300 PRINT
310 PRINT TAB(24);"Can you send the computer broke?"
320 PRINT : PRINT
330 PRINT TAB(24);"[ 1 ]  To see the User Guide"
340 PRINT TAB(24);"[ 2 ]  Play Acey Duecey"
350 CH$ = INKEY$ : IF CH$ = "" THEN 350
360 IF CH$ = "1" THEN GOSUB 2150
370 MIN = 1
380 LIMIT = 200
390 HUMANBANK = 900
400 COMPBANK = 900
410 KITTY = 200
420 RETURN
430 ' ----------------------------------------------
440 '                                  PRESS ANY KEY
450 ' ----------------------------------------------
460 LOCATE 25,1 : PRINT ,,,"Press any key to continue";
470 WHILE INKEY$ = "" : WEND
480 CLS
490 RETURN
500 ' ----------------------------------------------
510 '                                    CREATE PACK
520 ' ----------------------------------------------
530 DIM CARD(52)
540 'GIVE GAME VALUES TO CARDS
550 FOR J = 0 TO 3
560   FOR K = 1 TO 13
570     CARD(J*13+K) = K+1
580   NEXT K
590 NEXT J
600 RETURN
610 ' ----------------------------------------------
620 '                                     SHOW CARDS
630 ' ----------------------------------------------
640 LOCATE 1,1
650 FOR K = 52 TO 1 STEP-1
660   IF CARD(K) < 11 THEN PRINT USING "####";CARD(K);
670   IF CARD(K) = 11 THEN PRINT "   J";
680   IF CARD(K) = 12 THEN PRINT "   Q";
690   IF CARD(K) = 13 THEN PRINT "   K";
700   IF CARD(K) = 14 THEN PRINT "   A";
710 NEXT K
720 PRINT : PRINT
730 RETURN                                          'END DISPLAY
740 ' ----------------------------------------------
750 LOCATE 24,1 :           PRINT "[SHUFFLE]       ";
760 ' ----------------------------------------------
770 RANDOMIZE TIMER
780 FOR K = 52 TO 2 STEP -1
790   X = INT(RND(1)*K)+1
800   SWAP CARD(K),CARD(X)
810 NEXT K
820 SHOE = 52                                       'PUT CARDS IN SHOE
830 RETURN
840 ' ----------------------------------------------
850 '                                     TIME DELAY
860 ' ----------------------------------------------
870 FOR K = 1 TO TD
880   FOR L = 1 TO TD
890   NEXT L
900 NEXT K
910 RETURN
920 ' ----------------------------------------------
930 '                                  PLAY THE GAME
940 ' ----------------------------------------------
950 WHILE (BET$ <> "Q") AND (HUMANBANK > MIN) AND (COMPBANK > MIN) 'CONTINUE
960   P = 0 : BET$ = ""                              'INITIALISE
970   PLHAND = 0
980   FOR K = 1 TO 3
990     PLCARD(K) = 0
1000   NEXT K
1010   BADCARDS = 0
1020   IF BET$ = "Q" THEN 1100                       'QUIT THE GAME
1030   IF (SHOE < 5) THEN GOSUB 750                  'RESHUFFLE POINT
1040   GOSUB 850                                     'TIME DELAY
1050   CLS
1060   GOSUB 1180                                    'HUMAN PLAYER
1070   IF (SHOE < 5) THEN GOSUB 750                  'RESHUFFLE POINT
1080   GOSUB 1540                                    'COMPUTER PLAYER
1090 WEND
1100 RETURN                                          'END DEALING
1110 ' ----------------------------------------------
1120 '                                    DEAL A CARD
1130 ' ----------------------------------------------
1140 CARD = CARD(SHOE)                               'THE TOP CARD
1150 SHOE = SHOE - 1                                 'REMOVE CARD FROM PACK
1160 RETURN                                          'DEAL CARD
1170 ' ----------------------------------------------
1180 '                                   HUMAN PLAYER
1190 ' ----------------------------------------------
1200 LOCATE 24, 1 : PRINT "HUMAN BANK";HUMANBANK;
1210 LOCATE 24,21 : PRINT "COMPUTER BANK";COMPBANK;
1220 GOSUB 1910
1230 HUMANBET = 0
1240 GOSUB 1120                                      'DEAL A CARD
1250 PLCARD(1) = CARD
1260 GOSUB 1120                                      'DEAL A CARD
1270 PLCARD(2) = CARD
1280 IF PLCARD(1) < PLCARD(2) THEN SWAP PLCARD(1),PLCARD(2)  'CARD(1) IS HIGH
1290 P = 1
1300 R = 80 : C = P*32 - 32 : GOSUB 2000             'SHOW CARD IN BOX
1310 P = 2
1320 R = 80 : C = P*32      : GOSUB 2000             'SHOW CARD IN BOX
1330 IF PLCARD(2)+1 >= PLCARD(1) THEN 1500           'NO SPACE BETWEEN CARDS
1340 LOCATE 25, 1 : INPUT;"MAKE A BET ",BET$
1350 IF BET$ = "Q" THEN 1520                         'QUIT THE GAME
1360 HUMANBET = INT(ABS(VAL(BET$)))                  'BET UNITS
1370 IF HUMANBET = 0 THEN 1500                       'REJECT HAND
1380 IF HUMANBET > KITTY THEN LET HUMANBET = KITTY   'LIMIT BET
1390 IF HUMANBET > LIMIT THEN LET HUMANBET = LIMIT   'MAXIMUM BET
1400 IF HUMANBET > HUMANBANK THEN LET HUMANBET = HUMANBANK   'BET THE LOT
1410 GOSUB 1120                                      'DEAL A CARD
1420 P = 3
1430 PLCARD(P) = CARD
1440 R = 16 : C = P*32 - 64 : GOSUB 2000             'SHOW CARD IN BOX
1450 HUMANBANK = HUMANBANK-HUMANBET
1460 KITTY = KITTY + HUMANBET
1470 IF (PLCARD(3)>= PLCARD(1)) OR (PLCARD(3) < =  PLCARD(2)) THEN 1500
1480 HUMANBANK = HUMANBANK+2*HUMANBET
1490 KITTY = KITTY - 2*HUMANBET
1500 FOR K = 1 TO 1000 : NEXT K
1510 GOSUB 1910                                      'KITTY
1520 RETURN
1530 ' ----------------------------------------------
1540 '                                COMPUTER PLAYER
1550 ' ----------------------------------------------
1560 LOCATE 24,21 : PRINT "COMPUTER BANK";COMPBANK;
1570 COMPBET = 0
1580 GOSUB 1120                                      'DEAL A CARD
1590 PLCARD(1) = CARD
1600 GOSUB 1120                                      'DEAL A CARD
1610 PLCARD(2) = CARD
1620 IF PLCARD(1) < PLCARD(2) THEN SWAP PLCARD(1),PLCARD(2)  'CARD(1) IS HIGH
1630 P = 1
1640 R = 80 : C = P*32 + 160 : GOSUB 2000            'SHOW CARD IN BOX
1650 P = 2
1660 R = 80 : C = P*32 + 192 : GOSUB 2000            'SHOW CARD IN BOX
1670 IF PLCARD(2)+1 >= PLCARD(1) THEN 1870           'NO SPACE BETWEEN CARDS
1680 FOR K = 1 TO SHOE
1690   IF CARD(K) >= PLCARD(1) OR CARD(K) <= PLCARD(2)THEN LET BADCARDS = BADCARDS+1
1700   IF BADCARDS >= SHOE/2 THEN LET K = SHOE
1710 NEXT K
1720 COMPBET = INT((SHOE-2*BADCARDS)/SHOE*COMPBANK)  'ADVANTAGE BET
1730 IF COMPBET < 1 THEN LET COMPBET = 0 : GOTO 1870
1740 IF COMPBET > KITTY THEN LET COMPBET = KITTY     'LIMIT BET
1750 IF COMPBET > LIMIT THEN LET COMPBET = LIMIT     'MAXIMUM BET
1760 IF COMPBET > COMPBANK THEN LET COMPBET = COMPBANK       'BET THE LOT
1770 LOCATE 25,21 : PRINT "COMPUTER  BET";COMPBET;
1780 GOSUB 1120                                      'DEAL A CARD
1790 P = 3
1800 PLCARD(P) = CARD
1810 R = 16 : C = P*32 + 128 : GOSUB 2000            'SHOW CARD IN BOX
1820 COMPBANK = COMPBANK-COMPBET
1830 KITTY = KITTY + COMPBET
1840 IF (PLCARD(3)>= PLCARD(1)) OR (PLCARD(3) < =  PLCARD(2)) THEN 1870
1850 COMPBANK = COMPBANK+ 2*COMPBET
1860 KITTY = KITTY - 2*COMPBET
1870 FOR K = 1 TO 2000 : NEXT K
1880 GOSUB 1910                                      'KITTY
1890 RETURN
1900 ' ----------------------------------------------
1910 '                                          KITTY
1920 ' ----------------------------------------------
1930 IF KITTY <> 0 THEN 1970
1940 HUMANBANK = HUMANBANK-100
1950 COMPBANK = COMPBANK-100
1960 KITTY = 200
1970 LOCATE 25,21 : PRINT "        KITTY";KITTY;
1980 RETURN
1990 ' ----------------------------------------------
2000 '                         PICTURE PLAYERS' CARDS
2010 ' ----------------------------------------------
2020 PICTURE = PLCARD(P)
2030 LINE (C+4,R+4)-(C+30,R+44),,B                   'DRAW CARD BORDER
2040 IF PICTURE = 10 THEN LET PIP$ = "1O"
2050 IF PICTURE = 11 THEN LET PIP$ = "J "
2060 IF PICTURE = 12 THEN LET PIP$ = "Q "
2070 IF PICTURE = 13 THEN LET PIP$ = "K "
2080 IF PICTURE = 14 THEN LET PIP$ = "A "
2090 IF PICTURE < 10 THEN LET PIP$ = RIGHT$(STR$(PICTURE),1)+" "
2100 LOCATE R/8+2,C/8+2 : PRINT PIP$;                'DRAW PIPS
2110 SUIT$ = CHR$(INT (RND(1)*4)+3)                  'CARD SUIT
2120 LOCATE R/8+4,C/8+3 : PRINT SUIT$;               'DRAW SUIT
2130 RETURN
2140 ' ----------------------------------------------
2150 CLS :              PRINT ,,"      ACEY  DUECEY" : PRINT
2160 ' ----------------------------------------------
2170 PRINT ,"This is a gambling card game. A player is dealt a"
2180 PRINT ,"two card hand face up. The player now has the choice"
2190 PRINT ,"of folding the hand or betting on the hand."
2200 PRINT ,"If he folds, the next player is dealt a hand."
2210 PRINT ,"If he bets, he is dealt a third card."
2220 PRINT ,"If this card is between the other two cards he wins."
2230 PRINT ,"If this card is equal to either card or is more than"
2240 PRINT ,"the big card or less than the small card he loses."
2250 PRINT ,"Cards are as normal with Ace a high card. No suits."
2260 PRINT
2270 PRINT ,"TO FOLD: Bet 0. Alternatively press [Return] key."
2280 PRINT ,"TO QUIT: Enter Q as a bet."
2290 PRINT
2300 PRINT ,"BETTING: All bets are in units of 1."
2310 PRINT ,"Each player contributes 100 units to a kitty."
2320 PRINT ,"Bet Limits:  Minimum 1 unit.  Maximum 200 units."
2330 PRINT ,"A bet is unable to exceed what remains in the kitty."
2340 PRINT ,"A player bets to win 'EVENS'. Winnings are taken"
2350 PRINT ,"from the kitty, losing bets are added to the kitty."
2360 PRINT
2370 PRINT ,"When the kitty is empty, the players again contribute"
2380 PRINT ,"100 units each.";
2390 GOSUB 440                                       'PRESS ANY KEY
2400 PRINT ,"NOTE:"
2410 PRINT ,"When a hand is dealt and there is no gap between"
2420 PRINT ,"the player's two cards, a new hand, or hands,"
2430 PRINT ,"will be dealt until a gap exists."
2440 GOSUB 440                                       'PRESS ANY KEY
2450 RETURN
```

##### Goldbach Conjecture

Highlight the following code and save it as a text file called `GOLBACH.BAS`.

```vb
10 'Goldbach conjecture
20 CLS :KEY OFF :CLEAR
30 PRINT "GOLDBACH CONJECTURE" :PRINT
40 PRINT "Every even number greater than 2 can be written as the sum of two primes." :PRINT
50 'Count and list Goldbach Prime Pairs
60 INPUT "Enter a test number ";T
70 T=2*INT(T/2)                   'Ensure test number is even
80 N=0
90 FOR K=3 TO T-3 STEP 2
100   X=SQR(K)
110   Z=0
120   FOR J=3 TO X STEP 2
130     IF K/J-INT(K/J)=0 THEN LET Z=Z+1
140   NEXT J
150   IF Z=0 THEN GOSUB 180       'found a prime, check for 2nd prime
160 NEXT K
170 END
180 'SUBROUTINE to test if other component is also prime
190 L=T-K
200 P=SQR(L)
210 Y=0
220 FOR M=3 TO P STEP 2
230   IF L/M-INT(L/M)=0 THEN LET Y=Y+1
240 NEXT M
250 IF Y=0 AND L>K THEN LET N=N+1 :PRINT,,USING"######";N;K;L
260 RETURN
```

##### Primes Between Two Numbers

List of all primes between two selected numbers. Highlight the following code and save it as a text file called `PRIMEA-B.BAS`.

```vb
10 'List primes between two selected numbers
20 CLEAR :CLS :KEY OFF
30 PRINT "List primes between two selected numbers." :PRINT
40 INPUT "Input smaller number ";SMALL
50 INPUT "Input larger  number ";LARGE
60 IF LARGE < SMALL THEN SWAP LARGE,SMALL   'Swap if entered in wrong order
70 SMALL=INT(SMALL/2)*2+1                   'Ensure small number is odd
80 LARGE=INT(LARGE/2)*2-1                   'Ensure large number is odd
90 FOR K=SMALL TO LARGE STEP 2
100   X=SQR(K)                              'Only need to check to square root
110   F=0                                   'Count factors as a logic step
120   FOR J=3 TO X STEP 2
130     IF K/J-INT(K/J)=0 THEN LET F=F+1    'Totals up factors. F=0 is prime
140   NEXT J
150   IF F=0 THEN PRINT USING "########";K; 'Prime has no factors
160 NEXT K
170 END
```

##### "Betting on Hamlet"

Highlight the following code and save it as a text file called `HAMLET.BAS`.

```vb
10 'Hamlet - the fencing match
20 CLEAR :CLS :KEY OFF
30 PRINT,"Shakespeare's 'Hamlet' - the fencing match." :PRINT
40 PRINT "   Claudius bets that Laertes cannot exceed Hamlet by 3 hits in 12 passes."
50 PRINT "   Because Laertes is nominally a better fencer than Hamlet, Claudius has"
60 PRINT "   laid on odds of 12 for 9. Is this a good bet?" :PRINT
70 '
80 RANDOMIZE TIMER
90 PRINT "      H-wins     L-wins   H-profit%  L-profit%"
100 PASSES=12                     'the maximum number of plays in a game
110 HT=0 :LT=0
120 FOR TIMES = 1 TO 10
130    HH=0 :LL=0
140    FOR CYCLE = 1 TO 1000
150       H=0 :L=0 :N=0
160       FOR HIT = 1 TO PASSES
170          P = INT(24*RND+1)
180          IF P <= 9 THEN H=H+1 ELSE L=L+1
190          IF H=5 OR L=8 THEN LET HIT = PASSES
200       NEXT HIT
210       IF H=5 THEN HH=HH+1 :HT=HT+1
220       IF L=8 THEN LL=LL+1 :LT=LT+1
230    NEXT CYCLE
240    PRINT USING "###########";HH;LL
250 NEXT TIMES
260 PRINT :PRINT USING "###########";HT;LT
270 PRINT "        x12         x9"
280 PRINT USING "###########";HT*12;LT*9;
290 PERCENT=(HT*12-LT*9)/(HT*12+LT*9)*100
300 PRINT USING "########.##";PERCENT :PRINT
310 PRINT USING "########.##";PERCENT;
320 IF PERCENT > 0 THEN PRINT "% profit shows that Claudius has made a good bet." ELSE PRINT "% loss shows that Claudius has made a bad bet."
330 END
```

##### Play a well-known tune

Highlight the following code and save it as a text file called `PLAYTUNE.BAS`.

```vb
10 REM This is a well-known piece of music.
20 'Note that 0 is used and so is O (for Octave).
30 'Note that either suffix # or + can indicate a sharp.
40 '
50 CLEAR
60 PARTTUNE$= "DF#A L2 O4 D L4 O5 DD P4"
70 PLAY "T180 DF#A L2 A L4 O4 AA P4 F#F# P4 O3 D"
80 PLAY "DF#A L2 A L4 O4 AA P4 GG P4 O3 C#"
90 PLAY "C#EB L2 B L4 O4 BB P4 GG P4 O3 C#"
100 PLAY "C#EB L2 B L4 O4 BB P4 F+F+ P4 O3 D"
110 PLAY PARTTUNE$
120 PLAY "O4 AA P4 O3 D"
130 PLAY PARTTUNE$
140 PLAY "O4 BB P4 EEG L8 B P8 ML B1 L4 MN G#A ML L3 O5 F#1"
150 PLAY "L4 MN D O4 F# ML L2 F# MN L4 E ML L2 B MN L4 A"
160 PLAY "D P8 D8 D4"
170 END
```

##### Armstrong Numbers

Highlight the following code and save it as a text file called `ARMSTRNG.BAS`.

```vb
10 ' PROGRAM Armstrong Numbers
20 CLEAR :KEY OFF :CLS
30 PRINT "ARMSTRONG NUMBERS" :PRINT
40 PRINT "Program computes all Armstrong numbers in the range of 0 - 999."
50 PRINT "An Armstrong number is a number such that the sum of its digits"
60 PRINT "raised to the third power is equal to the number itself." :PRINT
70 '
80 '   A, B, C                             the three digits
90 '   ABC, A3B3C3                         the number and its cubic sum
100 '   COUNT                              a counter
110 '
120 A=0: B=0: C=0: COUNT=0                 'initialise
130 FOR A = 0 TO 9                         'for the left most digit
140   FOR B = 0 TO 9                       'for the middle digit
150     FOR C = 0 TO 9                     'for the right most digit
160       ABC = A*100 + B*10 + C           'the number
170       A3B3C3 = A^3 + B^3 + C^3         'the sum of cubes
180       IF ABC = A3B3C3 THEN GOSUB 230   'if they are equal
190     NEXT C
200   NEXT B
210 NEXT A
220 END
230 ' Display results subroutine
240 COUNT = COUNT + 1                      'count the Armstrongs
250 PRINT "Armstrong number"; COUNT;": "; USING "####"; ABC
260 RETURN
```

##### Wind Chill Temperature Table

Highlight the following code and save it as a text file called `CHILL.BAS`.

```vb
10 REM Wind chill temperature table
20 CLEAR :CLS :KEY OFF
30 PRINT SPC(27);"WIND  CHILL  TEMPERATURE" : PRINT
40 PRINT SPC(27);"Temperature (Fahrenheit)"
50 PRINT "         ";
60 FOR T = 30 TO -30 STEP -5
70   PRINT USING "#####";T;
80 NEXT T
90 PRINT : PRINT "Wind speed"
100 PRINT "miles/hour"
110 FOR V = 5 TO 80 STEP 5
120   PRINT USING "########";V;
130   PRINT " ";
140   FOR T = 30 TO -30 STEP -5
150     A = 35.74 + .6215*T - 35.75*V^.16 + .4275*T*V^.16
160     PRINT USING "#####";A;
170   NEXT T
180 PRINT
190 NEXT V
200 END
```

##### Sample Animation

Highlight the following code and save it as a text file called `ANIMATE.BAS`.

```vb
10 --------------------------------------------
20 '          ANIMATION (using XOR)
30 --------------------------------------------
40 CLEAR :CLS :KEY OFF
50 '
60 DIM IMAGE%(150)
70 SCREEN 1
80 CLS
90 '
100 CIRCLE (20, 20), 6
110 PAINT (20, 20)
120 DRAW "D16 NE8 NH8 D4 NF8 NG8"
130 GET (8, 8) - (31, 55), IMAGE%
140 CLS
150 '
160 'Draw background of 4 coloured boxes
170 LINE (100, 60) - STEP(20, 20), 1, BF
180 LINE (150, 60) - STEP(20, 20), 3, BF
190 LINE (100, 90) - STEP(20, 20), 3, B
200 LINE (150, 90) - STEP(20, 20), 2, BF
210 '
220 FOR X% = 20 TO 200 STEP 2
230    PUT (X%, 60), IMAGE%, XOR     'Draw a stick figure
240       NOW! = TIMER
250       WHILE (TIMER - NOW!) < .15 'Pause for .15 seconds
260       WEND
270    PUT (X%, 60), IMAGE%, XOR     'Erase stick figure
280 NEXT X%
290 SCREEN 2 :SCREEN 0
300 END
```

##### Reassign Function Keys

Highlight the following code and save it as a text file called `KEY.BAS`.

```vb
10 ' Program assigns alternative values to rarely-used Function Keys
20 ' If a batch file is used to load GW-BASIC, add key to the file text.
30 ' This program will then run automatically to do its job.
40 CLS :KEY ON
50 KEY 5,"SYSTEM"               'leave gwbasic, checks first if ok
60 KEY 6,"RENUM 10"+CHR$(13)    'instant renumbering from line 10
70 KEY 7,"EDIT "                'add a line number, Enter, and edit it
80 KEY 8,"FILES"+CHR$(13)       'a list of files at any time
90 KEY 9,"LIST -200"+CHR$(13)   'lists code down to line 200
100 KEY 10,"KEY LIST"+CHR$(13)  'shows the values assigned to keys
110 FILES                       'conveniently lists files at the start
120 NEW                         'ready for action!
```

##### Quarter Squares Table

Highlight the following code and save it as a text file called `QTR_SQRS.BAS`.

```vb
10 REM Table of Quarter Squares
20 CLEAR :CLS :KEY OFF
30 PRINT,,"QUARTER SQUARES" :PRINT
40 PRINT "Before the discovery of logarithms, tables of quartersquares were used"
50 PRINT "for multiplication. The quartersquare of an integer is the integer part"
60 PRINT "of one quarter of its square." :PRINT
70 PRINT "To multiply the two numbers x and y it is simply necessary to calculate"
80 PRINT,"xy = quartersquare(x+y) - quartersquare(x-y)" :PRINT
90 PRINT "Press any key for a sample table of quartersquares of integers up to 199."
100 GOSUB 260                         'PRESS ANY KEY
110 PRINT TAB(13);
120 FOR UNIT = 0 TO 9
130    PRINT USING "######";UNIT;
140 NEXT UNIT
150 PRINT :PRINT
160 FOR TENS = 0 TO 190 STEP 10
170    PRINT TAB(8); USING "####";TENS;
180    PRINT " ";
190    FOR NUMBER = TENS TO TENS+9
200       PRINT USING "######"; INT(NUMBER^2/4);
210    NEXT NUMBER
220    PRINT
230 NEXT TENS
240 END
250 ' ----------------------------------------------
260 '                                  PRESS ANY KEY
270 ' ----------------------------------------------
280 LOCATE 25,1 :PRINT ,,,"Press any key to continue";
290 WHILE INKEY$ = "" :WEND
300 CLS
310 RETURN
```

##### Decimal to Base Converter

Highlight the following code and save it as a text file called `DECIBASE.BAS`.

```vb
10 REM Decimal to Base converter
20 CLEAR :CLS :KEY OFF
30 DIM DIGIT(15)
40 PRINT,"Convert a Decimal number to any base 2 through 16" :PRINT
50 INPUT "Enter a Decimal number less than 32768 ";DECIMAL
60 IF DECIMAL < 1 OR DECIMAL > 32768! THEN 50
70 PRINT
80 INPUT "Enter Base 2 through 16 ";BASE
90 IF BASE < 2 OR BASE > 16 THEN 80
100 LET TEMP = DECIMAL
110 N = 0                   'count digits in answer
120 WHILE TEMP > 0
130   N = N+1
140   DIGIT(N) = TEMP MOD BASE
150   TEMP = INT(TEMP/BASE)
160 WEND
170 ' Show converted number
180 PRINT :PRINT,DECIMAL; "= ";
190 FOR K = N TO 1 STEP -1
200   IF BASE <= 10 THEN PRINT RIGHT$(STR$(DIGIT(K)),1);
210   IF BASE > 10 THEN IF DIGIT(K) <= 9 THEN PRINT RIGHT$(STR$(DIGIT(K)),1); ELSE GOSUB 260
220 NEXT K
230 PRINT " to base";BASE
240 END
250 '
260 'Base 11 through 16 subroutine
270 IF DIGIT(K) = 10 THEN PRINT "A";
280 IF DIGIT(K) = 11 THEN PRINT "B";
290 IF DIGIT(K) = 12 THEN PRINT "C";
300 IF DIGIT(K) = 13 THEN PRINT "D";
310 IF DIGIT(K) = 14 THEN PRINT "E";
320 IF DIGIT(K) = 15 THEN PRINT "F";
330 RETURN
```

##### Redhead - A Match Game

Highlight the following code and save it as a text file called `REDHEAD.BAS`.

```vb
10 REM "Redhead" - a match game
20 ' List of variables
30 '         BOX     = Total number of matches in the box at any time
40 '         PLAYER  = The player whose turn it is to pick up matches
50 '         MATCHES = The number of matches picked up each turn
60 '         NUM     = Each match in the display stack
70 '         AGAIN$  = another game
80 '         K       = Timer loop counter
90 '
100 ' --------------------------------------
110 '                  Description and rules
120 ' --------------------------------------
130 CLEAR :CLS :KEY OFF
140 LOCATE  5,18
150 COLOR 14,  1 :PRINT "** The Game of ";
160 COLOR  4, 15 :PRINT "REDHEAD";
170 COLOR 14,  1 :PRINT " **"
180 LOCATE  8, 9
190 PRINT "Redhead is a match game between two players." :PRINT
200 PRINT TAB(9) "The two players are you and the computer." :PRINT
210 PRINT TAB(9) "A number of matches are in a box and the players"
220 PRINT TAB(9) "take turns to remove 1, 2 or 3 matches from the box."
230 PRINT TAB(9) "The player who has to pick up the last match is the loser."
240 ' --------------------------------------
250 '                 Getting ready - inputs
260 ' --------------------------------------
270 LOCATE 20, 9
280 PRINT "Press any key to start the game.";
290 Z$=INKEY$ :IF Z$="" THEN 290
300 CLEAR :CLS
310 LOCATE 10, 24
320 INPUT "How many matches are in the box ";BOX
330 IF BOX < 2 THEN PRINT :PRINT TAB(24); "Too few! Try again." :PRINT TAB(24);"";:GOTO 320
340 IF BOX > 23 THEN PRINT :PRINT TAB(24); "Maximum number for game is 23." :PRINT TAB(24);"";:GOTO 320
350 PRINT :PRINT TAB(24); "";
360 INPUT "Who goes first, you = 1 or the computer = 2 ";PLAYER
370 ' --------------------------------------
380 '                           Main program
390 ' --------------------------------------
400 CLS
410 GOSUB 900                               'to match-drawing subroutine
420 ON PLAYER GOSUB 610, 740                'to player subroutines
430 GOSUB 1040                              'time delay
440 CLS
450 BOX = BOX-MATCHES                       'current match total
460 GOSUB 900                               'to match-drawing subroutine
470 IF BOX > 1 THEN 420                     'next player
480 ' --------------------------------------
490 '                        Display results
500 ' --------------------------------------
510 GOSUB 1040                              'time delay
520 LOCATE  6,25
530 IF PLAYER = 1 THEN PRINT "The computer wins" ELSE PRINT "You win the game."
540 IF BOX = 0 THEN LOCATE 9,25 :PRINT "You took the lot! You are a silly mug."
550 GOSUB 1040                              'time delay
560 LOCATE 12,25
570 INPUT "Another game? YES OR NO ";AGAIN$
580 A$ = LEFT$(AGAIN$,1)
590 IF A$ = "Y" OR  A$ = "y" THEN 300 ELSE PRINT :PRINT "Game over" :END
600 ' --------------------------------------
610 '                Human player subroutine
620 ' --------------------------------------
630 PRINT TAB(25);"";:INPUT "How many matches do you want (1, 2 or 3) ";MATCHES
640 IF MATCHES > 3 OR MATCHES < 1 THEN 630 'check player's move
650 PRINT
660 PLAYER = 2                              'prepare for other player
670 IF MATCHES >= BOX THEN MATCHES = BOX :PLAYER = 1 'stay with present player
680 LOCATE  8,25
690 PRINT "You picked";MATCHES; "match";
700 IF MATCHES > 1 THEN PRINT "es"
710 PRINT
720 RETURN
730 ' --------------------------------------
740 '             Computer player subroutine
750 ' --------------------------------------
760 LOCATE  5,25
770 PRINT "It's the Computer's turn"
780 GOSUB 1040                              'time delay (simulate thinking)
790 MATCHES = ((BOX-1)/4 - INT((BOX-1)/4))*4             'computer strategy
800 IF MATCHES = 0 THEN LET MATCHES = INT(1 + 3*RND(1))  'best alternative
810 PLAYER = 1                              'prepare for other player
820 LOCATE  8,25
830 PRINT "The computer picked";MATCHES; "match";
840 IF MATCHES > 1 THEN PRINT "es"
850 PRINT
860 RETURN
870 ' --------------------------------------
880 '               Match-drawing subroutine
890 ' --------------------------------------
900 FOR NUM = 1 TO BOX
910   LOCATE 24-NUM,10                      'location of matches
920   COLOR  4,15
930   PRINT " *";                           'match head
940   COLOR  0,15
950   PRINT "======= "                      'match stick
960   COLOR 14, 1
970 NEXT NUM
980 LOCATE 23-B0X/2,25                      'location of text
990 PRINT "The box now contains";BOX;"match";
1000 IF BOX > 1 THEN PRINT "es"
1010 PRINT
1020 RETURN
1030 ' --------------------------------------
1040 '                  Time delay subroutine
1050 ' --------------------------------------
1060 FOR J = 1 TO 2000
1070   FOR K = 1 TO 2000
1080   NEXT K
1090 NEXT J
1100 RETURN
```

##### Reverse a Phrase

Highlight the following code and save it as a text file called `REVERSE.BAS`.

```vb
10 REM Reverse the letters of a phrase
20 CLEAR :KEY OFF :CLS
30 INPUT "What is your phrase";PHRASE$
40 PRINT :PRINT "The phrase reversed: ";
50 FOR LETTER = 1 TO LEN(PHRASE$)
60   PRINT LEFT$(RIGHT$(PHRASE$,LETTER),1);
70 NEXT LETTER
80 END
```

##### Crossword Clue Solver

Highlight the following code and save it as a text file called `ANSWERS.BAS`.

```vb
10 REM Crossword clue solver
20 CLEAR : CLS :KEY OFF
30 PRINT TAB(28);"AUTOMATIC CROSSWORD CLUE SOLVER" :PRINT
40 PRINT,"Find potential crossword answers from the known letters." :PRINT
50 PRINT,"A text file named WORDLIST.TXT containing a list of words"
60 PRINT,"needs to exist. No limit to how many words it can contain." :PRINT
70 PRINT,"ANSWERS.BAS searches WORDLIST.TXT for all words that fit"
80 PRINT,"the known letters." :PRINT
90 DIM LETTER$(15)
100 INPUT "Type the letters you know, - for unknown, then press Enter ";WORD$
110 LENGTH = LEN(WORD$)
120 IF LENGTH < 2 THEN PRINT :PRINT "2 letters minimum. Try again.": PRINT :GOTO 100
130 IF LENGTH > 15 THEN PRINT :PRINT "15 letters maximum. Try again.": PRINT :GOTO 100
140 FOR K = 1 TO LENGTH
150   LETTER$(K) = MID$(WORD$,K,1)
160   IF ASC(LETTER$(K)) >64 THEN LET LETTER$(K) = CHR$(ASC(LETTER$(K))+32)
170   IF ASC(LETTER$(K)) >122 THEN LET LETTER$(K) = CHR$(ASC(LETTER$(K))-32)
180 NEXT K
190 PRINT
200 OPEN "WORDLIST.TXT" FOR INPUT AS #1
210 WHILE NOT EOF(1)
220   INPUT #1, THISWORD$
230   IF LEN(THISWORD$) <> LENGTH THEN 300
240   FOR X = 1 TO LENGTH
250     IF LETTER$(X)= "-" THEN 270
260     IF LETTER$(X) <> MID$(THISWORD$,X,1) THEN THISWORD$ = ""
270   NEXT X
280   IF THISWORD$ > "" THEN PRINT THISWORD$,
290   THISWORD$ = "" 
300 WEND
310 CLOSE #1
320 KEY ON
330 END
```

##### First 40 Fibonacci Numbers

Highlight the following code and save it as a text file called `FIBON.BAS`.

```vb
10 REM First 40 Fibonacci Numbers 
20 CLEAR :CLS
30 TEMP = 0
40 FIB = 1
50 FOR NUMBER = 1 TO 40
60    PRINT USING "##########";FIB;
70    PAIR = TEMP + FIB
80    TEMP = FIB
90    FIB = PAIR
100 NEXT NUMBER
110 END
```
