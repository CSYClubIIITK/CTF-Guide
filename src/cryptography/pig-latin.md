---
description: The toy of cryptography
---

# Pig Latin

### Introduction

It is a playful cipher in which the English word is encoded by moving consonants and adding some suffix to it with relatively simpler algorithm&#x20;

### How to Identify

Identifying a pig latin encryption is a child's play as in a sentence encoded by pig latin all the words will end with `ay`  &#x20;

### Code / Tool /Algorithm

First of all we will try to understand how can we encrypt some text using pig latin&#x20;

#### Encoding

1. If the length of word is smaller than 3 character then leave it as it is
2. If length is more than 3 character and first character is a consonant then move all the consonants up to first vowel at the back and add a `ay`  at the end&#x20;
3. If the first character is a vowel then keep the word as it is and add a `yay` at the end&#x20;

#### Decoding

1. If length of a word is less than 3 then keep it as it is&#x20;
2. If  length is more than 3 and the word end with `yay` then remove the prefix and check weather it form a real word or not&#x20;
3. if the word end with ay or test no 2 fails then remove the prefix ay and move consonant from the last until you get an English word

#### Program

```python
from nltk.tokenize import word_tokenize
from nltk.corpus import words

# Function to encrypt a single word using Pig Latin rules
def encrypt_word(text):
    vowel = ["a", "e", "i", "o", "u"]
    text = text.lower()
    
    if len(text) <= 3:
        return text  # Ignore words with length less than or equal to 3
    elif text[0] in vowel:
        return text + "yay"  # For words starting with a vowel, add "yay" at the end
    else:
        encrypted_text = text
        for i in text:
            if i in vowel:
                return encrypted_text + "ay"  # Move consonants before the first vowel to the end and add "ay"
            encrypted_text = encrypted_text[1:] + encrypted_text[0]
        return encrypted_text + "ay"

# Function to decrypt a single Pig Latin word back to English
def decrypt_word(word):
    if len(word) <= 3:
        return word  # Ignore words with length less than or equal to 3
    elif word[len(word) - 3:] == "yay":
        return word[:-3]  # For words ending in "yay", remove "yay"
    else:
        word = word[:-2]  # Remove "ay" from the end
        while word not in words.words():  # Rotate the word until it matches an English word
            word = word[-1] + word[:-1]
        return word

# Function to encrypt a complete sentence using the encrypt_word function
def encrypt(text):
    words_list = word_tokenize(text)  # Tokenize the input text into words
    encrypted_text = ""
    
    for i in words_list:
        encrypted_text += encrypt_word(i) + " "  # Encrypt each word and append to the result
    
    return encrypted_text

# Function to decrypt a complete Pig Latin sentence using the decrypt_word function
def decrypt(text):
    text = text.lower()
    words_list = word_tokenize(text)  # Tokenize the input text into words
    decrypted_text = ""
    
    for i in words_list:
        decrypted_text += decrypt_word(i) + " "  # Decrypt each word and append to the result
    
    return decrypted_text

```

before executing the current program first we need to download nltk data which you can download by using following script

```python
import pip

def install(library):
    pip.main(['install', library])

library_name = "requests"
install(library_name)
try:
    import nltk
except:
    install('nltk')
import nltk
nltk.download("words")
nltk.download('punkt')
```

### Sample problem

For example we will take a question from our own Apoorv's treasure hunt&#x20;

```
To whomever it may concern,

Thank you for your inquiry regarding Mr. David Parker's disappearance. I appreciate your concern and your efforts to assist in this matter.

It is indeed troubling that Mr. Parker's knowledge about a colleague's illicit affair with a student may be connected to his sudden disappearance. While I cannot confirm any specifics at this time, it is certainly a possibility that we cannot overlook. I will ensure that this information is brought to the attention of the authorities handling Mr. Parker's case.

In light of your inquiry, I want to provide you with some additional information that may be relevant to our search for Mr. Parker. During my tenure as a colleague of Mr. Parker's, he had previously shared knowledge that he had his college documents archived on a blogspot page.

He also left me with a piece of text, but I'm quite sure it doesn't hold any significance.

The text is as follows:

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor olcay egelay ackbay upeyay ialay stay in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

While I cannot guarantee that the information contained within the archive will provide any definitive answers, I believe it is worth exploring as we continue our efforts to locate Mr. Parker.

If you require any further assistance or have any additional questions, please feel free to reach out to me. I am committed to doing everything in my power to support our efforts to locate Mr. Parker and ensure his safe return.

Thank you again for your cooperation and support.

Best regards,
Nathaniel Crowe
Professor of Physics, USF

```

the above is a mail regarding murder of someone named Elia \
\
on analysing the lorem ipsum text we get the following part where all the words end with ay so it could be encoded using pig latin and was hidden in lorem ipsum&#x20;

```
olcay egelay ackbay upeyay ialay
```

on decoding we get following message \
`col lege back upe lia` \
\
on rearranging spaces we get the message as \
`college back up elia`\
\
and on further investigation the name of criminal was found on college backup server

### References&#x20;

For exploring it further you can refer to \
1\. [https://www.dcode.fr/pig-latin-language](https://www.dcode.fr/pig-latin-language)\
2\. [https://en.wikipedia.org/wiki/Pig\_Latin](https://en.wikipedia.org/wiki/Pig\_Latin)\
For practice problem you can refer to [https://play.picoctf.org/practice](https://play.picoctf.org/practice)

