## Project Overall
For this project, we tried natural language processing on over 500,000 pairs of English and Chinese sentences. The goal is to build a villina machine translation programme and try out the four different Chinese word seperating systems to see which one performs better.

The results were evaluated by cross entropy and pkuseg turns out to be the best one, although there wasn't any big differences between these four systems because of the language material was carefully scrutinized by us and was labeled by different domain, so the machine translation machanism a.k.a. the LSTM model with attention was smart enough to do a mostly accurate translation. But we also thinks that when the language material wasn't looked at and was performed translation on in their raw state, the scaling up process would require a better word seperating system. 

To look at the core of each chinese word seperating system, we can see why pkuseg would perform better. This mechanism allows for different seperating rules would the same character combination came up and the ability of defining the seperating rule for each one can also be boosted by attention mechanism.


## Main Steps
•	Cleaned and validated all the - about 500,000 - pairs of training sentences to keep the translations consistent in each advertising domain. 

•	Applied and compared four different Chinese word separating systems - character by character, pkuseg, thulac and jieba.

•	Built word embedding and encoder and decoder on all the data using TensorFlow 2.1.0 and tflearn packages.

•	Implemented padding in Keras 2.2.0 to preprocess the sentences. Implemented gradient clipping to avoid gradient exploding. Divided datasets into several epochs and batches as well as specified learning rate to control the learning process. Implemented Adam as optimizer to optimize the model runtime. Utilized grid search to tune these parameters to achieve better accuracies. Visualized the accuracy line charts during the running process for better evaluation using matplotlib.

•	Trained single layer LSTM with attention on 30% of the training sets using those four different mechanisms separately, with GPU on AWS EC2 instance.

•	Evaluated the model accuracy using cross-entropy.

## Environment
AWS S3/EC2, Python 3.7, Spark 2.2.3, TensorFlow 2.1.0, Keras 2.2.0



## Materials from Google's LSTM Paper
Our model consists of a deep LSTM network with 8 encoder and 8 decoder layers using attention and residual connections.

To improve parallelism and therefore decrease training time, our attention mechanism connects the bottom layer of the decoder to the top layer of the encoder. 

To accelerate the final translation speed, we employ low-precision arithmetic during inference computations. 

To improve handling of rare words, we divide words into a limited set of common sub-word units ("wordpieces") for both input and output.

Our beam search technique employs a length-normalization procedure and uses a coverage penalty, which encourages generation of an output sentence that is most likely to cover all the words in the source sentence.



One of the most effective techniques to improve NMT with monolingual data is back-translation. If our goal is to train an English-to-German translation model, then we first train a model for German to English and use it to translate all the monolingual German data. We then simply train the final English-to-German model on both the existing and new data. Our paper shows that it is important how the data is translated and that deliberately not always choosing the best translation, through sampling, is very beneficial.

If we add 226 million back-translated sentences to the existing training data of 5 million sentences, then we can dramatically improve translation quality. The graph below shows the accuracy of this system on the test set of the standard WMT’14 English-German benchmark on the left (fairseq & monolingual data). This system can be trained in 22.5 hours on 16 DGX-1 machines. It also shows the accuracy of DeepL, a specialized translation service that relies on high-quality human translations, which previously reported the best performance on this benchmark.

We also improved the speed with which fairseq can translate once a model has been trained. In particular, we implemented clever caching, or removing finished sentences from the computation and batching by the number of words instead of sentences. This improved the speed by nearly 60 percent. The figure below shows a comparison with other popular tool kits. Simply changing from Float 32 to Float 16 improved speed by 40 percent.
