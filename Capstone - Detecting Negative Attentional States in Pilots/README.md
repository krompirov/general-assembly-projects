# Detecting negative attentional states in pilots

DATASET:
Please download at: https://www.kaggle.com/c/reducing-commercial-aviation-fatalities/data

Only train.csv is required for this repo.

## Libraries required

biosspy

NeuroKit2

Pywt

tsfresh


## Introduction
In aviation, operational safety is of paramount importance. For any activity in aviation you can think of, there probably exists a safety manual for it. Maintaining the highest levels of safety requires everyone to constantly be at the top of their game. However, it is also a fact that air crew are only human, and sometimes, fatigue and long hours of work could cause unintentional lapses in safety standards. The very unfortunate [2002 Uberlingen mid-air collision](https://www.skybrary.aero/index.php/T154_/_B752,_en-route,_Uberlingen_Germany,_2002) involving 2 aircraft was an example of how a distracted Air Traffic Controller failed to ensure the proper safety standards in maintaining aircraft separation. Pilots, too, are not exempt from such situations. That is why a robust system of having 1-2 extra co-pilots rotating exists, to prevent fatigue from affecting safety standards.

## Problem statement
Most flight-related fatalities can be attributed to a loss of airplane state awareness on the part of the pilot. Pilots who are distracted, sleepy or otherwise in any other undesirable cognitive state risk jeopardizing flight safety. In this project, we will aim to build a classifier that can detect undesirable attentional states of pilots, so that they can be warned when they unaware that they are slipping into these states. This classifier is intended to be operationally functional, in that it should work in real-time and real conditions, rather than something that is used post-hoc to analyze an experiment.

## Secondary goals
We explore 2 different ways of training our models. The first is take a given length of signal, extract scalar features from it, and use those to train a traditional boosted tree classifier. This method requires more pre-processing and domain knowledge on what features to extract and how.

The second is to use the raw signal vectors as inputs to deep learning models. This method requires less pre-processing and domain knowledge about the specific type of signal involved, but is more data-intensive and is reliant on the topology of the deep learning model to get good results.

## Executive summary

This project explored the feasibility of the extracted feature approach and the raw signal approach to training a classifier to detect negative attentional state in pilots.

We trained a Light GBM classifier on extracted features, obtaining a macro AUROC of 0.92, and one-vs-rest (OvR) AUROC for our minority class B and D of 0.81 and 0.95 respectively.

Using our raw signals, we trained a CNN model called the Multivariate LSTM-Fully Convolutional Network, which returned to us a macro AUROC of 0.95, and OvR AUROC of 0.87 and 0.96 for classes B and D respectively.

To extract scalar features for our LGBM classifier, we employed the Discrete Wavelet Transform (DWT) technique to extract approximate and detailed coefficients from our base signal. With these coefficients we were then able to calculate sub-band energy to use as features. In total, we calculated 5 different energy features - 1 total energy of the entire signal, and 4 energy features from 4 of the decomposed sub-bands returned to us by the DWT technique. In addition, we used the cD3 coefficients to reconstruct the signal in the frequency band of 32-64 Hz to be used as additional signal features for training our MLSTM-FCN.

Other CNN models were tested that did not reach the performance of the MLSTM-FCN. These include the MTEX-CNN and the XCM. These did not return strong results, and in fact were unable to get the validation loss to stably converge. While I believe I may not have implemented the architectures exactly right, I feel that the main reason they did not work as well is because the topology of the model was not suited to the size and complexity of our data. It is not an indictment of these models themselves.

In conclusion, it is possible to build workable classifiers using both raw signals and extracted features. For our goal of building a classifier that can function in an operational setting, we recommend the MLSTM-FCN for its superior performance, lightweight topology, and ease of data pre-processing in comparison to the LGBM.

## Data
Data was collected through a series of experiments designed to elicit specific attentional states. These experiments are as follows:

- Channeled Attention (CA)
    - Pilot is asked to focus on a puzzle solving video game
- Distracted Attention (CA)
    - Pilot is asked to do a 'monitoring' task and is periodically disturbed by being asked to quickly a maths question before resuming the monitoring task
- Startled/Surprised (SS)
    - Pilot is asked to watch movie clips with Jump scares. This is possibly the least realistic experiment

From these experiments, we are given 4 attentional states to detect.
- A
    - 'Baseline state' for DA and SS experiments when the event in question is not happening.
    - Somewhat misleading, because the baseline states for DA and SS are not the same
- B
    - Startled/Surprised.
    - Jumpscares
    - 1 or 2 of such events per SS experiment
- C
    - Channeled Attention. This state is constant throughout all CA experiments
- D
    - Distracted Attention. Event where pilot has to quickly switch tasks and complete the distraction task in the DA experiment

Apart from the above 2 features, we are given the following in the dataset:

1. Crew
    - comprised of 2 pilots
2. Seat
    - 0 or 1, denoting which seat the pilot from a given crew is sitting on.

3. ECG
    - 3-lead ECG recording, combined into 1 channel.
    - Not the best representation for an ECG signal
4. 20 separate EEG channels
    - each channel is its own lead, so it is purer than the ECG signal
5. R, respiration
    - measure of rise and fall of the chest
6. GSR, galvanic skin response
    - measure of electrodermal activity.

## Recommendations
In the context of building a classifier to help pilots, these are some  recommendations for taking this project further.

1. Get measurements under more realistic flight conditions
    - There is genuine concern that the results of this project cannot be generalized to actual attentional state monitoring during flight because none of the experiments approximate events that occur during real flying.


2. Choose more relevant attentional states to learn
    - Like discussed elsewhere in the project, the attentional state of Startled/Surprised is not a very useful state to predict. This state is already very visceral by nature, and it is almost impossible that pilots will be unaware of being startled.
    - In contrast, it may be more beneficial to measure a state like drowsiness or daydreaming, whereby a pilot slips into a disengaged state unintentionally. Such states regularly occur in drivers engaged in long-distance trips, like with truckers for example, and a state like this is significantly more detrimental to operational safety.


3. Create a classifier for each individual pilot
    - Biomedical signals are highly variable from individual to individual. Training on one pilot's readings in order to build a classifier to classify attentional states in other pilots is akin to building a housing price prediction model by training on Singapore housing data and using it to predict New York house prices.

## References

Amin, Hafeez Ullah, et al. "Feature extraction and classification for EEG signals using wavelet transform and machine learning techniques." Australasian physical & engineering sciences in medicine 38.1 (2015): 139-149.

Amin, Hafeez Ullah, et al. "Classification of EEG signals based on pattern recognition approach." Frontiers in computational neuroscience 11 (2017): 103.

Assaf, Roy, et al. "MTEX-CNN: Multivariate Time Series EXplanations for Predictions with Convolutional Neural Networks." 2019 IEEE International Conference on Data Mining (ICDM). IEEE, 2019.

Boonyakitanont, Poomipat, et al. "A review of feature extraction and performance evaluation in epileptic seizure detection using EEG." Biomedical Signal Processing and Control 57 (2020): 101702.

Fauvel, Kevin, et al. "XCM: An Explainable Convolutional Neural Network for Multivariate Time Series Classification." arXiv preprint arXiv:2009.04796 (2020).

Karim, Fazle, et al. "Multivariate LSTM-FCNs for time series classification." Neural Networks 116 (2019): 237-245.

Subasi, Abdulhamit. "EEG signal classification using wavelet feature extraction and a mixture of expert model." Expert Systems with Applications 32.4 (2007): 1084-1093.
