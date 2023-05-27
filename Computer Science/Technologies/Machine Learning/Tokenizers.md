## Subword tokenization
The idea is that common words should not be broken down into smaller character encodings. They also encode what words are start and ending of words (like a prefix or suffix). Depending on the encoder it can be with "##" or "\_" but most words are broken down into parts.

### WordPiece
TODO
### Unigram
TODO

### Byte Pair Encoding (BPE)
One of the initial inspirations for subword tokenization scheme. It is a a compression technique from the 1994, by Philip Gage, "A New Algorithm for Data Compression" paper.
![[../../../NotebookAssets/bpe_example.gif]]
This technique mixed with as the main means to do subword compression allowed for rare words in corpuses to be encoded and tokenized. Rather than the being labeled as "unk" as they may have never been in the original corpus.

It does this by breaking up words into their components. For example "athazagoraphobia" my not be in the wiki raw corpus, however, the individual 