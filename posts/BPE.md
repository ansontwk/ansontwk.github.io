---
layout: default
---

# Byte Pair Encoding of protein sequence

Byte pair encoding(BPE) is an algorithm originally desgined for word compression. This is an example of adopting BPE for tokenziation of protein amino acids sequences to feed it into LLMs. This example will use 2500 completely random sequence of uniform size 50 aa. In practice, the sequence length will be vastly different.

## Prerequisite

* random *(optional)*

## Installation

* None

## Usage

1. Import random and set seed for preproducibility

    ```python
    import random
    SEED = 179180
    random.seed(SEED)
    ```

2. Define the amino acid list and the initial vocabulary. Also initilize and define a maximum vocabulary size. *(e.g. 1024)*

    ```python
    VOCAB = {
    'A': 0, 'C': 1, 'D': 2, 'E': 3, 'F': 4, 'G': 5,
    'H': 6, 'I': 7, 'K': 8, 'L': 9, 'M': 10, 'N': 11,
    'P': 12, 'Q': 13, 'R': 14, 'S': 15, 'T': 16, 'V': 17,
    'W': 18, 'Y': 19, 'X': 20} 

    ```

3. Define housekeeping function to generate a random corpus of sequence and generate random sequences. For this example, a corpus of 2500 random sequence is used to generate the vocabulary.

    ```python
    def gen_random_seq():
        seq = []
        for i in range(50):
            seq.append(random.choice(AMINOLIST))
        return seq

    def gen_corpus(): 
        corpus = []
        for i in range(2500): #generate 2500 random sequences for the corpus
            corpus_seq = gen_random_seq()
            corpus.append(corpus_seq)
        return corpus
    ```

4. Define function for counting the occurences of each consecutive tokens, and return all the counts. 

    ```python
    def count_dipeptide(corpus):
        pass_counts = {}
        for seq in corpus:
            for i in range(len(seq) - 2 + 1):
                try:
                    dipeptide = seq[i] + seq[i+1]
                except:
                    break
                
                if dipeptide not in pass_counts:
                    pass_counts[dipeptide] = 1
                else:
                    pass_counts[dipeptide] += 1
        return pass_counts
    ```
5. Define the function to update each sequence with the most occuring tokens-pairs and another function to update the corpus with the newly merged sequence.

    ```python
    def update_sequence(seq, max_dipeptide):
        new_seq = []
        i = 0
        while i < len(seq):
            if i < len(seq) - 1 and seq[i] + seq[i+1] == max_dipeptide:
                new_seq.append(max_dipeptide)
                i += 2
            else:
                new_seq.append(seq[i])
                i += 1
                    
        return new_seq

    def update_corpus(old_corpus, max_dipeptide):
        new_corpus = []
        for seq in old_corpus:
            new_seq = update_sequence(seq, max_dipeptide)
            new_corpus.append(new_seq)
        return new_corpus
    ```
6. Main BPE program.

    The logic flow is as follow:
    * In every loop, the the all occurences of combinations of tokens is reported.
    * Using the the most ocurring token-pair, update all corpus sequences to merge this combination, if any.
    * Append this token-pair to the vocabulary dictionary.
    
    ```python
    corpus = gen_corpus()
    testfa = gen_random_seq()
    
    org_len = len(testfa)

    while len(VOCAB) < MAX_VOCABSIZE:
        counts = count_dipeptide(corpus)
        max_dipeptide, max_count = max(counts.items(), key=lambda x: x[1])
        
        #add to vocab
        VOCAB[max_dipeptide] = len(VOCAB)
        
        #update corpus
        corpus = update_corpus(corpus, max_dipeptide)
    ```

7. Using the vocabulary, compress the test sequence.

    ```python
    for key, value in VOCAB.items():
        if value >= 21: #skips the 20 base amino acids and X
            testfa = update_sequence(testfa, key)
    ```

8. Compare the original sequence length with the BPE sequence.

    ```python
    print(org_len, len(testfa))
    ```

    The original sequence is 50 aa. The sequence compressed with BPE is 28 tokens long. The compression factor is about 1.8.
    
[back](../)


