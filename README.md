# QMK_Combo_Generator
This python notebook calculates the optimal send string combos for your QMK keyboard.

I have attached the combos.def files generated for english words using common layouts so that you can just add them to your QMK files. The 'standard' files assume that the space key is the only thumb key and '2 thumbs' files assume that you have space on one thumb key and backspace on the other.

## How to use with QMK:
Copy as many lines as you want from the applicable combos_XXX.def file to the appropriate file in your keymap. Be careful not to exceed the space available on your micro controller, if you are using something newer like a RP2040 then you can probably use about 7,500 combos, older boards will probably need to limit to around 100 combos.

The '2 thumbs' layouts assume that one thumb can press space while the other presses backspace so that all 10 fingers are available. You can find/replace backspace if you want to use a different 2nd thumb key.

Reference the QMK documentation if you are not familiar with combos or see the gboards guide: http://combos.gboards.ca/docs/chords/

There are also examples on my github profile.

## How to know what keys generate a word

Each word will be assigned to the key combo that uses as many reachable letters as possible from left to right. This is the most natural and memorable way to assign them since you would already be reaching for the keys in this order for regular typing.

You will need to skip letters that are in a column where the finger is already being used. For example, the word 'because' on a QWERTY keyboard will use the keys: B, E, A, U, S. The C key is skipped because it will conflict with the E key which also requires the left middle finger. These conflict rules are assigned based on an ortholinear grid layout it does not expect you to shift your hand to reach keys in unexpected columns. An example of this is the word 'through' where the assigned QWERTY keys are just: T, H, O. If you use a standard keyboard with staggared keys instead of ortholinear you may feel like you could also use your left middle finger to reach the R key but that key is assigned to the index finger only. If not for the staggering, that was added originally just to support typewriter mechanisms, it would feel like a significant hand movement to reach the R key like this. Once you are used to the assigned columns for each finger you will find that it is easy to know what keys to use.


## How the notebook works:
This notebook is used to automatically determine the best key combos to use for a QMK keyboard. 

- The current combos are for Colemak-DH and QWERTY but you can change the keys and generate it for any other layout
- Other combo dictionaries allow 2 key combos and I have found that this can interfere with typing. This system will mostly use 3 key inputs to avoid these issues.
- The outputs are chosen in order of the frequency of their usage, you can force certain words to be ranked higher or force certain combos if you have preferences also.
- I did some cleaning to the datasets so they no longer match exactly to the source, there are probably additional typos that should be fixed and weird copy write text from the books that were referenced
- This should ideally be used with a RP2040 or another micro-controller with lots of storage space so that you can store more combos.
- I think you can probably use this to learn to type over 300 WPM like the stenographers do without the difficult learning curve. I have looked through other combo lists and nothing seems to be as complete and easy to use as this so I would recommend it for all keyboards.


## Data used

The data used to generate the combos came from the following sources:
- [https://www.kaggle.com/datasets/dongjie/word-frequency-enwiki](https://www.kaggle.com/datasets/dongjie/word-frequency-enwiki)
  - license: Database: Open Database, Contents: Database Contents
- [https://storage.googleapis.com/books/ngrams/books/datasetsv2.html](https://storage.googleapis.com/books/ngrams/books/datasetsv2.html)
  - license: Creative Commons Attribution 3.0 Unported License

### Revision Notes:

I completely revised the process to change from the shortest combos possible to the longest possible. This makes it a lot easier to remember or guess combos and shouldn't affect speed much since all keys are press at the same time no matter what.

I also made several other improvements.

There were too many shingles that no human would want (for example 'tha' is common but unwanted) so it is now limited to a fixed list of prefixes and suffixes. The word length weight system was dropped so that weight is only determined by the word frequency.

The rules that limit hard to reach combos were changed so that it will now save the difficult combo but it then continue checking for an easier combo. When this happens you will see the same word sequentially repeated more than 2x in the combos.def file and the final combo will be the easiest to use. It will not allow impossible combos, only combos where you need to reach in awkward ways. For example, on a standard QWERTY layout you can type 'which' by pressing all the letters but you will find that 'w' and 'c' are difficult to reach so the ideal combo is (KC_H, KC_I, KC_W).

For layouts that use the 2 thumb version, this change de-prioritized backspace in combos because it was previously hard to know when it would be used. Backspace is now used when there are no other options without it or when the output is multiple words. An example of this in QWERTY is "there" (KC_BSPC, KC_E, KC_H, KC_T) because more frequent words use all the available options (also 'r' and 't' conflict).

To further increase the chance of guessing the correct combo, this change added 10 repeat attempts at finding more combos for words.
