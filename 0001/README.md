# Problem 1

The language is [Shakespeare](https://esolangs.org/wiki/Shakespeare).

## Starting from the basics

To keep things simple, I went with the O(1) solution without any loops.

The multiples of `k` below 1000 are `k, 2k, 3k, ...` up to `m = 999 // k`, so their sum is `k` times the `m`th triangular number. Multiples of 15 land in both piles, so subtract them once:

```python
def t(k):
    m = 999 // k
    return k * m * (m + 1) // 2

print(t(3) + t(5) - t(15))
```

The rest is turning that into a play.

## Mapping it onto a stage

| Python | Shakespeare |
| --- | --- |
| `999` | Romeo |
| `total` | Juliet |
| `total = x` | Romeo says `You are x` to Juliet |
| `999` inside `t(k)` | `me`, since Romeo is the one speaking |
| `print(total)` | `Open your heart` |

Numbers are nouns. A noun is 1 and each adjective doubles it, so `a cat` is 1 and `a big big cat` is 4. There are no numerals, so 3 is `the sum of a big cat and a cat`.

You can only assign to the person you're talking to. Romeo holds 999 and never changes, Juliet takes every result, so Romeo does all the talking.

## One term

`t(3)`, written out:

```
Romeo: You are as good as the product of the sum of a big cat and a cat and the quotient between the product of the quotient between me and the sum of a big cat and a cat and the sum of the quotient between me and the sum of a big cat and a cat and a cat and a big cat!
```

Read it inside out. `the quotient between me and the sum of a big cat and a cat` is `999 // 3`, and it appears twice because there is nowhere to put an intermediate. Division floors, which is what makes `999 // 5` come out at 199 instead of 199.8. The rest is `m * (m + 1) / 2`, then times 3.

The other two lines are the same shape with 5 and 15, one adding to Juliet and one subtracting.

## Writing 999

Out of doubling nouns, 999 is 512 + 256 + 128 + 64 + 32 + 4 + 2 + 1. That's 82 words. Shakespeare has `the cube of`, and 999 is 10 cubed minus 1:

```
Juliet: You are as bad as the difference between the cube of the sum of a big big big cat and a big cat and a cat!
```

21 words, same number.


## Running it

```
pip install shakespearelang
python -c "from shakespearelang import Shakespeare; Shakespeare(open('0001.spl').read()).run()"
```
