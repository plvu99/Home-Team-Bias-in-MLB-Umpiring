# ️⚾ Home-Team Bias in MLB Umpiring

## Background and Context

Baseball is a sport where the umpire’s role is pivotal, and their calls directly influence the fairness and outcome of each game. An article by the Society for American Baseball Research (SABR) reports that even top-performing umpires miss 12–13 calls per game, though accuracy has improved since Major League Baseball (MLB) introduced performance evaluation systems in 2009. A Boston University study analyzed over 4 million pitches across 11 MLB seasons and found that certain incorrect calls occurred more than 20% of the time, particularly in high-pressure situations.

It is not uncommon that fans blame the loss of the game to home advantages and umpire biases. Psychologist research shows that umpire biases exist and even extensive training cannot eliminate such biases, but how they benefit or harm the teams remain unknown. Some studies argue umpire bias relates more to player race, while others suggest it directly influences team performance outcomes. Some research equate home advantages and umpire biases; however, home bias is not entirely explained by umpire, nor is it attributable to umpiring inconsistencies (Hsu, 2023). Given that, our project tends to close the gap between whether or not there is a significant home bias among umpires and how it impacts the outcomes.

## Research Question

Is there significant home-team bias among MLB umpiring? (favor_home and total_run_impact)

## Objectives and Scope

Our project seeks to examine the existence of home-team bias in MLB umpiring decisions and to quantify how such bias may affect the game outcome through measures like favor_home and total_run_impact. Understanding umpire bias is critical for maintaining the integrity of the sport, shaping fan perception, and potentially informing team strategies for home and away games.

## Methodology

### Dataset Description

