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

#### Over-Sampling

It was Observed that the dataset was Highly Imbalanced. It contained around 99 % Data Points for Non-ExoPlanets and Just 1 % Data Points for Exo-Planets. Hence, the dataset was Split Into Training and Validation Sets, after which the Training Set was Over Sampled Using SMOTE(Synthetic Minority Over Sampling Technique) which doesn't duplicate Minority Class data points rather creates Synthetic Examples Similar to the ones present in the dataset. Since only the Training Set was Over Sampled, there was no risk of Data Leakage into Validation Set.

### Intuition for CNN Architecture

The Project aims at Detecting an Object using a set of points whose values are Light Intensities. This is Similar to Classifying Images which consist of Pixels and Collection of Pixels gives us the image. Finding out spatial relation/pattern among pixels helps us in Classification. Similarly here, finding spatial Pattern between light Intensities treating them as pixels can help us correctly Detect Exo-Planets by taking into consideration the relation different intensities have with each other.

### CNN Architecture Used

Among all the Architectures used for Experimentation, the most promising results were obtained from the following:-

**1. Customised AlexNet + Dense Layers** :- The results Obtained from this architecture were as follows -

| Label                 | Precision         | Recall            | f1-Score          |
| -------------         |:-----------------:|:-----------------:|:-----------------:|
| 0(Non-ExoPlanet)      | 1.00              | 0.97              | 0.98              |
| 1(Exo-Planet)         | 0.21              | 1.00              | 0.34              |

**Confusion Matrix**

| Label                 | 0(Non-ExoPlanets) | 1(Exo-Planet)    |
| -------------         |:-----------------:|:-----------------:
| 0(Non-ExoPlanets)     | 546               | 19               |
| 1(Exo-Planet)         | 0                 | 5                |

**Take Away**

The test Set had 565 Non-ExoPlanets and 5 Exo-Planets. Still, the above model identified all Exo-Planets Correctly without Mis-Classification. Out of 565 Non-ExoPlanets it identified 546 Correctly. Hence, we can conclude that the above model succeeds in correctly identifying Exo-Planets, although there is error in classifying Non-ExoPlanets.

**2. Multi-Channel CNN** :-

**Intuition** :- Usually in Object Detection Tasks where Features of a good number of Negative samples match with features of Positive samples, classifiers fail to create a bias and we end up with high False Positives. To prevent this, we need to Build an architecture which can Identify Different Features of Positive Examples Separately and then combine all the features to differentiate it from Negative Examples. 

Using a Multi-Channel CNN helps here. In the first Channel, a filter of length 2001 has been used to Identify Global Features, i.e Overall Shape of Transits. In the Second Channel a filter of Length 201 has been used to Identify Local Features of Transits , i.e to make sure they are in accurate transit shape and are not Noises arising from Other Phenomenon. Finally both these Features are combined to make a prediction.

The results are as Follows -


| Label                 | Precision         | Recall            | f1-Score          |
| -------------         |:-----------------:|:-----------------:|:-----------------:|
| 0(Non-ExoPlanet)      | 1.00              | 1.00              | 1.00              |
| 1(Exo-Planet)         | 1.00              | 0.60              | 0.75              |

**Confusion Matrix**

| Label                 | 0(Non-ExoPlanets) | 1(Exo-Planet)    |
| -------------         |:-----------------:|:-----------------:
| 0(Non-ExoPlanets)     | 565               | 0                |
| 1(Exo-Planet)         | 2                 | 3                |

**Take Away**

The test Set had 565 Non-ExoPlanets and 5 Exo-Planets. The  above model identified all Non-ExoPlanets Correctly without Mis-Classification. Out of 5 ExoPlanets it identified 3 Correctly. Hence, we can conclude that the above model succeeds in correctly identifying Non-ExoPlanets, although there is error in classifying Exo-Planets.

## Conclusion

The First Model is Good at Detecting Exo-Planets at Cost of Non-ExoPlanets. The Second Model Detects Non-ExoPlanets Accurately. Hence we can combine the two models together to make a reasonable prediction. When both the models predict something as Exo-Planet/Non-ExoPlanet, we can be fairly sure of our Prediction(Since Models with opposite bias agree on a prediction).
