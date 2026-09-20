**Project.4. Statistical Analysis: A/B Testing**

**Project Overview**
Apply statistical hypothesis testing to validate A/B test results and perform customer
segmentation using clustering techniques. This project bridges statistics and actionable
business decisions.

**Learning Objectives**
 Design and analyze A/B tests using statistical rigor
 Perform hypothesis testing (t-tests, chi-square, etc.)
 Interpret p-values and confidence intervals correctly
 Segment customers using clustering algorithms
 Visualize segments and derive business strategies
 Document assumptions and statistical limitations


**Dataset Information**

**Dataset Link:**
 A/B Test Data: Kaggle - A/B Testing Dataset

**A/B Test Columns:**
 User ID, Group (Control/Treatment), Conversion (0/1), Timestamp


**Step-by-Step Guidance**

**Phase 1: A/B Test Setup & Exploration (2-3 hours)**
1. Load and inspect test data.
2. Check sample sizes.
3. Verify randomization (balance between groups)
   
**Phase 2: Hypothesis Testing (3-4 hours)**

1. Two-Sample T-Test (Continuous Metric - e.g., Average Order Value)
control_revenue = data[data['variant'] == 'Control']['revenue']
treatment_revenue = data[data['variant'] == 'Treatment']['revenue']
t_stat, p_value = stats.ttest_ind(control_revenue, treatment_revenue)
print(f"t-statistic: {t_stat:.4f}, p-value: {p_value:.4f}")
if p_value < 0.05:
print("Statistically significant difference at 95% confidence")
else:
print("No significant difference detected")

3. Chi-Square Test (Categorical - e.g., Conversion Rate)
contingency_table = pd.crosstab(data['variant'], data['conversion'])
chi2, p_value, dof, expected = stats.chi2_contingency(contingency_table)
print(f"Chi-square statistic: {chi2:.4f}, p-value: {p_value:.4f}")
Calculate conversion rates
control_cr = data[data['variant'] == 'Control']['conversion'].mean()
treatment_cr = data[data['variant'] == 'Treatment']['conversion'].mean()
print(f"Control CR: {control_cr:.2%}, Treatment CR: {treatment_cr:.2%}")

5. Calculate Confidence Intervals
from scipy.stats import t as t_dist
n_control = len(control_revenue)
mean_control = control_revenue.mean()
std_control = control_revenue.std()
se_control = std_control / np.sqrt(n_control)
ci = t_dist.interval(0.95, n_control-1, loc=mean_control, scale=se_control)
print(f"95% CI for Control: [{ci[0]:.2f}, {ci[1]:.2f}]")


7. Effect Size (Practical Significance)
Cohen's d for t-test
pooled_std = np.sqrt((std_control**2 + treatment_revenue.std()**2) / 2)
cohens_d = (treatment_revenue.mean() - control_revenue.mean()) / pooled_std
print(f"Cohen's d: {cohens_d:.4f}")
d > 0.2 is small effect, > 0.5 is medium, > 0.8 is large


**Deliverables**
 Jupyter notebook with A/B test analysis and segmentation
 Statistical summary: test statistics, p-values, effect sizes, confidence intervals
 Business recommendations based on findings

**Tools & Libraries**
Python, Pandas, NumPy, SciPy, Matplotlib, Seaborn
