# Cryptography

`The Code Book - Simon Singh` is a fantastic introduction to this topic.

!!! note "Tools to help identify the cipher"

    - [dcode - cipher identifier](https://www.dcode.fr/cipher-identifier)

    - [Boxentriq - cipher identifier](https://www.boxentriq.com/code-breaking/cipher-identifier)

    - [Cryptocrack - suite of crypto tools](https://sites.google.com/site/cryptocrackprogram/home)

    - [CyberChef - magic analysis tool](https://gchq.github.io/CyberChef/#recipe=Magic\(3,false,false,''\))

---

## Monoalphabetic vs. Polyalphabetic Ciphers

We can categorise a cipher as being either `monoalphabetic` or `polyalphabetic` - determined by the mapping of the letters between the ciphertext and the plaintext.

!!! definition "Define: Monoalphabetic cipher"
    **ciphers in this category**: Caesar, substitution, ROT-13, etc.

    A one-to-one mapping - e.g. the plaintext letter 'a' is always represented by the ciphertext letter 'e', and vice versa.

!!! definition "Define: Polyalphabetic cipher"
    **ciphers in this category**: Vigenère, Enigma, etc.

    A many-to-many mapping - e.g. the plaintext letter 'a' is represented by several ciphertext letters.

---

## Entropy

!!! definition "Define: Entropy"
    A measure of uncertainty/ randomness - decimal value in the range 0 (no randomness) to 8 (complete randomness).

    Calculate using tools such as [CyberChef's entropy tool](https://gchq.github.io/CyberChef/#recipe=Entropy\('Shannon%20scale'\)) - using the `Shannon scale` to evaluate the result.

    [NIST publication](https://tsapps.nist.gov/publication/get_pdf.cfm?pub_id=915121)

- `3 to 3.5` - standard English text
    - likely to be a **monoalphabetic cipher**

- `7.5+` - encrypted/compressed data
    - likely to be a **polyalphabetic cipher**

---

## Index of Coincidence

!!! definition "Define: Index of Coincidence (IoC)"
    Calculates whether the distribution of letters is similar or not to the expected frequency.

    [dcode - index of coincidence calculator](https://www.dcode.fr/index-coincidence)

- `0.0667` - English language

- `~0.070` - ciphertext similar to plaintext
    - **transposition cipher** - where letter positions have been changed, but the characters used in the plaintext and the ciphertext are identical

    - **monoalphabetic substitution cipher** - where letters have been replaced with alternative letters (i.e. Caesar cipher)

- `~0.0385` - ciphertext appears to be random
    - **polyalphabetic cipher** - where a plaintext letter has been replaced by multiple alternative letters (e.g. Vigenère cipher)

    - generally, the lower the IoC value, the more alphabets used

---

## Frequency Analysis: Letters

!!! note "Letter frequencies (English)"
    `E`-`T`-`A`-`O`-`I`-`N`-`S`-`R`-`H`-`D`-`L`-`U`-`C`-`M`-`F`-`Y`-`W`-`G`-`P`-`B`-`V`-`K`-`X`-`Q`-`J`-`Z`

    [Graph representation - Cornell](https://pi.math.cornell.edu/~mec/2003-2004/cryptography/subs/frequencies.html)
    
    [Relative Frequencies of Letters in General English Plain Text - Robert Edward Lewand](https://web.archive.org/web/20070122235914/http://pages.central.edu/emp/LintonT/classes/spring01/cryptography/letterfreq.html)

Longer ciphertexts are preferred for frequency analysis, as with shorter ciphertexts you may not get a good sample of all of the letters.

---

## Frequency Analysis: Digrams, Trigrams, and n-grams

This is particularly useful when the ciphertext hasn't been obfuscated by removing the spaces, or formatting it into equally-sized blocks.

Just like letters, some words are more common than others in the English language.

*If you look at Lewand's digram analysis, you'll notice that it differs from the above results - likely as a result of the 13-year gap between the two studies. As the English language evolves and words become more-and-less popular, the frequency of certain bigrams, trigrams, and n-grams is going to shift.*

!!! note "Define: Digrams"
    Two letter words - e.g. `is`, `an`, `on`, `in`

In descending order of frequency, the most common digrams include:

`TH`, `HE`, `IN`, `ER`, `AN`, `RE`, `ON`, `AT`, `EN`, `ND`, `TI`, `ES`, `OR`, `TE`, `OF`, `ED`, `IS`, `IT`, `AL`, `AR`, `ST`, `NT`, `TO`...

[SAS Blog - Bigram Frequency](https://blogs.sas.com/content/iml/2014/09/26/bigrams.html)

!!! note "Define: Trigrams"
    Three letter words - e.g. `and`, `the`, `was`, `all`, `ill`, `far`

In descending order of frequency, the most common trigrams include:

`THE`, `AND`, `ING`, `ENT`, `ION`, `HER`, `FOR`, `THA`, `NTH`, `INT`, `ERE`...

[Practical Cryptography - English Letter Frequencies](http://practicalcryptography.com/cryptanalysis/letter-frequencies-various-languages/english-letter-frequencies/)

---

### Highlighting the Importance of Choosing the Right Corpus for Analysis

We saw that the figures differed between the three linked articles.

Two factors can have a large impact on the frequencies: *when* and *where* the text is from.

!!! note "Example: Comparing frequency analysis of three sources"
    *Scientific paper* - include a lot of Latin scientific names, and without abbreviations or contractions.

    *Sunday newspaper* - more colloquial phrasing, contractions, and simpler terminology to make it more accessible to the general public.

    *Student text conversation transcripts* - very informal language, abbreviations/contractions/acronyms used throughout, and repeat occurances of particular letters - e.g. `pleaassseeeeee` instead of `please`.

---

### Chi-Squared Analysis
*Most useful for shift ciphers.*

!!! definition "Define: Chi-Squared Analysis"
    Used to compare the distribution of characters in the ciphertext against the expected distribution of the plaintext.
    
    The **lower the score, the better fit** to the expected distribution (frequency).

    [Southampton University - chi squared tool](https://www.southampton.ac.uk/~wright/1001/chi-squared-test.html)

    [CryptoCrack - chi squared calculator](https://sites.google.com/site/cryptocrackprogram/user-guide/statistics-tab/chi-square)


#### Solving a Vigenère Cipher

We can visibly confirm that the right shift has been found when solving a monoalphabetic cipher (single Caesar cipher).

However a Vigenère cipher requires you to effectively **solve multiple Caesar ciphers**, but we cannot visibly confirm that the right shift has been found.

Chi-squared analysis allows you to find the shift with the lowest score - likely to be the correct shift.