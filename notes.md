### Questions


1a) Study generate feature vector(df) in the helper.py file. The input to this function is a pd.DataFrame containing the data for a single patient admission. The output is a python dictio- nary object, corresponding to a d-dimensional feature vector for this patient (with missing values). The keys of this dictionary are feature names, and the values are the corresponding feature values. For the time-invariant variables, we use the raw values. We replace unknown observations (−1) with unde- fined (use np.nan), and name these features with the original variable names. For each time-varying variable, we compute the mean of all measurements for that variable.

(i) Read the [documentation](https://physionet.org/challenge/2012//#weight) on the variable ICUType, and reflect on the current feature representation of this variable. **What does such a representation imply, when using a linear classifier? How else might you represent this variable (as possibly more than one feature)?**

ICUType 
- 1: Coronary Care Unit, 
- 2: Cardiac Surgery Recovery Unit,
- 3: Medical ICU, or 
- 4: Surgical ICU

We have levels of 1,2,3, and 4 and this could imply a step relationship ( ie 4 is 4 times as much as 1), even though we are just using the numbers as indicators and not implying any numeral relationships. 

We could change the ICUType variable into 4 variables that contain 0 or 1 (like a dummy or flag variable), converting leveled variable into dummy variables will allow AI to avoid implying numeral relationships bwtween the numbers. 

so instead of a variable like 

```R
ICUType 
[1] 1, 2, 1, 4 , 4, 3, 4
```

We will have 4 variables like

```R
ICUType1
[1] 0 0 1 0 0 0 0 1
ICUType2
[1] 1 0 0 0 0 1 0 0
ICUType3
[1] 0 0 0 1 0 0 0 0
ICUType4
[1] 0 1 0 0 1 0 1 0
```

(ii) **Here we only consider the mean of the numerical variables. What limitations are associated with this representation? What other summary statistics could be useful?**

Well, the word **mean** should be a major trigger if you had done stats, mean doesn't meant anything on its own, you need at least a  Confidence interals(CI) to make mean results meaninful, you could also use standard error(SD). 

We could also split the time variable into smaller time chunks (window the data), to observe the association with time. 

1b) Study impute missing values(X). Given a feature matrix X (where each row corresponds to a patient admission and each column a feature) with missing values, we consider each feature column independently. For each column, we impute the missing values by replacing it with the mean value of the observed values in that column. **What assumptions does this imputation approach make? How else might you handle missing data?**

If we use mean value to replace missing values, we are assuming all missing value are average sample, and this is definitely not true. We need to consider the possibility of missing at random, missing compoletely at random, and missing not at random. 

I personally prefer to just use **resampleing** techniques to repalce missing values, lets say we have a data set of 1000 samples and 20 of the sample had missing variable A , I would use the other 980 sample that have valid variable A values as sample and randomly sample (with replacement) from it to replace the missing values. If we have lots of other variables we could make a model and **impute** for missing values, if the missing values are from a variable that has strong realtionship we could try **K-neareat neighbour** (KNN). 


1c)
Notice that many of these feature values lie on very different scales. To address this, we normalize each feature column xd to have range between 0 and 1. **Why might it be useful to scale the features in this way?**

We scaled all paremeters, so we have result values between 0 to 1, Variable in different scales need to be adjusted so every variable sort of have the same weight in terms of numbers. 

For our algorithm we need to minimising Euclidean distance, if we did not normalise the variables, variables with bigger values will influence the results with a graeter influence comapre to smaller values. 

### Other notes

Lets think absurdity. 

If we are particularly worried about sensitivity or specificity, we could make sensitivity or specificity to 100%, what will happen?

We will ahve a great vlue for one of the measurement, but the other corresponding measure will go all over the place, this is definitely not good. This is why we need to find a balenced measure. ie. Evalurting the sensitivity/specificity trade off and find the optimum solution.


**Receiver operating characteristic** (ROC) curve is a good way to should what will happen to sensitivity/specificity if we change the value for one or another. 


**Area under curve** (AUC or AUROC) is a good measure to evaluate different senitivity/specificity ratios for our models. 
Higher AUC, better sensitivity/specitivity ratio. 


For this particular exercise, the ROC for 2.2b seem to be more jaggered than ROC curve from 2.1d. 

I thought maybe randomness hads something to do with the jaggedness of ROC (ie more randomness will cause greater jaggeredness, if there is no randomness we will have a beautiful smooth curve) but the lecturers doen't seem to be agree, they thought it was due to the difference in intervals that were used. 

So, If Roc curve is smooth, this probabily meant that we are using finer intervals. vise evrsa,
if Roc curve is very jagged, this probabily meant that intervals we use is big. 


