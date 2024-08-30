# Spellcaster
Processing code to implement John Fairfield's Spellcaster

Processing is a visually-oriented Java-based language developed by 
Casey Reas and Ben Fry. It is open source and available from processing.org.

Spellcaster was originally developed on Apple 2e by John Fairfield in 1984, 
and ported to Commodore 64 by Scott Gilkeson. It was published with a tutorial 
and a book to get you started casting spells.

Spellcaster starts with a dot in the middle of the screen. Each letter key is a 
command that acts on that dot--to move it one step, change the direction,
change the color, or change the location (teleport). You can test whether the
color you are stepping onto matches the current pen color, and branch based
on the result. You can name a series of commands (create a spell) which you
can then cast and include in other spells.

```
Single syllable spells available in Spellcaster:
'key' syllable and meaning:

'A' AKA      : cycle to next color
'B' BO       : set square colour to pen colour then move one step in the current direction
'D' DI       : reverse direction
'E'          : expose (set) teleporter (next character is teleporter name)
'F'          : felt (return to) teleporter (next character is the name)
'G' GO       : move one step in current direction and "wash" both squares with pen colour
'H' HI       : turn to point upwards
'I' IX       : if - exit if matched (pen color and color stepped on)
'J' JO       : move one step in the current direction, not drawing
'K'          : set pen color (next character is A,E,I,O,U - see note about numbers)
'L' LI       : turn left
'M'          : repeat (beginning of word, next character is A,E,I,O,U number)
'N' NU       : repeat indefinitely (must be the beginning of word)
'O' OX       : if not - exit if unmatched (pen color and color stepped on)
'P' PU       : left paren (start new spell/word)
'Q' QUSH     : toggle sound (no sound in this version currently)
'R' RI       : turn right
'S' SPELLS TU: name a spell
'T' TU       : begin spell name
'V' VUZIM    : like W, but doesn't wait - looks for one key spell
'W' WU       : request input until ZIM
'X' XEN      : else (MUST BE AT VERY BEGINNING OF WORD)
'Y' Y        : toggle mirror
'Z' ZIM      : right paren (ends PU or WU phrase, or TU spellname)
' '          : ends word, UNLESS INSIDE A PU OR WU
'!'          : clears screen and resets everything
```

mouse click saves named spells currently in memory to disk file spells.txt

TODO: I don't think VU and WU work correctly, and there may be some problems 
with PU and spaces (it has been a while since I wrote this and I don't remember
all the issues).

Spellcaster had the ability to use arrow keys to back up and go forward, and
could pre-load spells into the key buffer, which was very useful for tutorials.


# note about numbers:
  
  in case of m:

    O A E I U
    0 1 2 3 random
  
  in case of k:
   ku chooses a random colour
  
   if there are four colours, they will be named: 
    KO KA KE KI
  
   if there are sixteen colours their names will be:
  
         -KO  -KA  -KE  -KI
    KO-  KOKO .... .... ....
    KA-  .... KAKA .... ....
    KE-  .... .... KEKE ....
    KI-  .... .... .... KIKI

   just fill in the blanks


# Red Robe Spells:

### BO
  set square colour to pen colour then move one step in the current direction

### JO
  move one step in current direction, not drawing

### GO
  move one step in current direction and "wash" both squares with pen colour

GO makes the pen step one step forward, and it uses the pen color to "wash" both the square it's leaving and the square it arrives on. When Go "washes" a square with the pen color, the square usually changes color, but the new color isn't necessarily the pen color.
What exactly do I mean by "wash"? Well, suppose X and Y are two colors (one of them is the color of the square getting washed, and the other is the pen color). Then these are the three laws of washing:

  1. X washed with Y makes the same color as Y washed with X.

(For instance, if you wash a green square with orange pen color, you get the same color as if you washed an orange square with green pen color.)

  2. X washed with KO (the zero color) makes X.

