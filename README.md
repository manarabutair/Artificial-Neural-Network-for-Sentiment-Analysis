# LSTM Sentiment Analysis Documentation

## Phase 1: Data Preparation

Several necessary libraries have been imported to prepare the data appropriately, including:
- **pandas**
- **numpy**
- **regex**
- **string**
- **nltk** methods: stopwords, lemmatizer, and tokenizer

### Steps:
1. **Slang Dictionary**: A dictionary called `slang_dict` is created to handle different casual abbreviations, extracting the abbreviated meanings behind the slang.
2. **Lemmatizer and Stop Words**: 
   - The lemmatizer returns words to their roots to simplify classification and reduce vocabulary size.
   - A set of stop words is initialized to remove common stop words from the corpus.
3. **Regular Expressions**: 
   - One regular expression removes URLs.
   - Another removes suspiciously placed HTML tags.
4. **Tokenizing the Corpus**: 
   - URLs and HTML tags are removed.
   - Text is converted to lowercase to ensure uniformity.
   - Punctuation marks are removed as they have less impact in casual text.
5. **CountVectorizer**: 
   - Used to determine the vocabulary size, approximately 100k.
6. **Data Organization**:
   - Input and label data are organized into a pandas DataFrame.
   - The data is split into training and testing sets.

## Phase 2: Vectorization

### Steps:
1. **Tokenization**: 
   - Keras' tokenizer is used to convert string data into numeric vectors.
2. **Padding Sequences**: 
   - `pad_sequences` function ensures all numeric sequences have the same length to avoid errors.

## Phase 3: Building the Model

### Steps:
1. **Sequential Object Initialization**: 
   - Begins the process of creating layers within the model.
2. **Embedding Layer**: 
   - Receives and operates on embedded data.
3. **LSTM Layer**: 
   - Memorizes the effect of several tokens on the result; the most important layer.
4. **Dropout Layer**: 
   - Prevents overfitting within the model.
5. **Dense Layer**: 
   - A final dense layer with a single node outputs the classification of the input data.

## Phase 4: Hyperparameter Tuning & Fitting the Model

### Steps:
1. **Hyperparameter Tuning**: 
   - Using `keras_tuner`, parameters for the network’s layers are randomly changed within a defined range.
   - The tuner goes through 5 different iterations, each with 2 epochs, aiming to maximize accuracy.
   - The third trial provides the best accuracy, although the improvement is minimal, indicating potential issues in data preparation or embedding.
2. **Model Compilation**: 
   - Compiled using the best hyperparameters:
     - Learning rate: 0.002
     - LSTM layer nodes: 160
     - Dropout layer hyperparameters, etc.
   - Loss calculated with `binary_crossentropy` since the model is a binary classifier.
3. **Model Fitting**: 
   - The compiled model is fit on the training data.
   - Checkpoints are set up at each epoch to handle potential technical failures.
   - The model’s accuracy is 54%, likely due to improper data handling.
