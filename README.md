# QMK_Combo_Generator
Calculate the optimal send string combos for your QMK keyboard


## How it works:
This notebook is used to automatically determine the best key combos to use for a QMK keyboard. 

- You will most likely need to limit the combos to about 100 but if you have more storage space then this could create as many combos as you want
- The current combos are for Colemak-DH but you can change the keys and generate it for any other layout
- This system assumes that you have Backspace and Space on separate thumb keys but you can remove backspace if necessary by changing the special key to None
- Other combo dictionaries allow 2 key combos that can interfere with typing, this system will mostly use 3 key inputs to avoid these issues
- The output are chosen based on the frequency of their usage, so you should not have to hunt for words unless you have a specific need
- This output also includes programming specific words that I chose, these would not be highly ranked for standard typing
- I did some cleaning to the datasets so they no longer match exactly to the source
