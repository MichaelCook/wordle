# wordle
Suggest guesses for Wordle.

Specify what you've tried so far and this script tells you the best words to
try next.

Example:

```
$ ./wordle --help
usage: wordle [-h] [attempts ...]

Suggest Wordle guesses

positional arguments:
  attempts    For each attempt: X - an uppercase letter is correct and in the
              right place, x - a lowercase letter is correct but in the wrong
              place, /x - letter is not in the solution

options:
  -h, --help  show this help message and exit
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
