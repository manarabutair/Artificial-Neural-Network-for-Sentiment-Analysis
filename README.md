LSTM SENTIMENTAL ANALYSIS DOC
Phase 1: Data preparing:
Several necessary libraries have been imported in order to prepare the data appropriately, namely: pandas, numpy, 
regex, string, and some nltk methods: stopwords, lemmatizer, and tokenizer.
A dictionary is first created to handle different casual abbreviations; its primary purpose is to extract the abbreviated 
meanings behind the slang. This dictionary is called ‘slang_dict’.
First, the lemmatizer and a set made up of stop words are initialized. The lemmatizer will be used to return words to 
their roots; to simplify classification and reduce the vocabulary size. The set of stop words is necessary to remove the many stop 
words that exist inside the corpus.
Second, two regular expressions are initialized; one for removing URLs, the other for removing suspiciously placed 
HTML tags.
The process of tokenizing the corpus begins by first removing any URLs, then removing the HTML tags. The text is 
then lowered to so the model doesn’t treat the same words differently. Finally, punctuation marks are removed; because they 
don’t make as much of an impact in casual text as they in formal text.
By using the CountVectorizer, we can extrapolate the size of the vocab, that being 100k. We organize the input and label data on a 
Panda’s dataframe in order to split into training and testing data.
Phase 2: Vectorization:
We use keras’ tokenizer to vectorize the string data and turn it into numeric vectors. In order to avoid further errors, we 
use the pad_sequences function to give all numeric sequences the same length.
Phase 3: Building the Model:
We initialize a Sequential object to begin creating layers within the model. First is the embedding model, which is 
created to receive and operate in embedded data; the data we’ve embedded beforehand. Then, we create the LSTM layer, which 
is the layer that memorizes the effect of several tokens on the result; it’s the most important one. Thirdly, the dropout layer, this 
layer is here to prevent any overfitting within the model. Finally, we add a final dense layer with a single node; this node will 
output the final result of the network, it’s the classification of the inputted data.
Phase 4: Hyperparameter Tuning & Fitting the Model:
Before compiling the NN, we must first find an appropriate set of parameters for the network’s layers. We use 
keras_tuner to randomly change the parameters within a defined range for each one. It’ll only go through 5 different iterations of 
different parameters, with each iteration run with 2 epochs. The objective of the hyper-tuning is to maximize the accuracy.
After we finish through all iterations of the different hyperparameters, we see that the third trial provided the best 
accuracy, albeit the difference is extremely small. The issue here seems to be beyond the NN model itself, and might be because 
of failure in preparing or embedding the data properly.
We compile the NN using the best hyper-parameters available: Learning rate is set at 0.002, the LSTM layer has 160 
nodes, the dropout layer’s hyperparameter etc…
The loss is calculated with ‘binary_crossentropy’ because the model itself is essentially a binary classifier.
We fit the compiled model on the training data and setup checkpoints at each epoch in case of some techhnical failure. 
The model’s accuracy is at a disappointing 54%, which again, is most likely because of improper data handling
