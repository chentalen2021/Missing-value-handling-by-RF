# Missing-value-handling-by-RF

Traditionally, the missing values in the dataset are filled by arithmetic mean/ mode. However, this seems too roughly to compute the missing data since it ignores the difference among the samples with missing values. A more accurate method for handling the missing values is using Random Forest (RF) which is proposed by Fei Tang and Ishwaran (2017). The RF computes the missing data considering their corresponding samples' uniqueness located by both their class labels and the correlation with other samples in the same class.\
\
Using RF for compute the missing data, you need to do the following steps:\
\
Step1, make an initial guess of the missing data in the dataset with arithmetic mean/ mode.\
\
Step2, using the dataset to build a RF.\
\
Step3, apply the data samples into the RF and get the leaf indices they belong to.\
\
Step4, initiate a proximity matrix with the shape of num_samples * num_samples (the total number of samples in the dataset) and the values of 0.\
\
Step5, compare the samples' leaf indices pair by pair through all the samples. If there are two samples (e.g., the i-th sample and the j-th sample) are in the same leaf, update the proximity matrix by add 1 to the position of (i, j) and (j, i).\
\
Step6, refine the initial guess (arithmetic mean/ mode) in the dataset with the proximity matrix. The missing data (e.g., male) of categorical type (e.g., gender) of the m-th sample should be refined by weighted frequency W*F. F refers to the frequency of "male" values in the gender column, W refers to the weight of "male" regarding the samples which have the same sex values to the m-th sample.  The missing data (e.g., 23) of numeric type (e.g., age) of the m-th sample should be refined by weighted average V*W. V is the value of the age of the m-th sample.\
\
Repeat step2 ~ 6 until the guess of the missing values do not change.\
\
\
Using this python module, you need to:\
Firstly complete the step1 and 3 by yourself.\
Import this module and use the method Reat_Until_Converge. Pass in the dataset with the initial guess (step1 above), the leaf index of the samples in the RF.\
You will get the new dataset with the guest refined and the error of the missing data to the ones in the last iteration.
