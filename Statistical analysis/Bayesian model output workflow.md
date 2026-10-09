## Bayesian model predictions — `brms` + `tidybayes`

This template extracts posterior expected predictions from a fitted `brms` model using `epred_draws()`. It is useful when you want to retain the posterior draws so that you can calculate custom summaries, credible intervals, contrasts, or other quantities later.
### The general logic

```text
fitted brms model
       ↓
choose prediction scenarios
       ↓
     newdata
       ↓
   epred_draws()
       ↓
posterior predictions
       ↓
summarise posterior
       ↓
median + 95% credible interval
       ↓
       plot
```

The most important habit is: **decide what prediction scenarios you want first, then construct `newdata` to represent those scenarios.** The rest of the workflow can usually stay almost identical across models.

## Quick reusable version

When you just need the standard workflow, this is the compact version:

```r
newdata <- expand_grid(
  variable_of_interest = seq(min(data$variable_of_interest),
                             max(data$variable_of_interest),
                             length.out = 20),
  second_predictor = c(
    round(quantile(data$second_predictor, 0.25), 2),
    round(quantile(data$second_predictor, 0.50), 2),
    round(quantile(data$second_predictor, 0.75), 2)
  ),
  third_predictor = mean(data$third_predictor),
  fourth_predictor = round(mean(data$fourth_predictor))
)

tidy_pred <- fitted_model %>%
  epred_draws(newdata = newdata, re_formula = NA)

pred_summary <- tidy_pred %>%
  group_by(variable_of_interest, second_predictor) %>%
  summarise(
    median = median(.epred),
    lower = quantile(.epred, 0.025),
    upper = quantile(.epred, 0.975),
    .groups = "drop"
  )
```

## Step-by-step
### 1. Create a prediction grid

Choose the values of the predictors for which predictions are required.

```r
newdata <- expand_grid(
  variable_of_interest = seq(
    min(data$variable_of_interest),
    max(data$variable_of_interest),
    length.out = 20
  ),
  second_predictor = c(
    round(quantile(data$second_predictor, 0.25), 2),
    round(quantile(data$second_predictor, 0.50), 2),
    round(quantile(data$second_predictor, 0.75), 2)
  ),
  third_predictor = mean(data$third_predictor),
  fourth_predictor = round(mean(data$fourth_predictor))
)
```

**What this does:** creates all combinations of the predictor values you want to make predictions for.

For a continuous predictor, you might use `seq()` to generate a smooth range of values. For another predictor, you might use representative values such as the 25th, 50th, and 75th percentiles. Other predictors can be held constant, usually at their mean or another scientifically meaningful value.

---

### 2. Extract posterior expected predictions

```r
tidy_pred <- fitted_model %>%
  epred_draws(
    newdata = newdata,
    re_formula = NA
  )
```

`epred_draws()` retains the posterior draws for the expected response rather than immediately reducing them to a single estimate.

`re_formula = NA` gives population-level predictions by excluding the model's random effects. If predictions for particular groups/subjects are required, this can be changed.

---

### 3. Summarise the posterior predictions

```r
pred_summary <- tidy_pred %>%
  group_by(variable_of_interest, second_predictor) %>%
  summarise(
    median = median(.epred),
    lower = quantile(.epred, 0.025),
    upper = quantile(.epred, 0.975),
    .groups = "drop"
  )
```

This produces:

- `median` = posterior median predicted value
    
- `lower` = lower bound of the 95% credible interval
    
- `upper` = upper bound of the 95% credible interval
    

**Important:** include every predictor that you want to keep separate in `group_by()`. If you vary a predictor in `newdata` but don't include it here, its posterior predictions will be combined when the summary is calculated.

---

### 4. Optional: add labels or identifiers

If the predictions are going into a larger figure or being combined with predictions from other models, you can add an identifier here.

```r
pred_summary <- pred_summary %>%
  mutate(
    model = "Model name",
    prediction_type = "Description"
  )
```

---
### 5. If you want to compare predictions directly

Because `epred_draws()` retains the posterior draws, you can calculate differences between conditions rather than just plotting the predictions.

For example:

```r
tidy_pred %>%
  group_by(.draw) %>%
  summarise(
    difference = .epred[condition == "A"] -
                 .epred[condition == "B"]
  )
```

I can then summarise `difference` in exactly the same way:

```r
summarise(
  median = median(difference),
  lower = quantile(difference, 0.025),
  upper = quantile(difference, 0.975)
)
```

This is one of the main advantages of retaining the posterior draws rather than using `fitted()` and immediately discarding them.

---

This code can be used in conjunction with [[Violin + pointrange plot]] for the complete model to plot workflow.

---
This template explainer page was created by ChatGPT based on code written by me, and then it was edited by me.