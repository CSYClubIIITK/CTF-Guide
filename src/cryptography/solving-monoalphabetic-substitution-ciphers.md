---
description: >-
  here we will learn how  we can solve the easiest of all the monoalphabetic
  substitution ciphers
---

# Solving Monoalphabetic Substitution Ciphers

### Introduction

A Monoalphabetic substitution cipher is a simple cipher in which we replace each character of our message by another character either based on some function or by using some random mapping&#x20;

### How to identify

Now the most important question is how we can identify whether the given cipher text is a monoalphabetic cipher or not in the first place for that you can refer to our page on [Index of coincidence](index-of-coincidence.md) which will help you solve this doubt

### Code/tools/websites

Now since we know that how we can identify this cipher text and what it is so finally and most importantly how can we encode or decode the text.\
For that the most simple and basic approach is to take pen and paper and start rewriting the text by replacing character by referring to the mapping but for large text this can really be a headache and time consuming method so we go by the better approach to write some program to do this task for us&#x20;

#### Encoding

we can encode our text in following way

* using some function
* using a stored map

here we will see both approaches one by one

**Using Some Function**\
for simplicity let us take a linear function for now

$$
f(x) = (ax+b)Mod26
$$

```python
// Some code
def gcd(a, b):
    """Compute the greatest common divisor of a and b"""
    while b != 0:
        a, b = b, a % b
    return a

def affine_encrypt(text, a, b):
    """Encrypt the text using the affine cipher with keys a and b"""
    # Check if a and the alphabet size (26) are coprime
    if gcd(a, 26) != 1:
        raise ValueError("a and 26 are not coprime, encryption is not possible.")

    result = ""
    for char in text:
        if char.isalpha():
            # Convert char to uppercase to handle uniformly
            char = char.upper()
            # Apply the affine transformation: E(x) = (a*x + b) % 26
            encrypted_char = chr(((a * (ord(char) - ord('A')) + b) % 26) + ord('A'))
            result += encrypted_char
        else:
            result += char

    return result
```

**Using a random map**\
for our case we are going to use following mapping  which you can change as per your wish

```python
{
        "a":"b",
        "b":"c",
        "c":"d",
        "d":"e",
        "e":"f",
        "f":"g",
        "g":"h",
        "h":"i",
        "i":"j",
        "j":"k",
        "k":"l",
        "l":"m",
        "m":"n",
        "n":"o",
        "o":"p",
        "p":"q",
        "q":"r",
        "r":"s",
        "s":"t",
        "t":"u",
        "u":"v",
        "v":"w",
        "w":"x",
        "x":"y",
        "y":"z",
        "z":"a"
    }
```

Python code

```python
def encode(text):
    text=text.lower()
    encoding_map={
        "a":"b",
        "b":"c",
        "c":"d",
        "d":"e",
        "e":"f",
        "f":"g",
        "g":"h",
        "h":"i",
        "i":"j",
        "j":"k",
        "k":"l",
        "l":"m",
        "m":"n",
        "n":"o",
        "o":"p",
        "p":"q",
        "q":"r",
        "r":"s",
        "s":"t",
        "t":"u",
        "u":"v",
        "v":"w",
        "w":"x",
        "x":"y",
        "y":"z",
        "z":"a"
    }
    encoded_text=""
    for char in text:
        if char in encoding_map:
            encoded_text+=encoding_map[char]
        else:
            encoded_text+=char
    return encoded_text
```

#### Decoding

For decoding we just need to follow the given steps until we get the complete map

* Scan through the cipher, looking for single-letter words. They’re almost definitely _A_ or _I._
* Count how many times each symbol appears in the puzzle. The most frequent symbol is probably _E._ It could also be _T, A,_ or _O,_ especially if the cryptogram is fairly short
* Pencil in your guesses over the ciphertext. Do typical word fragments start to reveal themselves? Be prepared to erase and change your guesses!
* Look for apostrophes. They’re generally followed by _S, T, D, M, LL,_ or _RE._
* Look for repeating letter patterns. They may be common letter groups, such as _TH, SH, RE, CH, TR, ING, ION,_ and _ENT._
* Scan for double letters. They’re most likely to be _LL,_ followed in frequency by _EE, SS, OO,_ and _TT_ (and on to less commonly seen doubles).
* Two-letter words almost always have one vowel and one consonant. The five most common two-letter words, in order of frequency, are _OF, TO, IN, IS,_ and _IT._
* The most common three-letter words, in order of frequency, are _THE, AND, FOR, WAS,_ and _HIS_
* The most common four-letter word is _THAT._ An encrypted word with the pattern 1 - - 1 is likely to be _THAT._ However, the pattern 1 - - 1 also represents 30 other words, so keep this in mind!

### Sample problem

As an example today lets solve a question form [picoctf.org](https://play.picoctf.org/) which is one of the best platform to practice for your CTF's

<figure><img src="../.gitbook/assets/the_numbers.png" alt=""><figcaption></figcaption></figure>

and the question text was given as follows "The numbers... what do they mean?" and the flag format is "picoctf{....}"

so from looking at the image we can some fragment of map as follows&#x20;

```json
{
    "a":"_",
    "b":"_",
    "c":"3",
    "d":"_",
    "e":"_",
    "f":"6",
    "g":"_",
    "h":"_",
    "i":"_",
    "j":"_",
    "k":"_",
    "l":"_",
    "m":"_",
    "n":"_",
    "o":"15",
    "p":"16",
    "q":"_",
    "r":"_",
    "s":"_",
    "t":"20",
    "u":"_",
    "v":"_",
    "w":"_",
    "x":"_",
    "y":"_",
    "z":"_"
}
```

and on observing the pattern that each character is replaced by their place number so we can complete it as follows

```json
{
    "a":"1",
    "b":"2",
    "c":"3",
    "d":"4",
    "e":"5",
    "f":"6",
    "g":"7",
    "h":"8",
    "i":"9",
    "j":"10",
    "k":"11",
    "l":"12",
    "m":"13",
    "n":"14",
    "o":"15",
    "p":"16",
    "q":"17",
    "r":"18",
    "s":"19",
    "t":"20",
    "u":"21",
    "v":"22",
    "w":"23",
    "x":"24",
    "y":"25",
    "z":"26"
}
```

and the text decode to "picoctf{thenumbersmason}" which is our flag

### References

For further practice you can try some challenges on  [picoctf.org](https://play.picoctf.org/) \
and for decoding texts you can use tools like [cyberChef](https://gchq.github.io/CyberChef/) ,[ dCode](https://www.dcode.fr/en) and can further explore internet for more

### Conclusion

In short in this page first we studied about what a monoalphabetic cipher is then we studied how we can encode and decode text after that we solved a problem for better clarification and at last we discussed about some tools which you can use to decode texts&#x20;
