### Results from experimenting with various parameters

_Note: With default parameters LinearSVC was giving highest accuracy, hence all the results other than Machine learning
algorithms' parameter tuning, i.e feature generation and vectorization results are produced using LinerSVC model of
sklearn. Features used all the time, 'including' the case while testing feature stack, are - NER, TAG, DEP, is-STOP.
Accuracy mentioned is empirical accuracy (percent)_

#### CountVectorizer of sklearn

1. Various `ngram_range`, (min, max) value:
    1. (1, 2) - 59.0%
    2. (3, 5) - 57.4%
    3. (2, 3) - 57.8%
    4. (3, 4) - 57.2%
    5. (1, 3) - 58.4%
    
Hence, adding longer and more n_gram range is not a good way to generate text features for question dataset. 
For the results below ngram_range=(1, 2) was used. 

#### Feature Generation (Feature stack)

1. 'TAG' is just more fine grained form of POS in spaCy lib. With 'POS' instead of 'TAG' - 55.6%. 
And with 'TAG' - 59.0%. More information can be found at spaCy [token](https://spacy.io/api/token) documentation.
2. 'Words' added as feature - 81.9% 
3. 'Lemma' (stem form of the word) added as feature - 82.7%
4. 'Lemma', 'Shape', 'is-Alpha' added as features - 83.9%
5. 'Lemma', 'is-Alpha' added as features - 82.8%
6. 'Lemma', 'Shape' added as features - 84.2%

Hence, from point 1 it is clear that accuracy and depth of the NLP lib can distinctively affect the results. From point
2 and 3 we conclude that stem form of the word is more useful as a feature than the word itself. From point 4, 5 and 6
we can conclude that shape or length of the word is more effective feature than the feature telling us, the word
is an alphabet or not.

#### Logistic Regression (lr)

1. All Default - 80.4%
2. `solver="newton-cg"` - 80.8%, increasing the number of max_iter also gives the same results.

#### Support Vector Machine (svm)

1. All Default - 27.8%
2. `gamma=1E-6` - 2.4%
3. `C=0.025` - 2.4%
4. `max_iter=750` - 14.2%

#### Linear Support Vector Machine (linear_svm)

_LinearSVC module is more efficient than svm with kernel="linear"_

1. All Default - 84.2%
2. `loss="squared_hinge"` and `dual=False` - 84.2%, with `dual=True` also gives same accuracy.
