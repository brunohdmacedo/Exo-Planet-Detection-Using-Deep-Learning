# Exo-Planet-Detection-Using-Deep-Learning
A Deep Convolutional Neural Network Architecture to correctly Identify whether a given Signal is a transiting Exo-Planet or a false Positive.

## Directory Structure
 
The directory Contains the Following Files:-

1.**NoteBooks** :- This folder Contains Jupyter notebooks on various architectures used for Exo-Planet Detection using the Kepler Labelled Time-Series Dataset Provided in Inter IIT Tech Meet 2017. The dataset can be found at Kaggle [here](https://www.kaggle.com/keplersmachines/kepler-labelled-time-series-data/tasks).

2.**Transit Photometry** :- This file Contains references to explanation of Transit Photometry(The technique used for Detecting Exo-Planets).

3.**Models** :- This Folder Contains Saved Weights of Trained Architectures.

## Project Summary

### Method of Detection

The technique used for Exo-Planet Detection in this Project is Transit Photometry. In Simple Terms, when an Exo-Planet revloves around its Star, the light Intensity coming from the star is Captured. When the Planet Comes in front of the star, Some portion of the Star is Obscured and there is dip in light Intensity for some Period of Time. Using the amount of dip in light intensity and the time-period for this event, we can determine whether the Revolving body is an Exo-Planet or not. More Details can be found in the links given [here](https://github.com/omkaranustoop/Exo-Planet-Detection-Using-Deep-Learning/blob/master/Transit%20Photometry)

### Data Pre-Processing

#### Data Labelling

The Dataset Used in this Project is Kepler-Labelled-Time-Series-Dataset Provided in Inter-IIT Tech Meet 2017. The dataset Contained Label 2 for Exo-Planet and 1 for Non-ExoPlanet. The labels were changed to 1 and 0 respectively. 

It was Observed that the dataset was Highly Imbalanced. It contained around 99 % Data Points for Non-ExoPlanets and Just 1 % Data Points for Exo-Planets. Hence, the dataset was Split Into Training and Validation Sets, after which the Training Set was Over Sampled Using SMOTE(Synthetic Minority Over Sampling Technique) which doesn't duplicate Minority Class data points rather creates Synthetic Examples Similar to the ones present in the dataset. Since only the Training Set was Over Sampled, there was no risk of Data Leakage into Validation Set.

### Intuition for CNN Architecture

The Project aims at Detecting an Object using a set of points whose values are Light Intensity. This is Similar to Classifying Images which consist of Pixels and Collection of Pixels gives us the image. Finding out spatial relation/pattern among pixels helps us in Classification. Similarly here, finding spatial Pattern between light Intensities treating them as pixels can help us correctly Detect Exo-Planets by taking into consideration the relation different intensities have with each other.

### CNN Architecture Used

Among all the Architectures used for Experimentation, two gave promising Results.They were:-

1.**Customised AlexNet + Dense Layers** :-
