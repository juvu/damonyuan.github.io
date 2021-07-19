# C2. kNN

1. [kNN in scikit](https://scikit-learn.org/stable/modules/neighbors.html)
2. key notes
   1. Euclidian distance
   2. the first k or lowest k distances are used to vote
   3. normalization -> from 0 to 1 or from -1 to 1; newValue = (oldValue - min)/(max-min)