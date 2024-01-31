# Quantum Chemistry of Organic Molecules Analysis with Python

Analysis of quantum chemistry data in Organic Chemistry from the published research article in Chemical
Physics, [Himmetoglu, J. Chem. Phys, 2016](https://pubmed.ncbi.nlm.nih.gov/27782427/) using machine learning models, Python, and Google Colab contribution as part of a team. Final project for the FAU course PHY 6938.

## Our Task
The purpose is to analyze molecular data from 𝑁 = 16,242 training observations to understand the fundamentals for the regression neural network algorithm.

The goal is to fit a model that can predict ground state energies of molecules made up of six atoms: C, H, N, O, P, and S, based on 𝑝 = 1,275 feature vectors.

To be specific, a given molecule in the dataset, for a total of 16,242 molecules, numbered with an index is represented by a p-dimensional feature vector xi where p is the total number of unique entries in the Coulomb matrix (for instance, the upper triangular part of the symmetric 50x50 matrix Cij, unrolled in into a 1,275-dimensional vector) or the number of eigenvalues (for example, a 50-dimensional vector of eigen values) (Himmentogu, B., 2016). 

The unfolded vectors from the Coulomb matrices were used in this analysis. In terms of machine learning algorithms, I performed a penalized (regularized) least squares fit of a linear model using ridge regression, with the model parameters obtained by batch gradient descent was performed. The tuning parameters were chosen using five-fold cross validation, and the best-fit model parameters was inferred on the training dataset conditional on an optimal tuning parameter, which is similar to the approach described by the author on the research article.

## Dataset
Data for these observations are given in the attached roboBohr.csv file, with atoms of each molecule labeled on each row (rows 2 through 16,243), and input features and response given on the columns (with the first row representing a header for each column). There are six quantitative features, given by columns labeled “0”, ‘1”, “2”, “3”, “4” ...”1274”

## Effect of tunning parameter on inferred regression coefficients.
A discrete grid of seven tuning parameter values 𝜆∈ {10-2 ,10-1 ,100 ,101 ,102 ,103 ,104} was considered where the tuning parameter is evaluated across a wide range of values on a log scale. For each tuning parameter value, gradient descent was used to infer the best-fit model.

## Methodology
* Step 1: 
Creating a plot showing the effect of the tuning parameter on the inferred ridge regression coefficients of 1,275 lines (one for each of the 𝑝 = 1,275 features), with the 𝑦-axis as 𝐵j,j = 1,2, ... ,1275, and the 𝑥-axis the corresponding log-scaled tuning parameter value log10 (𝜆) that generated the particular 𝐵j. 

* Step 2: 
Creating a plot showing the effect of the tuning parameter on the cross-validation error with the 𝑦-axis as CV error, and the 𝑥- axis the corresponding log-scaled tuning parameter value log10(𝜆) that generated the particular CV(5) error. 

* Step 3: Highlighting the 𝜆 value that generated the smallest CV(5) error.

* Step 4: 
Retraining the model on the entire dataset of 𝑁 = 16,242 observations and providing the estimates of the 𝑝 = 1,275 best-fit model parameters using the optimal 𝜆. 

## Final Analysis 

### Insight 1
The model described above seems to work for this data because the plot generated on step 2 shows the expected behavior of a curvature where, as the tuning parameter lambda increases, the CV error decreases. The tuning parameter lambda that produces the lowest CV error is 1000 for this dataset. The model score using the entire dataset suggests the trained model can make accurate predictions approximately 95.6% of the times.

### Insight 2
The second value for ‘ridge_regressor.best_score_’ is the main cross-validated score of the best_estimator. The mean
can be positive or negative. This served as an additional metric to describe the best predictor. Maybe displaying the mean square error may be more informative. It could be a good approach to compare these results with those to be obtained without using statistical or ML libraries and provide a discussion as to why the results are different if applicable.

For future and, to optimize the model, it could be good approach and/or suggestion to perform a penalized (regularized) least-squares fit of a linear model using elastic net, with the model parameters obtained by coordinate descent.


