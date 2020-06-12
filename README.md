# Modern port of Softporn Adventure (1981) by Charles Benton

I met "Chuck" Benton when I was a kid, maybe 10 years old, and he was showing me this, his new creation, on his Apple II. He had just begun selling it. I remember being amazed at how intelligent the AI seemed, not to mention it was funny! It had adult themes that were very different from the other generic space games and arcade ports I was used to seeing on my Apple II. 

I still remember this 39 years later, but at one point, I innocently typed "TKAE" instead of "TAKE" and it scolded me by saying: "Learn to spell, idiot!!!". I was mesmerized that it even knew about my spelling errors to give it a chance to insult me. I was in awe.

I'm thrilled to have access to the source and delighted it's in a high-level language. It's actually quite readable even to this day. At the time, I had assumed it was written in AppleSoft BASIC, but it was too fast and too complex for that. 

I don't believe that this Pascal source code was the original that was compiled on the Apple II because there is a comment at the start of the first source file that says, "24 for CP/M, 25 for IBM PC", referring to the terminal console line height. This source must be a bit later in the history of this game, after it was ported a bit. I would like to try to compile this under USCD Pascal for the Apple II.

Surprisingly little was needed to adapt this to a modern Pascal compiler. I chose Free Pascal because it is no cost, multi-platform, and it is easy to use.

## The Conversion

It took just an evening to get it to compile under Free Pascal and work. 

* Changing the source names to end in .pas so that modern editors will automatically do proper syntax highlighting
* Added an explicit "uses Crt;" to reference this standard unit
* Change variables named "object" to "obj" as "object" is now a reserved keyword in modern Pascal
* There were some unused variables that the compiler was complaining about, so they were removed 
* Fixed an original bug: the direction_name_string array was too small and has been resulting in an overflow situation
* Replaced read( kbd, ch ) with ReadKey(), as the former doesn't map to modern Pascal
* Instead of hard-coding the height of the terminal, it now adapts to your terminal height
* Added a `$define cheat` to give you $10,000 at the start and a `$define omit_extra_newlines` to not stick a blank newline everywhere
* And that's really it!

## Compiling

### Ubuntu / Debian

```
$ sudo apt install fp-compiler  # install the Free Pascal compiler ("fpc")

$ fpc softpack.pas              # compile the tool; ignore linker "link.res contains output sections" warnings in Free Pascal 3.0.x
$ fpc softporn_adventure.pas    # compile the game; ignore linker "link.res contains output sections" warnings in Free Pascal 3.0.x

$ ./softpack                    # one-time step; converts softporn.txt to softporn.msg message file
```

## Running

This game is of course entirely text-based, so it runs in a console/terminal.

### From the terminal

```
$ ./softporn_adventure          # runs the game
```

The game has been played through to its winning state, it is verified to work. 

As in the initial help screen, type "save" to save your progress, and "restore" to bring it back. At any point, type "quit" to end.

### From a graphical file explorer

Just click the "Softporn Adventure.desktop" file. No need to install the program in any special location; it will magically run from the folder you've compiled into. (Tested under Linux/KDE Plasma Desktop [5.17.4] using Dolphin.) It will save games to the directory of the executable.

## To do

* Need to figure out why the close() function doesn't want to compile?? It's commented out now.
* softporn-2.inc.pas:91 & :31 change to a real bell

## Further Ports

This shouldn't be too difficult to do--just a matter of some possible ifdef's and testing. Pull requests accepted.
