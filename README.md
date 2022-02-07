# wordle
Suggest guesses for Wordle.

Specify what you've tried so far and this script tells you the best words to
try next.

Example:

```
$ ./wordle --help
usage: wordle [-h] [--num-suggestions N] [--debug] [attempts ...]

Suggest Wordle guesses

positional arguments:
  attempts              For each attempt: X - an uppercase letter is correct
                        and in the right place, x - a lowercase letter is
                        correct but in the wrong place, /x - letter is not in
                        the solution

options:
  -h, --help            show this help message and exit
  --num-suggestions N, -n N
                        Maximum number of suggestions to show (default: 10)
  --debug               Enable debug logging
$
$ ./wordle t/ea/s/e Ao/rt/a
  874 aloft
  839 allot
  780 atoll
  778 afoot
  736 about
  708 adopt
  599 abbot
$
```

The number in the first column is the "score" for that word.
A higher number means the word is more likely to be right.

The ten best words to start with:

```
$ ./wordle | head
 1437 slate
 1411 sauce
 1409 slice
 1403 shale
 1398 saute
 1393 share
 1392 sooty
 1382 shine
 1381 suite
 1378 crane
$
```

A variant of the `wordle` script is `wordle-all`.

```
$ ./wordle-all --help
usage: wordle-all [-h] [--debug]

For each word in the Wordle dictionary, show the best series of guesses

options:
  -h, --help  show this help message and exit
  --debug     Enable debug logging
$
```

We can see the three hardest words:

```
$ ./wordle-all | sort -r | head -3
8 hound = slate crony bound pound found mound wound hound
8 hatch = slate taint carat batch patch match watch hatch
8 graze = slate crane brake frame grade grape grave graze
$
```

Each of these words (hound, hatch and grace) would take 8 guesses if you
guessed the word most likely to match each time.  But of course you only get 6
guesses.

There are 19 words that take 7 guesses.

```
$ ./wordle-all | grep -c ^7
19
$
```
