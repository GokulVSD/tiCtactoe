                              ﻿   Tic Tac Toe
                                      -by Gokul Vasudeva


This was the first Graphical User Interface based game that I created.
It was for a college presentation, during my 1st year, Undergraduate at PESIT.
Started: March 24th, 2017
Finished: April 9th, 2017  (Had a lot of assignment work and my internal tests were going on)


This was my first foray into GTK and creating an application in C.
I learnt GTK from the ground up, and I’d received rudimentary knowledge in C from my 1st Semester.
Spent a lot of time deciding what Library to use.
After choosing GTK, tried coding all the widgets by hand; realised it's
too time consuming, so switched to Glade, a GTK UI widget handler, produces XML files.
Took a while to figure out how to use the XML file to create the
main widget.
Took a while to figure out how to link call back signals to functions
Button linking wasn't working because I kept linking the “Activate” signal, instead of the
“Clicked” signal. (This was due to lack of proper documentation for Glade).
Learned to debug by sending messages to terminal via g_print().
Fixed aspect ratio of certain widgets.
Took a while in getting the close/credit/licence buttons in the About dialog to work.
This was because they were created as a container widget, so sending individual
callback signals was not possible. Because of this, I had to read a lot of
documentation based on dialogs and response signals, and realised that
running the dialog instead of showing it was far more ergenomic;
the dialog automatically responds to the response signal which was predefined in the close button,
so that problem was solved. Took a very long time to figure that one.


Next I set up the difficulty selection menu, I tried very hard to terminate the
widget after selecting the difficulty, but the widget wouldn't terminate.
Same thing with buttons, I needed to change their text to either ‘X’ or ‘O’ or ‘ ‘
And it simply wasn't working, because when I tried initializing all the widgets
in order for me to perform actions on them, they created new widgets instead of
linking to the ones in the Glade XML file. I spent several days in overcoming
this hurdle, spent several hours going through Google to try to find some
documentation for the functions I was using, but GTK is primarily used with
Python, so almost all the documentation was only referencing Python, which is
object oriented, so that was useless.


After exhausting every avenue, I gave up and proceeded to try and generate
a new main window every time I triggered some event. This would be literally the
most inefficient way to do things, but it was the only option left.
But somewhere in between, I realised that I can directly pass user_data through
glade and modify the template itself from the XML file.
So I scrapped almost all the code I had done and restarted with this in mind.
But even after all of this, I still was not able to perform the actions.
After pondering for awhile, I came to the conclusion that the problem was
related to the parameters I was setting for my callback functions, so I googled
it and found the correct parameters. It still wouldn't work, and that's when I
realised that I had to type cast all the passed user_data as dynamic pointers
called g_pointers. After doing this, everything started to work.


But I was still not able to edit the labels of buttons, because Glade had a bug
where in it wouldn't let me select the button itself to be passed as user_data,
so I had to manually go into the XML file and link all correct user_data to the
respective buttons. I figured out how to fix this problem relatively quickly.


Next is the restart functionality of the game, it took a while for me to figure
out that GTK libraries had predefined the initialising of GTK and the main method
to require argc and argv. Then I reinitialized all the variables to zero, terminated
gtk_main and called main(0,NULL) to restart. This worked, except that for some
unknown reason, gtk_main_quit() simply would not quit if I tried to put anything after that
statement in the function. So I could close the game, but couldn't restart it,
or I could make a new game and overlay it over the last game, without closing the previous one.
Both cases were not ideal.
This was bad because if you simply dragged the window to the side, it would show
the last game window, once again this is very inefficient, and would cause
interference in the current game’s logic. After awhile, I figured out that I'd need
to pass the entire main window as a user_data, then typecast to a dynamic pointer,
then I could terminate just the main window widget, then start the new main.


Was not able to dynamically edit status bar’s label as I could only pass one user data at a time,
so I created a “Click to start” button, which then passed the user data of the button onto a static variable,
this allowed me to dynamically change the label in any function.


Encountered quite a few stupid implicit declaration/prototyping errors because C is an old dumb language.


Realised that I couldn’t send multiple user data in one button click because Glade doesn’t support it,
so I set up an Initialise procedure when PvC is selected,
where in every button needs to be pressed to send its respective user data in order to be stored in static variables.
This was a very tedious process because I had to modify a lot of code.


Created a Computer AI based on a scoring system. If difficulty is hard,
the highest scored move is played, if medium, second highest scored move is played, if easy,
third highest scored move is played. The scoring system worked off of several criteria,
and scores were adjusted for certain edge cases.
Implementing the PvC mode within the already created code took a lot of time and effort,
and required me to fix a lot of bugs that arose with calling the computerMove() function after Player’s move.


Command for compiling using GCC (GTK+ 3.0 Libraries must be installed first):

gcc -o TicTacToe main.c -Wall `pkg-config --cflags --libs gtk+-3.0` -export-dynamic
