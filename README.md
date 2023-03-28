# Music_Genre_Classification
Categorizing songs based on extracted attributes from audio files. Data from the GTZAN Dataset - Music Genre Classification

![jazz00000](https://user-images.githubusercontent.com/120589094/228378619-4e492ca1-32c9-4a1b-8613-cf4b81e1e71e.png)*Spectrogram of jazz00000.wav audio file*

## Overview
A DJ has a disorganized collection of audio tracks from recording samples over the years. The DJ wants to be able to sort each of these samples into the appropriate genres to make them easy to catalog and search through.
<br>
<br>
Since the DJ has no information on the samples but their audio files, we have been enlisted to create a classification model that can sort the audio tracks into genres. The final model was accurately classifying audio files into genres 82% of the time. 
<br>
<br>
This model was limited by the amount of data I had for each of the 10 genres (only 100 samples each). For a more accurate model, I would spend time increasing the size of my data and well as try to better select which columns/features to extract from the audio files to begin with. I would also increase the number of genres as the dataset grows so that it can be more applicable to unseen data.

## Business Understanding
A DJ has a disorganized collection of audio tracks from recording samples over the years. The DJ wants to be able to sort each of these samples into the appropriate genres to make them easy to catalog and search through.
<br>
<br>
Since the DJ has no information on the samples but their audio files, we have been enlisted to create a classification model that can sort the audio tracks into genres.

## Data Understanding
I chose to use ["GTZAN Dataset - Music Genre Classification" from Kaggle](https://www.kaggle.com/datasets/andradaolteanu/gtzan-dataset-music-genre-classification) which is a dataset of 1000 audio tracks of a 30-second duration. The 1000 rows of data are evenly divided into 10 genres with 100 tracks each. All the original audio files are in 22050Hz Mono 16-bit files in .wav format.

On Kaggle, we fortunately had a csv file available with features already extracted from each audio file. In "features_30_sec.csv" which I am using, each row represents a 30-second long song recording. The columns contain a mean and variance computed over multiple features that can be extracted from an audio file using the Librosa python package.

Predictive Features with some of the strongest correlations:

<img width="466" alt="spec_cent_mean_vs_rolloff_mean" src="https://user-images.githubusercontent.com/120589094/224121169-84fa0a57-524d-430b-816e-7910ba4a0db2.png">

<img width="458" alt="spec_cent_mean_vs_mfcc2_mean" src="https://user-images.githubusercontent.com/120589094/224121202-7a0ccb86-4ba5-45fd-83ea-1458bdd1ed4d.png">

For the most part,it seems the variables that are means are generally correlated with means and variables that are variances are correlated with variances. Genres seem to appear in clusters showing that similar genres likely have similar audio features. We will drop the columns mfcc2_mean, spectral_centroid_mean, and rolloff_mean in order to remove correlation close that is at or over 0.9 or -0.9.

## Modeling
If we know that our data contains 10 genres of 100 samples each, then it reasons that our **model-less baseline** accuracy would be 10%; meaning that if we predicted that every song sample was 1 genre, we would be right 10% of the time. That's a pretty low baseline so I'm confident our model will perform better.

### Final Model
Our best model seemd to be our 11th Model that was a tuned stack of 5 different alogorithms (Logistic Regression, Quadratic Discriminant Analysis, K-Nearest Neighbor, Random Forest, and XG Boost).
<br>
<br>
Although it still overfit on the training data (**96.75%** accuracy score), our test accuracy score was the highest we've seen at **82%**.

## Evaluation
Let's take a look at our best model's confusion matrix.

![11th_Model_Confusion_Matrix](https://user-images.githubusercontent.com/120589094/224121565-6fcad1a1-75cf-435c-b710-8ce7e4b9fa80.png)

In our final model, our accuracy, precision, and recall all scored 70% or higher on unseen/test data which is a promsing sign of the model's success.

### Conclusion
Our results show that the audio data of a song is similar to other songs in their genre and thus can be used to separate and classify music. Our results also shows that this is a difficult problem as genres overlap and some genres can be mistaken for others quite often (for example: 3 reggae songs being classified as hiphop).

This model was limited by the amount of data I had for each of the 10 genres (only 100 samples each). For a more accurate model, I would spend time increasing the size of my data and well as try to better select which columns/features to extract from the audio files to begin with. I would also increase the number of genres as the dataset grows so that it can be more applicable to unseen data.

## Repository Structure
```
├── data
├── .gitignore
├── Music_Genre_Classification.ipynb
├── README.md 
└── presentation.pdf
```
