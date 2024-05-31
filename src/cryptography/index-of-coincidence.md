---
description: First test on encoded text
---

# Index of Coincidence

### Introduction

The index of coincidence (IC or IoC) is an indicator used in cryptanalysis which makes it possible to evaluate the global distribution of letters in an encrypted message for a given alphabet.

it can easily be calculated using following formula&#x20;

$$
IC = \sum_{i=A}^{Z} \frac{n_i(n_i - 1)}{N(N - 1)}
$$

with ni the number of occurrences of the letter i in the text and N the total number of letters.

### Use Case

It can be used for any encoded text to get a rough idea about the Algorithm used to encode it&#x20;

In cryptography we can classify all algorithms in mainly following 2 categories:&#x20;

#### Monoalphabetic substitution

In this type of cipher text each alphabet is either shifted by some position or replaced by a specific alphabet they are generally easy to decode.

IoC value of a monoalphabetic substitution is similar to plain text that is about 0.07

#### Polyalphabetic substitution

In this type of cipher text a character or a group of character is replaced by another group of character they are relatively difficult to decode

IoC value of polyalphabetic cipher is smaller around 0.03-0.04

### Code&#x20;

We can also calcualte IoC usign the followign python code&#x20;

```python
def index_of_coincidence(text):
    # Remove spaces and convert to uppercase (standard practice for cryptographic analysis)
    text = text.replace(" ", "").upper()
    
    # Length of the text
    n = len(text)
    
    # Frequency of each letter in the text
    frequency = {}
    for letter in text:
        if letter.isalpha():  # Consider only alphabetic characters
            frequency[letter] = frequency.get(letter, 0) + 1

    # Calculate the index of coincidence
    ic = 0
    for count in frequency.values():
        ic += count * (count - 1)
    
    if n > 1:
        ic /= (n * (n - 1))
    else:
        ic = 0  # If the text length is 1 or less, IC is 0 by definition

    return ic
```

### Example

Let us take some example to have a better understanding \
"Gwzd zd bo bqqzon hzuwna"\
\
By using the above python code we get index of coincidence as 0.063 which  is closer to 0.07 so this is a monoalphabetic substitution cipher \
and on further analysis which will be covered in other section we get the decoded message as "This is an affine cipher"

### References

To study further about this topic you can refer to following website&#x20;

{% embed url="https://www.dcode.fr/index-coincidence" %}

{% embed url="https://www.dcode.fr/affine-cipher" %}

### Conclusion&#x20;

Index of coincidence is the first tool which we can use to shorten the list of possible encryption algorithms but this is not the only method so keep on exploring ...
