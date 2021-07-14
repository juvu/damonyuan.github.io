# C4. Naive Bayes

- Statistics tells us that if we need N samples for one feature, we need N^10 for 10 features and N^1000 for our 1000-feature vocabulary. The number will get very large very quickly.
- If we assume independence among the features, then our N^1000 data points get reduced to 1000 * N
  - this is what is meant by **naive** in the Naive Bayes classifier
  - the other assumption we make is that every feature is equally important
- real-world condition
  - prevent getting 0 by initialize all of our occurrence counts to 1 and we'll initialize the denominator to 2
  - underflow: take the natural logarithm of the product
- documentation model
  - set-of-words
  - bag-of-words    
