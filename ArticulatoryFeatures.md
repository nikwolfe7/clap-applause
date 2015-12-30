# Features from AF files #
```
1: Voiced/unvoiced
2: Vowel length d - 
3: Vowel length l - 
4: Vowel length s - 
5: Vowel length a - 
6: Vowel height 1 - close?
7: Vowel height 2 - mid?
8: Vowel height 3 - open?
9: Vowel front 1 - front?
10: Vowel front 2 - central?
11: Vowel front 3 - back?
12: Vowel rounding
13: Consonant type s - stop
14: Consonant type f - fricative
15: Consonant type a - approximate
16: Consonant type n - nasal
17: Consonant type l - liquid
18: Consonant type r - lateral approximate?
19: Consonant place l - labiodental
20: Consonant place b - bilabial
21: Consonant place d - dental
22: Consonant place a - alveolar
23: Consonant place p - postaveolar
24: Consonant place v - velar
25: Consonant place g - glottal
26: Silence
```

These are binary features indicating presence or absence of that particular feature. However, since you are using a neural network to extract these values directly from the audio, you'll get a number which is sort of like a probability of that feature occurring.