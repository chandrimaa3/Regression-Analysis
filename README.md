# Regression-Analysis
## 1. Load the dataset
```{r}
data = read.csv("C:/Users/chand/Downloads/MLr data - Sheet1.csv")
attach(data)
```

## 2. Model selection
```{r}
# Forward Selection
fitstart = lm(y ~ 1, data)  
fitall = lm(y~.,data)
fwd = step(fitstart, direction = "forward",scope = formula(fitall))
summary(fwd)
AIC(fwd)
??AIC
# Backward Elimination
back = step(fitall, direction = "backward")
summary(back)
AIC(back)
```

### *Interpretation:*
Comparing the AIC values of the two models selected by the forward selection and backward elimination, we will select the model selected by backward elimination because of its less AIC value.

## *The Final Model*
```{r}
model = lm(y ~ x1 + x3 + x4 + x7, data = data)
summary(model)
```

# 3. Residuals
```{r}
plot(model)
abline(model)

# Residuals
res = residuals(model);res
dii = rstudent(model)
```

# 4. Residuals Analysis 
```{r}
library(lmtest)
# Check For Nomality
shapiro.test(dii)
```

### *Interpretation:*
Since p-value > 0.05, we will accept the null hypothesis, which means the errors are normally distributed.

```{r}
# Check For Heteroscedasticity
bptest(model)
```

### *Interpretation:*
Since p-value > 0.05, we will accept the null hypothesis, which means there's no heteroscedasticity among the errors.

```{r}
# Check for Autocorrelation
dwtest(model)
acf(res)
```

### *Interpretation:*
Since p-value > 0.05, we will accept the null hypothesis, which means there's no autocorrelation among the errors.

# 5. Check For Multicollinearity
```{r}
library(car)
vif(model)
```

### *Interpretation:*
Since the VIF are less than 5, there's no multicollinearity present in the dataset.

# 6. Check for Outliers
```{r}
boxplot(x1,x3,x4,x7)
# Standardized Residuals
std_res = rstandard(model)
outliers = which(abs(std_res) > 3);outliers
```

### *Interpretation:*
There's no outlier observed in the data.
