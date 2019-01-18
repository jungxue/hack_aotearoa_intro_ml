### Questions

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






Not just mean, need SD, could split the time variable in smaller chunks (window the data)

Imputation, what to do with imputation, mean value imply average patient thing are missing at random ( no it is more likely to be missing systematically)

maybe find neigest neighbour,
Encode the missing ness, add missing ness variable and impute for it

We scaled all paremeters, we have values between 0 to 1, 
Variable in different scales need to be adjusted so everything sort of have same weight in terms of numbers
We need to minimising Euclidean distance, so each value able is normalised for the computation, other wie variables with bigger values will influence more 

Higher AUC, better sensitivity/specitivity ratio

### Other notes
