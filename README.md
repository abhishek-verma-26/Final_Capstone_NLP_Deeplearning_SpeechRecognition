# Final_Capstone_NLP_Deeplearning_SpeechRecognition

Describe your model in detail?

In this notebook, I propose a model to predict errors in speech recognition text played with low, moderate to strong background noise. Most of the audio speech occuring in real world is mostly coupled with some background noise which can lead to incorrect translations. It could be a mis-translation of a voice command, a speech, movie subtitle etc. Using NLP and deep learning flows, I build a speech error prediction model. This model takes a speech translated text and outputs possible error words associated to the texts.

For modelling purpose, I choose the Recurrent Neural Network(RNN) framework with one bi-direction LSTM hidden layer.

Speech converted texts are subsampled into three word vectors containing the current scanned word, previous and next word. Each given sentences is subsampled and feed to the model as input. In this fashion we increase the training sample for wording errors and bring the word position information in modelling.

The model output is a 4 element vector containing error probabilities based on the word positioning in the three word vector. Based on this information a list of word with error probabilities within a sentence is constructed.

Why you chose it ?

One major benefit of RNN type models in NLP based modelling is its ability to deal with sequential information. Since in our case, we are dealing with sequence of words where the combination and positioning of words matters, the RNN or LSTM based neural network helps in capture those dependencies.

Why it works

The modelling of the RNN is based of speech conversion samples from noisy audio clips. In our case, statistically we find more number of case where one word was mistranslated into another word. This approach helps in simplifying the modelling to simple wording errors rather than large textual error (less than 5% cases).

Also by using the three word subsampling approach our modelling is exposed to more cases of wording errors along with word positioning and context.
What problem it solves

Our model predicts possible wording errors in speech translation as a result of background noises. It also provided a error confidence level with the associated word

How it will run in a production like environment

In a production enviroment, this model will be attached to the speech recognition tool. As an audio speech is translated, the textual content is sent to this model as inputs of 3 word vectors. The error prediction is carried out and word with errors are highlighted based on their confidence level.

A trained speech correction model (text recommendation) or a grammer correction model can be added to operated on the predicted word providing corrections to the overall speech translation.

What would you need to do to maintain it going forward?

The challenge for the modelling scheme is to propagate the prediction errors to the model on untrained data (real world scenario). One possible way would be to apply background noise filtering externally from the audio clips and apply speech recognition tool to build a clean speech version. The filtering can be varied from low, mild to harsher cleanup forming an ensemble based modelling.

If a translation is identified as having no speech error, it shall be passed as the most accurate speech translation. The remaining speech translation can be stored and be effectively used for training the model in production run.

Limitation
I list the limitations on the NLP based model proposed here

The underlying assumption is that only the presence of noise creates speech recognition error. However, speech text errors can also be made by various sources such as mis-pronounciations, language accent, speaker voice quality etc. This implies that the clean speech text may not always yield a good text to compare our modelled noisy texts.
The input to RNN network only contains the previous and next words (3 word string in total). If a larger dataset is available, the bi-gram or tri-gram wording can also be included to provide more contextual information of the word and hence improve the prediction accuracy.
To increase the accuracy of our model prediction, a much larger set of speech texts should be used. In total only 5660 unique token (words) are taken into account. For a better generalization of the model, a large volume of speech to text can be included in our modelling.
Our model is based on one-word error presumption. As we have shown, multiple cases of errors were found, where one word could be mis-translated into multiple words and vice-versa.
Most of the mistranslations are for prepositions and articles word that are higher in word frequency.

Modelling Improvements
There are many possible ways that our NLP modelling can be improved:

The process of data augmentation can be followed. We have clean audio which can be superimposed with many different noise types at various db levels. This procedure can increase the dataset size and provide more texts to train the models.
Also, more speeches can be included in our training. The data website https://datashare.is.ed.ac.uk/handle/10283/2791 has one more set of speeches that included 58 speakers and hence a large augmented audio list can be used. Also audio clip such as story telling, podcast imposed with simulated noise can also serve to increase the word vocabulary and generalize the modelling to a wide variety of speech audios.
Data augmentation in terms of addition rhyming words can be implemented as well. For each errored words a set of rhyming words can be inserted to increasing training data size.
Input Subsampling with word vector (3) can be increased (5 or 7) to provide contextual and word combination information to the modelling
With large vocabulary dataset, we can propagate our model to text recommendation model, which can help provide word correction to the speeches
