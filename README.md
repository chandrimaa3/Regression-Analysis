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