(That means that washing a square when the pen color is KO doesn't change the square. 1 and 2 together mean that washing a KO colored square with pen color X makes the square X colored.)

  3. If you wash a square twice in a row with the same color, the second time
      "undoes" the effect of the first.
      In other words.
      If X washed with Y makes color Z,
      then Z washed with Y makes X.

### LI RI
  in the main screen: turn left/right

  when on the border, these have no effect. use DI to turn around on the border.

### DI
  turn the pen around, will face left if it was facing right same for up and down.

### HI
  in the main screen: point up.
  in the border: point clockwise

### Y
  mirror drawing along the middle of the screen

### QUSH
  toggle sound on or off (no sound in this version currently)

### AKA
  cycle pen color


## Special keys
  There are a few keys that have special effects when you are using Spellcaster, these  special keys are !, (RETURN), ?, <, >, (BACKSPACE), left arrow, right arrow, -, +, \*.

## Activity change Keys
When you are using Spellcaster, you're usually doing one of three activities.

  1. You're ???? at the drawing screen, casting spells.
  2. You're invoking? at the command menu, choosing a command.
  3. You're  ???? at a page (for example the tutorial).

The following keys take you from one activity to another.

### ! or (RETURN)
  go to the drawing screen and clear the drawing screen

### ?
  go to the command menu

### <
  go to the previous page

### >
  go to the next page

## The keystroke stack
The best way to learn about the keystroke stack, is to type a spell and then play around with the up, down, left and right labeled arrow keys. left will move one keystroke to the stack and right will back it out again. the whole spell can be saved in the stack one by one. the up arrow will bring you to this state in one button press and the down button will cast the whole stack content so far onto the screen.

### Delete
Delete removes the last keystroke from the spell you are typing and redoes the spell up to that point.

### Rightdelete
The rightdelete key removes the topmost keystroke (the one that blinks at you) from the keystroke stack.

### Leftarrow
Leftarrow is like delete, only it puts the deleted keystroke onto the top of the keystroke stack. In this way, the keystroke stack can remember the deleted keystrokes, so that it can cough them up for you when you use rightarrow.

### Rightarrow
Rightarrow removes the top keystroke (the one that blinks at you) from the keystroke stack, and types that key for you.

### superleft arrow
superleftarrow has the same effect as if you beat on the leftarrow key until the entire spell were put into the keystroke stack.

### superright arrow
Superrightarrow has the same effect as if you beat on the rightarrow key until all the keys in the keystroke stack were used up. The superrightarrow key makes Spellcaster start getting keystrokes from the keystroke stack, until the stack is empty, or until you hit 


### Zapperleftarrow
Zapperleftarrow does the same thing as superleftarrow, but it also makes Spellcaster turn off spellcasting. You can still type in spells, but nothing happens on the drawing scring. This is especially handy if you are trying to change a spell that takes a long time to run: you can work much faster if you turn off spellcasting. If spellcasting is turned off and you hit the zapperleftarrow key again, it turns spellcasting back on.



# Defining and Casting Spells

A spell is made of words. Words are made of syllables

Example syllables: BO WU IX MU KA. A syllable is few letters long, and you usually just have to type the first letter to get the whole syllable.

Example words: BORIBOLI XENBO NUBOIX. A word is made of one or more syllables and ends with a blank (though there's one way of enclosing blanks within a word: quickfind PU),

A spell is made of one or more words. Every time you want to cast a spell, do you have to type the whole thing? No, you can give a spell a name, and make the computer remember the spell and its name. Then, every time you type the name of the spell, it happens just as if you had retyped the whole thing.

The next page tells you how to give a spell a name.

# Spells

To give a spell a name, follow these steps:

 1. Type the spell.
 
    Example: NUBORIBOLIIX RIBOBOBO
 
 2. Hit the S key (which stands for the syllable "SPELLS"). The computer will print "SPELLS TU" and wait for you to type any name you want. The TU is a syllable that marks the beginning of a spell name: all spell names begin with TU.
 
    Example: NUBORIBOLIIX RIBOBOBO SPELLS TU

 4. Type a name for your spell.
 
    Example: NUBORIBOLIIX RIBOBOBO SPELLS TUWALLPAPER

 5. Hit the Z key (which stands for the syllable ZIM). All spell mames end with ZIM.

    Example: NUBORIBOLIIX RIBOBOBO SPELLS TUWALLPAPERZIM !