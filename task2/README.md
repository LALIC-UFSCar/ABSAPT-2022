# Sentiment Orientation Extraction

The image below show the pipeline we used to solve task 2. We first used [SpaCy](https://github.com/explosion/spaCy) to help us find the meaningful surroundings; 
we could then input these surroundings into the pre-trained [GoEmotions for the Portuguese model](https://github.com/Luzo0/GoEmotions_portuguese). 
We then generated a polarity for each aspect based on the predictions and scores given by GoEmotions. 
Finally, we assigned polarity 0 to all aspects whose DEP tag in the SpaCy output was labeled as OBL.

<p align="center">
<img src="https://user-images.githubusercontent.com/31036627/176501845-53eb04b4-439b-4185-8abf-55fac9e5ad0b.png" width="700" />
<\p>

## Results in the Training Dataset

We used the training dataset to perform experimentations, using different techniques and approaches for the task, 
and then we compared the results to decide which to apply to the test dataset. The code for the experimentations can be found [here](https://github.com/LALIC-UFSCar/ABSAPT-2022/blob/main/task2/task2_train.ipynb).

In our experiments, we tested:

* inputting the whole aspect sentence versus only the aspect's meaningful surroundings to the GoEmotions model;
* calculating the polarity of the aspect in three different ways: (1) by assigning the value of prediction 1, (2) by selecting the value of the majority of the top-3 predictions, and (3) by combining these two approaches and setting the value of prediction 1 only if it was higher than a threshold;
* setting polarity 0 to all aspects that SpaCy tagged as OBL compared to not doing this post-processing

You can see the Balanced Accuracy Score (bacc) results in the tables bellow.

1. By Aspect Sentence

Model                  | Not Annull OBL Aspects | Annull OBL Aspects
:----------------------|:-----------------------|:--------------------
Prediction 1           | 0.58                   | 0.59
Top 3 without treshold | 0.59                   | 0.61
Top 3 with treshold    | 0.60                   | 0.61

2. By Meaningful Surroundings

Model                  | Not Annull OBL Aspects | Annull OBL Aspects
:----------------------|:-----------------------|:--------------------
Prediction 1           | 0.59                   | 0.59
Top 3 without treshold | 0.62                   | 0.63
Top 3 with treshold    | 0.64                   | 0.63


## Final Results

The approach we chose to send the results of Task 2 was the one we input the meaningful surroundings to the GoEmotions model,
took the top-3 predictions with threshold, and annul the OBL aspects. The code of the model we sent can be found [here](https://github.com/LALIC-UFSCar/ABSAPT-2022/blob/main/task2/task2_test.ipynb).
The table bellow presents the final results obtained.

Dataset | Bacc | F1   | Precision | Recall
:-------|:-----|:-----|:----------|:-------
test    | 0.63 | 0.61 | 0.65      | 0.63

