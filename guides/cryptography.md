# Cryptography

> `The Code Book - Simon Singh` is a fantastic introduction to this topic.

## Identifying the Cipher Category

Some useful tools for identifying the cipher type:
- [dcode - cipher identifier](https://www.dcode.fr/cipher-identifier)
- [Boxentriq - cipher identifier](https://www.boxentriq.com/code-breaking/cipher-identifier)
- [Cryptocrack - suite of crypto tools](https://sites.google.com/site/cryptocrackprogram/home)
- [CyberChef - magic analysis tool](https://gchq.github.io/CyberChef/#recipe=Magic(3,false,false,''))

These tools can usually identify the cipher (or at least narrow it down to a group of ciphers) and will save you a *lot* of time in the CTF - but as always, software makes mistakes.

That's why I find it useful to have a general understanding of the basics behind cryptographic statistical analysis so that I can just double check any assumptions that are made along the way. Plus it's a really interesting topic!

### Monoalphabetic vs. Polyalphabetic

The easiest way to narrow down the cipher type is to determine which category it falls into.

The category is determined by the mapping of letters between the ciphertext and the plaintext.

If there is a one-to-one mapping, then the cipher is *monoalphabetic*.
- e.g. the plaintext letter `a` is always represented by the ciphertext letter `e` (as occurs in a Caesar cipher with shift 5).

- **ciphers in this category**: Caesar, substitution, ROT-13, etc.

If there is a many-to-many mapping, then the cipher is *polyalphabetic*.
- e.g. the plaintext letter `a` is represented by several ciphertext letters.

- **ciphers in this category**: Vigenère, Enigma, etc.

But how can we determine the appropriate category? *Statistical analysis*.

### Entropy

Calculate the entropy of a string using tools such as  [CyberChef's entropy tool](https://gchq.github.io/CyberChef/#recipe=Entropy('Shannon%20scale')) to determine whether it is encrypted/compressed or not.

> `entropy` - the measure of randomness/uncertainty (see [NIST publication](https://tsapps.nist.gov/publication/get_pdf.cfm?pub_id=915121) for more information)

We can use the `shannon scale` to evaluate the result of these entropy calculations.
- the score will be a decimal in the range 0 (no randomness) to 8 (complete randomness)
- standard English text falls in the range 3 to 3.5
- encrypted/compressed data (of a reasonable length) has a score over 7.5

This can help us to narrow down the type of cipher. Assume for the purpose of this guide that the plaintext will always be in English.

> The linked tool `Cryptocrack` has the benefit of providing analysis support for multiple languages. Every language has very different letter frequencies, and so trying to apply the same expected frequency data to different languages will give you useless results.

**A monoalphabetic cipher: entropy score of 3 - 3.5** - this is because the one-to-one mapping maintains the same frequency patterns - just with different letters.
- it is fact that the most common plaintext letter is `e`
- as there is a one-to-one mapping, we can therefore say with certainty that the most frequent ciphertext letter **must** map to `e`

**A polyalphabetic cipher: entropy score of 7.5+** - the many-to-many mapping creates a high degree of randomness, making any potential frequency analysis useless.
- the plaintext `e` might map to letters `f`, `o`, and `x` - but the letter `x` might also map to `h`
- therefore frequency analysis is no longer useful as we cannot say with any certainty now that the most frequent plaintext letter is the correct mapping to `e`

### Index of Coincidence

Very similar to `entropy`, we can use the `Index of Coincidence (IoC)` to determine whether the distribution of letters is similar or not to the English language (or other languages).

[dcode - index of coincidence calculator](https://www.dcode.fr/index-coincidence)

- `0.0667` - English language

- `~0.070` - ciphertext similar to plaintext
    - **transposition cipher** - where letter positions have been changed, but the characters used in the plaintext and the ciphertext are identical

    - **monoalphabetic substitution cipher** - where letters have been replaced with alternative letters (i.e. Caesar cipher)

- `~0.0385` - ciphertext appears to be random
    - **polyalphabetic cipher** - where a plaintext letter has been replaced by multiple alternative letters (e.g. Vigenère cipher)

    - generally, the lower the IoC value, the more alphabets used


## I've Identified the Category ... Now What?

### Frequency Analysis: Letters

[Relative Frequencies of Letters in General English Plain Text - Robert Edward Lewand](https://web.archive.org/web/20070122235914/http://pages.central.edu/emp/LintonT/classes/spring01/cryptography/letterfreq.html)

The alphabet in frequency order, highest to lowest (
[see graph representation - Cornell](https://pi.math.cornell.edu/~mec/2003-2004/cryptography/subs/frequencies.html)).

> `E`, `T`, `A`, `O`, `I`, `N`, `S`, `R`, `H`, `D`, `L`, `U`, `C`, `M`, `F`, `Y`, `W`, `G`, `P`, `B`, `V`, `K`, `X`, `Q`, `J`, `Z`

Longer ciphertexts are preferred for frequency analysis, as with shorter ciphertexts you may not get a good sample of all of the letters.

**Example:**

*Capitalisation of letters only for the purpose of differentiating between plaintext and ciphertext letters.*

> gsrh rh zm vcznkov lu z hfyhgrgfgrlm xrksvi dsviv gsv zokszyvg szh yvvm ivevihvw

- entropy score: 3.9 (within the English language range)
- performing letter frequency analysis on this ciphertext:

    - V: 12× (17.91%)	
    - G, S, H, Z: 6× (8.96%)
    - R: 5×	(7.46%)
    - I: 4×	(5.97%)
    - M, K, Y: 3× (4.48%)
    - O, L, F: 2× (2.99%)
    - C, N, U, X, D, E, W: 1× (1.49%) 

- if we assume all instances of `v` in the ciphertext map to `E` in the plaintext:

> gsrh rh zm EcznkoE lu z hfyhgrgfgrlm xrksEi dsEiE gsE zokszyEg szh yEEm iEeEihEw

- the problem then comes with the next letters - without further statistical analysis, we can't tell which ciphertext letter (from `g`, `s`, `h`, or `z`) maps to the plaintext letter `T`

- this is where frequency analysis of diagrams, trigrams, and n-grams comes in handy...

### Frequency Analysis: Digrams, Trigrams, and n-grams

`Digrams` - two letter words - e.g. `is`, `an`, `on`, `in`

`Trigrams` - three letter words - e.g. `and`, `the`, `was`, `all`, `ill`, `far`

`N-grams` - `n` letter words

This is particularly useful when the ciphertext hasn't been obfuscated by removing the spaces, or formatting it into equally-sized blocks.

Just like letters, some words are more common than others in the English language.

Some of the most frequent bigrams are as follows, in descending frequency ([SAS blog - bigram frequency](https://blogs.sas.com/content/iml/2014/09/26/bigrams.html)).

> `TH`, `HE`, `IN`, `ER`, `AN`, `RE`, `ON`, `AT`, `EN`, `ND`, `TI`, `ES`, `OR`, `TE`, `OF`, `ED`, `IS`, `IT`, `AL`, `AR`, `ST`, `NT`, `TO`...

*If you look at Lewand's digram analysis, you'll notice that it differs from the above results - likely as a result of the 13-year gap between the two studies. As the English language evolves and words become more-and-less popular, the frequency of certain bigrams, trigrams, and n-grams is going to shift.*

[Practical Cryptography - English Letter Frequencies](http://practicalcryptography.com/cryptanalysis/letter-frequencies-various-languages/english-letter-frequencies/)

In descending order of frequency, the most common trigrams include:

> `THE`, `AND`, `ING`, `ENT`, `ION`, `HER`, `FOR`, `THA`, `NTH`, `INT`, `ERE`...

*Again, you'll notice that whilst the list of most frequent bigrams is more similar to that of the linked SAS research, it differs as you move down the list.*

#### Highlighting the Importance of Choosing the Right Corpus for Analysis

Looking specifically at bigram frequency, we saw that the figures differed between the three linked articles.

This is partially due to the three sources being researched across the span of a decade, and so the English language will be slightly different at the point of each study. Especially with the growing influence of the Internet and social media on our vocabulary, the popularity of certain words rises-and-falls more quickly than ever.

Perhaps more importantly however is the corpus on which the study is completed - i.e. where is the text coming from?

---

#### Example

Imagine comparing the results of frequency analysis performed on three sources:
- a scientific research paper on a Biology topic,
- the Sunday newspaper, and
- the transcripts of messages sent between school students.

The scientific paper will likely include a lot of Latin scientific names. Words won't be abbreviated or use contractions, but instead will be written out in full.

The Sunday newspaper will have more colloquial phrasing, likely using contractions and fewer 'complicated' words - making it more accessible to the general public.

The transcripts of student's conversations however will be very different from the previous two sources. Abbreviations will be used throughout, as the language will be very informal, with acronyms used instead to save time. However, there'll also be an increase in particular letters, as the last letteers in words are often repeated to make a point or soften the tone of the message.

- e.g. `pleaassseeeeee` instead of `please`

---

### Chi-Squared Analysis
*Most useful for shift ciphers.*

Used to compare the distribution of characters in the ciphertext against the expected distribution of the plaintext ([Southampton University - chi squared tool](https://www.southampton.ac.uk/~wright/1001/chi-squared-test.html)).

[CryptoCrack - chi squared calculator](https://sites.google.com/site/cryptocrackprogram/user-guide/statistics-tab/chi-square)

The **lower the score, the better fit** to the expected distribution (frequency).

#### Solving a Vigenère Cipher

A Vigenère cipher requires you to effectively solve multiple Caesar ciphers.

Unlike solving a monoalphabetic cipher (single Caesar cipher), where trying every possible shift will eventually give you the decrypted plaintext (which we can visibly confirm as it will be readable!), we need to identify the correct Caesar cipher shift for each alphabet without being able to visibly identify this.

This is where chi-squared analysis comes in handy - as we can identify the shift with the lowest score, and this is likely to be the correct shift for each alphabet.

