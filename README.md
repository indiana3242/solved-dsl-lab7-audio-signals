Download Link: https://assignmentchef.com/product/solved-dsl-lab7-audio-signals
<br>
The main objective of this laboratory is to put into practice what you have learned on classification techniques. You will mainly work on audio signals. In particular, you will try to build a classification model that is able to identify which digit was uttered analyzing the content of short audio samples from different speakers.

<strong>Important note. </strong>For what concerns this laboratory, you are encouraged to upload your results to the competition we launched on <a href="https://www.kaggle.com/">Kaggle</a><a href="https://www.kaggle.com/">,</a> even if the submission will not count on your final exam mark. If you do not have it yet, you will need to create an account. It is <strong>mandatory </strong>to follow the subscription instructions reported in the <a href="http://dbdmg.polito.it/wordpress/wp-content/uploads/2019/11/Data_Science_Lab___Kaggle_competition_guide.pdf">Kaggle guide</a> from the course website, otherwise your score will be excluded from the competition. Reference Section 3 to read more about the competition.

<h1>1          Preliminary steps</h1>

<h2>1.1         Datasets</h2>

<h3>1.1.1         Free Spoken Digit Dataset</h3>

The dataset for this laboratory has been inspired by the <a href="https://github.com/Jakobovski/free-spoken-digit-dataset">Free Spoken Digit Dataset</a><a href="https://github.com/Jakobovski/free-spoken-digit-dataset">.</a>

It is composed of 2,000 recordings by 4 speakers of numbers from 0 to 9 with English pronunciation. Thus, each digit has a total of 50 recordings per speaker. Each recording is a mono wav file. The sampling rate is 8 kHz. The recordings are trimmed so that they have near minimal silence at the beginnings and ends.

The data has been distributed uniformly in two separate collections:

<ul>

 <li>Development (dev): a collection composed of 1500 recordings <strong>with </strong>the ground-truth labels. This collection of data has to be used during the development of the classification model. Each file in this portion of the dataset is a recording named with the following format &lt;Id&gt;_&lt;Label&gt;.wav.</li>

 <li>Evaluation (eval): a collection composed of 500 recordings <strong>without </strong>the labels. This collection of data has to be used to produce the submission file containing the labels predicted for each evaluation recording, exploiting the previously built model. Each file in this portion of the dataset is a recording named with the following format &lt;Id&gt;.wav.</li>

</ul>

So far, you should be used to work, developing your models, with training, validation and test sets. In this case, the Development data must be used to tune your hyper-parameters while you should consider the Evaluation portion as the actual test set.

<h3>1.1.2         Dataset tree hierarchy</h3>

The dataset archive is organized as follows:

<ul>

 <li>dev: the folder that contains the labeled recordings.</li>

 <li>eval: the folder that contains the unlabeled recordings. Use this data to produce the submission file containing the predicted labels.</li>

 <li>csv: a sample submission file.</li>

</ul>

You can find the dataset on the competition we launched on Kaggle. Head to Section 3 to know how to register on Kaggle and download the dataset. For the sake of simplicity, you can also download the dataset at: https://github.com/dbdmg/data-science-lab/raw/master/datasets/free-spoken-digit.zip

<h1>2          Exercises</h1>

In this laboratory you have a single classification task to carry out.

<h2>2.1         Free Spoken Digit classification</h2>

In this exercise you will build a complete data analytics pipeline to pre-process your audio signals and build a classification model able to distinguish between the classes available in the dataset. More specifically, you will load, analyze and prepare the Free Spoken Digit dataset to train and validate a classification model. Finally, you will be able to upload your classification results and participate to the lab competition.

<ol>

 <li>Load the dataset from the root folder. Here the Python’s <a href="https://docs.python.org/3/library/os.html#module-os">os</a> module comes to your help. You can use the os.listdir function to list files in a directory. Furthermore, you can use the wavefile module from SciPy to read a file in wav format. You can read more about it on the <a href="https://docs.scipy.org/doc/scipy/reference/io.html#module-scipy.io.wavfile">official documentation</a><a href="https://docs.scipy.org/doc/scipy/reference/io.html#module-scipy.io.wavfile">.</a></li>

 <li>Focus now on the data preparation step. You should have noticed that wavfile gives you an array of floating point values, plus the sampling rate. Before continuing, take you your time to answer these questions:

  <ul>

   <li>what do these numbers represent?</li>

   <li>were the audios recorded under the same conditions? (e.g. recording volume, noise, etc.)</li>

   <li>do the arrays have an equal length? How different lengths could impact on your pre-processing solution? If it was needed, could you figure a way out to align them to the same number of sample?</li>

  </ul></li>

</ol>

Now, in order to train your model, you are required to design and build a vector representation. This mainly involves extracting several features out of your initial representation. Bear in mind that, since you are dealing with audio signals, you can work either on the time domain or the frequency one. In the former case, you might opt, for example, to split the signal into chunks and characterize them by means of statistical measures (e.g. mean, standard deviation). In the latter case, you can base your features on the frequencies contained in the signal. This involves reshaping the signal using a transformation function (e.g. Fourier transform) and work on its spectrum of frequencies (e.g. spectogram). Data preparation on frequencies can be hard to carry out. To know more about it, please refer to Camastra and Vinciarelli 2015 and Oppenheim and Schafer 2014, and Presti and Neri 1992.

Identify a set of possible feature candidates and transform your data using them.

<ol start="3">

 <li>Once you have your vector representation, choose one classification algorithm of those you know. Then, perform the classic training-validation pipeline on the Development dataset to identify the best set of hyper-parameters for your model. As you can read in section 3, we will evaluate your results on the Mean F1 score. Hence, it is a reasonable option trying to optimize it on the Development dataset <a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>.</li>

</ol>

<strong>Info: </strong>the Mean F1 score, also known as <em>macro average</em>, calculates the F1 for each label, and computes their unweighted mean. This does not take label imbalance into account.

<ol start="4">

 <li>Assign a classification label (i.e. the spoken digit) to each recording in the Evaluation dataset.</li>

 <li>Submit your results to the Kaggle competition. Head to section 3 to know more about it.</li>

 <li>Compile your final report and upload it to the “Portale della Didattica” as described in section 2.</li>

</ol>

<a href="#_ftnref1" name="_ftn1">[1]</a> Actually, since your task does not present class imbalance, optimizing the classification accuracy would have been equally correct.