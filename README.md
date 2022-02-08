# wordle

Suggest guesses for Wordle.

Specify what you've tried so far and this script tells you the best words to
try next.

Example:

```shell
$ ./wordle --help
usage: wordle [-h] [--num-suggestions N] [--all] [--debug] [attempts ...]

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
  --all, -a             For each word in the Wordle dictionary, show the best
                        series of guesses
  --debug               Enable debug logging
$
$ ./wordle t/ea/s/e Ao/rt/a
ATTEMPTED:
 1293 tease
  786 aorta

SUGGESTED: (7)
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

A word's score is calculated based on how often each letter appears in each of
the five positions throughout the dictionary.  For example, for the word
"slate":

- There are 366 words with 's' in the 1st position
- 201 with 'l' in the 2nd position
- 307 with 'a' in 3rd
- 139 with 't' in 4th
- 424 with 'e' in 5th

So "slate" gets a score of 1437 = 366 + 201 + 307 + 139 + 424.

The ten best words to start with:

```shell
$ ./wordle | head
SUGGESTED: (2315)
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

With the `--all` option, the script analyzes the whole dictionary.

We can see the three hardest words:

```shell
$ ./wordle --all | sort -r | head -3
8 hound = slate crony bound pound found mound wound hound
8 hatch = slate taint carat batch patch match watch hatch
8 graze = slate crane brake frame grade grape grave graze
$
```

Each of these words (hound, hatch and graze) would take 8 guesses if you
guessed the word most likely to match each time.  But of course you only get 6
guesses.

There are 19 words that take 7 guesses.

```shell
$ ./wordle --all | grep -c ^7
19
$
```

With this scoring algorithm, we can expect 3.8 guesses on average.

```shell
$ wordle --all | awk '{s+=$1} END{print s/NR}'
3.82333
$
```
