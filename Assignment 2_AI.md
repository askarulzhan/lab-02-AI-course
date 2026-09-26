**Assignment 2 · Lab 02 --- Open the box**

**Askar Ulzhan**

**Part 0 --- a token is not a word.** First I wrote my prediction, then
I ran the code. The word \"бөлімшеңізде\" got 19 tokens, close to my
prediction of 15-20. The Russian word \"банк\" got 5 tokens instead of
1, because GPT-2 was trained mostly on English text. Merges only happen
for pairs of letters that are common in training data. Cyrillic letters
are rare there.

**Part 1 --- the output is 50,257 numbers (10 min).** My prediction was
wrong. The #1 token is Ast at 22.87%, not Paris. Paris is second at
22.08% - almost a tie only 0.8% apart. GPT-2 copied Astana from the
context. The top ten tokens hold only 64.0%, not more than 90%. So the
distribution is flat, the model is not sure. The output has 50,257
numbers (logits), and after softmax they sum to 1.0000. This confirms
slide 14, the model outputs a list of probabilities, not a word.

I checked probabilities for a few prompts. The top token is not always
the correct answer. For example, \"Kazakhstan is famous for\" gave
\"its\" as the top token, not a real fact. This shows the model does not
\"know\" facts. It only predicts the most common next word from
patterns.

Temperature and top-p. I checked that temperature changes the shape of
the distribution, but it does not change the order of tokens - the top-1
token stays the same at every temperature. Top-p works differently, it
deletes some tokens completely, sets them to zero, not just changes
their shape.

**Part 2 --- attention is a table of weights.** I found one head (layer
4, head 11) that always looks at the previous token - a clear diagonal
line on the heatmap. I also found a head (layer 7, head 10) that puts
almost all its attention on the first token of the sentence. This does
not mean the first word is important. Softmax makes every row sum to 1,
so a head puts extra weight on the first token when it has nothing
useful to look at.

**Part 3 --- the model in Kazakh.** I compared tokens per character for
English, Russian, and Kazakh. Russian(1.11) and Kazakh(1.10) got similar
numbers, both much worse than English (0.22). The problem is not the
Kazakh language. The problem is GPT-2\'s vocabulary table, it has almost
no merges for Cyrillic letters, so both languages break into single
bytes.

**Conclusion.** All three claims from the lecture were true in this
test. GPT-2 gives a list of probabilities, not a word. Temperature
changes the shape of the list, but not the order. Attention is a table
of weights, and every row sums to 1.

**Declaration on the Use of AI\
**I used DeepSeek while working on this lab. I used it only to check my
answers after I wrote them myself and ran the code. I also asked it to
explain difficult terms like merge, logit, softmax, and attention sink
in simple words. DeepSeek also helped me translate a few words and make
my sentences shorter.
