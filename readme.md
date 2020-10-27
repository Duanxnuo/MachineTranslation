## Project Goal
This research project focuses on using language materials to create a translation mechanism to better assist the international businesses publishing their advertisements. With more customized advertisement materials, this translation mechanism was expected to be more accurate and personalized.


## Main Steps
•	Cleaned and validated all the - about 500,000 - pairs of training sentences to keep the translations consistent in each advertising domain. 
•	Applied and compared four different Chinese word separating systems - character by character, pkuseg, thulac and jieba.
•	Built word embedding and encoder and decoder on all the data using TensorFlow 2.1.0 and tflearn packages.
•	Implemented padding in Keras 2.2.0 to preprocess the sentences. Implemented gradient clipping to avoid gradient exploding. Divided datasets into several epochs and batches as well as specified learning rate to control the learning process. Implemented Adam as optimizer to optimize the model runtime. Utilized grid search to tune these parameters to achieve better accuracies. Visualized the accuracy line charts during the running process for better evaluation using matplotlib.
•	Trained single layer LSTM with attention on 30% of the training sets using those four different mechanisms separately, with GPU on AWS EC2 instance.
•	Evaluated the model accuracy using cross-entropy.

## Environment
AWS S3/EC2, Python 3.7, Spark 2.2.3, TensorFlow 2.1.0, Keras 2.2.0
