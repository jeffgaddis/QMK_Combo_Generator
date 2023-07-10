# QMK_Combo_Generator
Calculates the optimal send string combos for your QMK keyboard


## How to use:
Copy as many lines as you want from the applicable combos_XXX.def file to the appropriate file in your keymap. Be careful not to exceed the space available on your micro controller, if you are not using something like a RP2040 then you will probabably need to limit to 100 combos or less.

The 'thumb' layouts assume that each thumb can press either space or backspace and it uses them as the highest priority key in the combos since thumbs are the strongest fingers.

Referance the QMK documentation if you are not familiar with combos or see the gboards guide: http://combos.gboards.ca/docs/chords/

## How it works:
This notebook is used to automatically determine the best key combos to use for a QMK keyboard. 

- The current combos are for Colemak-DH but you can change the keys and generate it for any other layout
- This system assumes that you have Backspace and Space on separate thumb keys but you can remove backspace if necessary by changing the special key to None or change it to a different key.
- Other combo dictionaries allow 2 key combos and I have found that this can interfere with typing. This system will mostly use 3 key inputs to avoid these issues.
- The outputs are chosen in order of the frequency of their usage, you can force certain words to be ranked higher or force certain combos if you have preferances also.
- I did some cleaning to the datasets so they no longer match exactly to the source, there are definately additional typos that should be fixed
- This should ideally be used with a RP2040 or another board lots of storage space so that you can store more combos than you can remember.
- I think you can probably use this to learn to type over 300 WPM like the stenographers do without the difficult learning curve. This is the first algorithmically generated combo system that I have seen, others seem to just pick combos manually which is tedious and makes it hard to deal with conflicts as the list grows.


### Revision Notes:

The last change seems to work well now for choosing the best keys to include. I noticed that some of the output strings are redundant as you get far down into the list so I still need to fix that but the first 100 seem good.