Our dataset was collected through [Kaggle](https://www.kaggle.com/datasets/mattop/mlb-baseball-umpire-scorecards-2015-2022) and originally sourced from Umpire Scoreboards, an online platform dedicated to measuring the accuracy, consistency, and favor of MLB umpires. It includes umpire scorecard data of each game for the 2015 - 2022 MLB seasons. For each game, there are 18 columns in total, including umpire, home, away, favor_home, total_run_impact, etc.

This study focused on two columns: favor_home and total_run_impact. The **favor_home** column represents the difference between the home team's and the away team's run expectancy impacts for a given game. Meanwhile, the **total_run_impact** column represents the sum of the favor of every missed call. In addition, we examined the relationship between incorrect_calls, accuracy, consistency, umpire, home, away and favor_home and total_run_impact to see if either of these factors potentially correlate with game outcomes.

### Data Preprocessing

We began by cleaning the data: removing rows with missing values and converting key columns to numeric format, such as home and away team runs, pitches called, incorrect calls, and important metrics like accuracy, consistency, favor_home, and total_run_impact.

### Models and Evaluation Metrics

This study applied both supervised and unsupervised learning techniques to analyze potential home-team bias among MLB umpires, focusing on favor_home and total_run_impact as primary indicators.

For **supervised learning**, we used Regression to predict the impact of incorrect calls on total run expectancy, and Classification to determine whether an umpire’s calls favor the home team. Four models were adopted as follows:

- **Simple Linear Regression** examined the relationship between incorrect_calls and favor_home and total_run_impact. This model intended to reveal if incorrect calls are directly favoring the home team and to what degree.

- **Multiple Linear Regression** extended the model by adding accuracy and interaction terms with below_expected flags to improve predictive performance.

  - R-squared and Root Mean Squared Error (RMSE) evaluated the goodness of fit for the linear regressions.

  - Validation Set Approach (Train/Test Split) measured the model accuracy and fitness as well as the generalization ability of simple and multiple linear regressions.

  - 5-Fold Cross-Validation provided a robust estimate of model stability by averaging RMSE across folds.

- **Logistic Regression** classified games based on whether total_run_impact is above or below the median, providing a binary view of bias.

- **Decision Tree Classification** further modeled the categorical outcomes by including additional features such as umpire ID, home team, and away team, allowing nonlinear splits and feature interactions to be captured.

  - Accuracy was used to assess the performance of two classification models.

On the **unsupervised** side, we used two methods: K-Means and Hierarchical Clustering. This allowed us to define clear umpire clusters based on bias and performance metrics.

- **K-Means Clustering** was applied to favor_home and total_run_impact to identify groups of umpires who systematically favor home teams, away teams, or remain neutral.

  - Inertia and the Elbow Method were used to select the optimal number of clusters.

  - Silhouette Scores measure how well the clusters were separated.

  - Chi-Square Tests were conducted to test the statistical significance of differences between home-team bias and away-team bias clusters.

- **Hierarchical Clustering** was additionally conducted on favor_home, total_run_impact, accuracy, and consistency to explore natural divisions among umpires based on bias and performance levels.

  - Dendrograms and Merge Heights Plots were used to determine the number of meaningful clusters in hierarchical clustering.

## Results & Discussion

### Regression

The result shows that there is almost no relationship between incorrect calls and how much the umpire favors the home team compared to the away team. Even after adding accuracy, consistency, and other supplementary variables, all predictors remained insignificant, and the model's R-square remained at 0.000. These results suggest no significant relationship between an umpire’s missed calls — including potentially intentional ones — and directly favoring the home team over the away team in terms of run expectancy.

However, when adding accuracy as one of the variables in modeling total_run_impact, accuracy actually is significant and increase in accuracy leads to a higher total_run_impact. This means that for umpires who have a higher accuracy rate, each incorrect call has a larger effect on the total_run_impact compared to umpires who have a low accuracy rate.

To further examine if different umpires have different biases on a specific home team, the data was grouped by umpire and home team and incorrect_calls and total_run_impact were calculated on mean. However, even after grouping by home team and umpire, the relationship between favor_home and incorrect calls remains weak. This may be due to limited repetitions of specific umpire-team pairings, making individual umpire preferences difficult to detect.

### Classification

The coefficient seems not significant, suggesting that an increase in incorrect calls may not actually increase the chance that the umpire is favoring home. After several other factors similar to multiple linear regressions were incorporated, no significant parameters stood out. The average cross validation score is around 0.515 and the accuracy is around 0.516, together with the confusion matrix. This indicates that using the number of incorrect calls to conclude whether or not the umpire is favoring the home team is basically no better than random guessing.

Because the combinations of umpire, home team, and away team are almost all unique, the decision tree shows that while the number of incorrect calls is a primary factor for splitting, the tree spreads too widely as other factors lack repetition.

Reviewing prior studies suggests that home bias among umpire calls does exist, particularly when the home team is batting, and that the type of incorrect call also plays a significant role. Simply examining the number of incorrect calls may blur these effects, as it mixes calls made while the home team and away team are batting, potentially evening out the observed bias. To improve accuracy, future studies should use datasets that specify the home team, batting team, and types of incorrect calls. Nevertheless, it remains important to recognize that each incorrect call increases total run impact, meaning no incorrect call is truly neutral. In practice, teams batting as the away team must be especially mindful of the potential disadvantage introduced by such biases.

### K-Means Clustering

Cluster 0, labeled “Neutral,” included 10,577 umpires (58.46%) who demonstrated no strong preference for either the home or away team. The favor_home scores for these umpires were close to zero, indicating a relatively neutral stance.

Cluster 1, “Away Team Bias,” comprised 3,617 umpires (19.99%) who favored the away team, as evidenced by a negative favor_home score and a higher total_run_impact score, suggesting that their calls were more likely to favor the visiting team’s chances.

Cluster 2, “Home Team Bias,” contained 3,899 umpires (21.55%) who favored the home team. These umpires had positive favor_home scores and higher total_run_impact values, indicating that their calls influenced the home team’s scoring more significantly.

The distribution of umpires across the clusters shows that most umpires (58.46%) are neutral, but there is still a substantial proportion who display some level of bias. Interestingly, the Home Team Bias cluster (Cluster 2) had more umpires than the Away Team Bias cluster (Cluster 1), suggesting that home team bias might be more prevalent than away team bias among MLB umpires. 

In terms of fairness, these results could have important implications for the sport. If certain umpires consistently favor the home team, this could lead to potential fairness concerns, particularly in close games where decisions might influence the final outcome. This raises questions about how to address this issue, whether through more thorough training for umpires to recognize and correct bias, or through the introduction of more technological tools, such as automated strike zones, to reduce human error.

### Hierarchical Clustering

The merge heights drop dramatically after the first few merges, then flatten. After that, there's very little distance between clusters. Based on these graphs, we identified 2-3 meaningful clusters. Given the dataset of over 18,000 games, 3 clusters seem better to capture importance differences. Beyond three, any additional clusters are very close together (small differences).

Cluster 1 umpires have the highest accuracy (94.59) and consistency (94.44) with low total_run_impact (0.976) and mild home-team favoring (0.126), suggesting strong performance and neutrality. Cluster 2 umpires show a slight away-team bias (-0.583) with moderate run impact (1.743) and lower accuracy (91.67) compared to Cluster 1. Cluster 3 umpires demonstrate stronger home-team bias (0.37), the highest run impact (2.127), and the lowest accuracy (90.04), indicating more biased and inconsistent decision-making. Overall, the table reinforces that the clusters meaningfully capture differences in umpire bias and performance. 

From a business perspective, these findings suggest actionable steps. Cluster 1 umpires could be prioritized for high-stakes games to ensure fairness. Cluster 3 umpires may need additional monitoring or retraining. Overall, clustering provides a way to support more transparent and data-driven officiating.

However, our analysis has some limitations. Hierarchical clustering is sensitive to outliers and depends heavily on a few variables. The results may also change depending on the linkage method we choose — for example, Ward vs single linkage. Lastly, it’s worth noting that hierarchical clustering is computationally heavy, especially with large datasets, so it may not scale well in real-time systems.
