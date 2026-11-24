# econ3916-lab19-random-forests

# Tree-Based Models: Random Forests

## Objective
I compared a single decision tree, linear models and a random forest on California Housing, looked at which features the forest relies on, and tuned the forest by cross-validation.

## Methodology
* Split California Housing into training and test rows and fit four models on the same training rows: a single decision tree with no depth limit, OLS, Ridge and a random forest.
* Scored each model on both the training and test rows using RMSE and R².
* Checked the forest's out-of-bag score against its test score, and checked how many leaves the unlimited tree grew.
* Measured feature importance two ways for the forest: impurity-based (MDI) and permutation importance on the test rows.
* Tuned the forest with `GridSearchCV`, trying different values of `max_depth` and `max_features`, and scored the best forest on the test rows.
* Wrote my own prompt asking an AI for a function that draws a feature-importance chart and returns the numbers as a table. I checked it against my permutation importance results and stopped after two rounds.

## Key Findings
* The single tree reached a test R² of 0.6228, Ridge reached 0.5758, and the random forest reached 0.8046. The tree grew almost one leaf per training row, so it memorized the training data and did worse on new rows. The forest beat Ridge with the same features, which tells me the link between the features and house values is nonlinear.
* MDI and permutation importance disagreed on some features. Latitude scored 0.0890 by MDI but 0.4427 by permutation. MDI also ranked AveOccup higher than permutation did. I trust permutation importance more because it is measured on test rows.
* Removing the depth limit mattered more than `max_features` in the grid. The tuned forest differed from my first forest only in `max_features`, and its test R² was 0.8094, a small gain over 0.8046.
* My prompt took two rounds. Round 1 matched my numbers on every line of the check. In round 2 I added one choice my prompt had left out, the chart title showing the actual number of features, and the check still said yes on every line. I also compared the function's `permutation_importance` call with my own, setting by setting, and they matched.
