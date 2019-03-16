# Vocabulary builder for BERT


<strong>Modified, simplified version of subword_builder.py and its dependencies included in 
[tensor2tensor library](https://github.com/tensorflow/tensor2tensor), making its output fits to 
[google research's open-sourced BERT project](https://github.com/google-research/bert).</strong>

***
Although google opened pre-trained BERT and training scripts, 
they didn't open source to generate wordpiece(subword) vocabulary matches to vocab.txt in opened model.<br>
So I modified subword_builder.py of tensor2tensor library 
which is one of suggestions google mentioned to generate wordpiece vocabulary.

###Modifications
- <strong>Original SubwordTextEncoder adds \"\_\" at the end of subwords appear 
on the first position of words. 
So I changed to add \"\_\" at the beginning of subwords follow other subwords, 
using _my_escape_token() function,
and later substitued \"\_\" with "##"</strong>

- Generated vocabulary contains all characters and all characters having "##" in front of them.
For example, `a` and `##a`.

- Made standard special characters like `!?@~` 
and special tokens used for BERT, ex : `[SEP], [CLS], [MASK], [UNK]` to be added. 

- Removed irrelevant classes in text_encoder.py, 
commented unused functions some of which seem to exist for decoding,
and removed mlperf_log module to make this project independent to tensor2tensor library.


###Requirement
- tensorflow