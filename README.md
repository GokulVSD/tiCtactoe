                              ﻿   Tic Tac Toe
                                      -by Gokul Vasudeva


Written during my undergraduate course at PESIT, Bangalore South Campus.
The game was written for a presentation during my first year.

Started: March 24th, 2017

Finished: April 9th, 2017  (Took a a break for internal exams/assignments)


This was my first foray into GTK and creating an application in C.
I learnt GTK from the ground up, and I’d received rudimentary knowledge in C from my 1st Semester.
Due to the lack of documentation for the GTK library (in C, the Python library has pretty good documentation),
Finishing the game took way longer than I anticipated. Most of my time was spent trying to cross compile
the game on windows. For future reference, I would not recommend creating a user interface in C, let alone GTK.
There are better ways to go about it. I encountered uncountable problems that required me to rewrite the vast
majority of code due to mismatchs in library versions. I don't even think they update the libraries for GTK on
windows anymore. For anyone looking to fork the code over, there's an issue with PvC (initialising of buttons)
as well as the restart functionality. It was working, but it broke after I redesigned the user interface.
Fixing it shouldn't be too much effort, I could do it myself, but realistically, no one's going to fork this,
unless they're desperate for a small game created in C with a GUI, for their college projects. In which case,
at least put in the effort to fix the small bugs before directly forking it, you'll at least get an idea
of how the code was implimented.

Screenshots:


<a href="http://imgur.com/XgSHkeN"><img src="http://i.imgur.com/XgSHkeN.png" title="source: imgur.com" /></a>

<a href="http://imgur.com/b1S2RAl"><img src="http://i.imgur.com/b1S2RAl.png" title="source: imgur.com" /></a>

<a href="http://imgur.com/XgSHkeN"><img src="http://i.imgur.com/XgSHkeN.png" title="source: imgur.com" /></a>

<a href="http://imgur.com/ig5jP4p"><img src="http://i.imgur.com/ig5jP4p.png" title="source: imgur.com" /></a>

<a href="http://imgur.com/kAvbwH6"><img src="http://i.imgur.com/kAvbwH6.png" title="source: imgur.com" /></a>

<a href="http://imgur.com/ukTvyRy"><img src="http://i.imgur.com/ukTvyRy.png" title="source: imgur.com" /></a>

<a href="http://imgur.com/iYwzEYi"><img src="http://i.imgur.com/iYwzEYi.png" title="source: imgur.com" /></a>




Command for compiling using GCC (GTK+ 3.0 Libraries must be installed first):

gcc -o TicTacToe main.c -Wall `pkg-config --cflags --libs gtk+-3.0` -export-dynamic

Command on windows with MSYS (Keep all required DLL's in the folder with the executable):

gcc main.c -o TicTacToe.exe `pkg-config --cflags --libs gtk+-3.0` -Wl,--export-all-symbols -mwindows

Warning! You need to quit the game only using the quit button on windows, if not, a ghost process
is left behind. (This is because of the version mismatch of GTK on Windows and Linux)

