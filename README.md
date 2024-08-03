LSTM Sentiment Analysis Documentation
Phase 1: Data Preparation
Several necessary libraries have been imported to prepare the data appropriately, including:

pandas
numpy
regex
string
nltk methods: stopwords, lemmatizer, and tokenizer
Steps:
Slang Dictionary: A dictionary called slang_dict is created to handle different casual abbreviations, extracting the abbreviated meanings behind the slang.
Lemmatizer and Stop Words:
The lemmatizer returns words to their roots to simplify classification and reduce vocabulary size.
A set of stop words is initialized to remove common stop words from the corpus.
Regular Expressions:
One regular expression removes URLs.
Another removes suspiciously placed HTML tags.
Tokenizing the Corpus:
URLs and HTML tags are removed.
Text is converted to lowercase to ensure uniformity.
Punctuation marks are removed as they have less impact in casual text.
CountVectorizer:
Used to determine the vocabulary size, approximately 100k.
Data Organization:
Input and label data are organized into a pandas DataFrame.
The data is split into training and testing sets.
Phase 2: Vectorization
Steps:
Tokenization:
Keras' tokenizer is used to convert string data into numeric vectors.
Padding Sequences:
pad_sequences function ensures all numeric sequences have the same length to avoid errors.
Phase 3: Building the Model
Steps:
Sequential Object Initialization:
Begins the process of creating layers within the model.
Embedding Layer:
Receives and operates on embedded data.
LSTM Layer:
Memorizes the effect of several tokens on the result; the most important layer.
Dropout Layer:
Prevents overfitting within the model.
Dense Layer:
A final dense layer with a single node outputs the classification of the input data.
Phase 4: Hyperparameter Tuning & Fitting the Model
Steps:
Hyperparameter Tuning:
Using keras_tuner, parameters for the network’s layers are randomly changed within a defined range.
The tuner goes through 5 different iterations, each with 2 epochs, aiming to maximize accuracy.
The third trial provides the best accuracy, although the improvement is minimal, indicating potential issues in data preparation or embedding.
Model Compilation:
Compiled using the best hyperparameters:
Learning rate: 0.002
LSTM layer nodes: 160
Dropout layer hyperparameters, etc.
Loss calculated with binary_crossentropy since the model is a binary classifier.
Model Fitting:
The compiled model is fit on the training data.
Checkpoints are set up at each epoch to handle potential technical failures.
The model’s accuracy is 54%, likely due to improper data handling.
