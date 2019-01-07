# SM-2 (Super Memo 2)

Here is the description of the algorithm used in SuperMemo 1.0.SuperMemo 1.0 was soon replaced by a nicer SuperMemo 2.0 that I could give away to friends at university. There were insignificant updates to the algorithm that was named Algorithm SM-2 after the version of SuperMemo. This means there has never been Algorithm SM-1.

To this day, Algorithm SM-2 remains popular and is still used by applications such as Anki, Mnemosyne and more.

## Application of a computer to improve the results obtained in working with the SuperMemo method

_Here I is Dr Piotr Woz_

Dr Piotr Wozniak wrote the first SuperMemo program in December 1987 (Turbo Pascal 3.0, IBM PC). It was intended to enhance the SuperMemo method in two basic ways:

- apply the optimization procedures to smallest possible items (in the paper-based SuperMemo items were grouped in pages),
- differentiate between the items on the base of their different difficulty.

Having observed that subsequent inter-repetition intervals are increasing by an approximately constant factor (e.g. two in the case of the SM-0 algorithm for English vocabulary), I decided to apply the following formula to calculate inter-repetition intervals:

```


    I(1):=1

    I(2):=6

    for n>2 I(n):=I(n-1)*EF

    where:

        I(n) - inter-repetition interval after the n-th repetition (in days)
        EF - easiness factor reflecting the easiness of memorizing and retaining a given item in memory (later called the E-Factor).

```

E-Factors were allowed to vary between 1.1 for the most difficult items and 2.5 for the easiest ones.

Shortly after the first SuperMemo program had been implemented, I noticed that E-Factors should not fall below the value of 1.3. Items having E-Factors lower than 1.3 were repeated annoyingly often and always seemed to have inherent flaws in their formulation (usually they did not conform to the [minimum information principle](http://supermemo.guru/wiki/Minimum_information_principle)).

Thus not letting E-Factors fall below 1.3 substantially improved the throughput of the process and provided an indicator of items that should be reformulated. The formula used in calculating new E-Factors for items was constructed heuristically and did not change much in the following 3.5 years of using the computer-based SuperMemo method.

In order to calculate the new value of an E-Factor, the student has to assess the quality of his response to the question asked during the repetition of an item (my SuperMemo programs use the 0-5 grade scale - the range determined by the ergonomics of using the numeric key-pad). The general form of the formula used was

```
    EF':=f(EF,q)

    where:

        EF' - new value of the E-Factor
        EF - old value of the E-Factor
        q - quality of the response
        f - function used in calculating EF'.

```

`EF':=EF-0.8+0.28*q-0.02*q*q`

`EF'=(q-4)(0.02q-0.2)`

## Algorithm

1. Split the knowledge into smallest possible items.
2. With all items associate an E-Factor equal to 2.5.
3. Repeat items using the following intervals:

```
I(1):=1
I(2):=6
for n>2: I(n):=I(n-1)*EF
where:

   I(n) - inter-repetition interval after the n-th repetition (in days),
   EF - E-Factor of a given item
```

If interval is a fraction, round it up to the nearest integer.

4. After each repetition assess the quality of repetition response in 0-5 grade scale:

```
    5 - perfect response
    4 - correct response after a hesitation
    3 - correct response recalled with serious difficulty
    2 - incorrect response; where the correct one seemed easy to recall
    1 - incorrect response; the correct one remembered
    0 - complete blackout.
```

5. After each repetition modify the E-Factor of the recently repeated item according to the formula:

```
    EF':=EF+(0.1-(5-q)*(0.08+(5-q)*0.02))
    where:

        EF' - new value of the E-Factor,
        EF - old value of the E-Factor,
        q - quality of the response in the 0-5 grade scale.

    If EF is less than 1.3 then let EF be 1.3.
```

6. If the quality response was lower than 3 then start repetitions for the item from the beginning without changing the E-Factor (i.e. use intervals I(1), I(2) etc. as if the item was memorized anew).
7. After each repetition session of a given day repeat again all items that scored below four in the quality assessment. Continue the repetitions until all of these items score at least four.

## Results

During the first year of using the SM-2 algorithm (learning English vocabulary), I memorized **10,255 items**. The time required for creating the database and for repetitions amounted to **41 minutes per day**. This corresponds to the acquisition rate of **270 items/year/min**. The overall retention was 89.3%, but after excluding the recently memorized items (intervals below 3 weeks) which do not exhibit properly determined E-Factors the retention amounted to **92%**.
