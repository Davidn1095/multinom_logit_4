# multinom_logit_4

### Loading the MASS Package and Preparing Data:

- `library(MASS)`: Loads the MASS package, which contains functions for statistical methods, including ordinal logistic regression.
- `Chapman.Cuali$Presion <- factor(...)`: Converts the `Presion` column in the `Chapman.Cuali` DataFrame to a factor with defined levels ("Optima", "Normal", "Alta", "Descompensada"). These levels are likely ordered.
- `Chapman.Cuali$IMC <- factor(...)`: Converts the `IMC` (Body Mass Index) column in the `Chapman.Cuali` DataFrame to a factor with defined levels ("Normal", "Sobrepeso", "Obesidad").

### Fitting an Ordinal Logistic Regression Model:

- `Ajuste.Ordinal.Cuanti <- polr(Presion ~ Edad + Colesterol, data = Chapman.Cuali)`: Fits an ordinal logistic regression model using the `polr` function. The model predicts `Presion` based on `Edad` (Age) and `Colesterol` (Cholesterol) as predictors.

### Model Summary and Coefficients:

- `summary(Ajuste.Ordinal.Cuanti)`: Provides a summary of the fitted ordinal logistic regression model, including coefficients and their statistical significance.
- `summary(Ajuste.Ordinal.Cuanti)$coefficients`: Extracts the coefficients from the model summary.

### Statistical Significance of Coefficients:

- `2 * pnorm(abs(summary(Ajuste.Ordinal.Cuanti)$coefficients[,"t value"]), lower.tail = F)`: Calculates the two-tailed p-values for the coefficients based on their t-values to assess their statistical significance.

### Interpreting Coefficients:

- `exp(-summary(Ajuste.Ordinal.Cuanti)$coefficients[c("Edad", "Colesterol"), "Value"])`: Exponentiates the negative coefficients for `Edad` and `Colesterol` to interpret them in the context of the ordinal logistic model.
- `exp(summary(Ajuste.Ordinal.Cuanti)$coefficients[c("Optima|Normal", "Normal|Alta", "Alta|Descompensada"), "Value"])`: Exponentiates the coefficients for threshold levels to understand the changes in odds for moving from one category to the next.

### Confidence Intervals:

- `confint.default(Ajuste.Ordinal.Cuanti)`: Calculates the confidence intervals for the model parameters.

### Predictions from the Model:

- `predict(Ajuste.Ordinal.Cuanti, type = "probs")[1:10,]`: Predicts the probabilities of each category for the first 10 observations.
- `predict(Ajuste.Ordinal.Cuanti, type = "class")[1:10]`: Predicts the class (category of `Presion`) for the first 10 observations.

### Evaluating Model Predictions:

- `table(Chapman.Cuali$Presion, predict(Ajuste.Ordinal.Cuanti, type = "class"))`: Creates a contingency table to compare the actual `Presion` categories with the predicted ones.

### Model Deviance and Statistical Testing:

- `Ajuste.Ordinal.Cuanti$deviance`: Retrieves the deviance of the fitted model, which is a measure of goodness of fit.
- `pchisq(Ajuste.Ordinal.Cuanti$deviance, 595, lower.tail = F)`: Calculates the p-value for the deviance statistic, testing the overall significance of the model. The `595` likely represents the degrees of freedom.


