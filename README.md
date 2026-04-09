# **SBA Loan Default Prediction with Logistic Regression**

This project analyzes SBA loan data to predict default risk using logistic regression. The goal is to identify key drivers of default and demonstrate how model decisions should be aligned with business risk, not just default statistical thresholds.

---

## **Project highlights**

* Built a logistic regression model to classify SBA loan defaults
* Performed feature selection using statistical significance (GLM results)
* Reduced model from 5 variables to 3 key predictors
* Evaluated model performance using classification metrics
* Conducted threshold analysis to align predictions with business risk
* Demonstrated real-world decision-making using model outputs

---

## **Business questions**

* Which loan characteristics are most associated with default risk?
* How accurately can we predict loan defaults?
* What tradeoffs exist between detecting defaults and avoiding false alarms?
* How should lenders adjust decision thresholds based on risk tolerance?

---

## **Tools used**

* Python
* pandas
* numpy
* statsmodels (GLM logistic regression)
* scikit-learn
* matplotlib
* Jupyter Notebook

---

## **Repository contents**

```
.
├── sba_loan_default_portfolio.ipynb
├── README.md
├── SBAcase.11.13.17.csv
└── requirements.txt
```

---

## **Key findings**

### **Final model (reduced)**

The final logistic regression model included:

* **RealEstate**
* **Portion**
* **Recession**

Variables **New** and **DisbursementGross** were removed due to lack of statistical significance.

---

### **Model performance (default threshold = 0.50)**

* Accuracy: **67.84%**
* Precision: **68.89%**
* Recall: **8.73%**
* Specificity: **97.99%**
* F1 Score: **0.155**

At the default threshold, the model performs well at identifying safe loans but fails to detect most defaults.

---

## **Threshold analysis (key insight)**

To improve decision-making, multiple probability thresholds were evaluated:

| Threshold | Recall | Specificity | Accuracy |
| --------- | ------ | ----------- | -------- |
| 0.10      | 95.8%  | 37.9%       | 57.5%    |
| 0.30      | 76.3%  | 60.2%       | 65.7%    |
| 0.40      | 75.8%  | 62.5%       | 66.9%    |
| 0.50      | 8.7%   | 97.9%       | 67.8%    |

---

### **Key insight**

* Lowering the threshold dramatically improves **recall (default detection)**
* However, this increases false positives (lower specificity)
* The default 0.50 cutoff is **not appropriate for this problem**

---

### **Recommended threshold**

A threshold of **0.3–0.4** provides the best balance:

* Captures ~76% of defaults
* Maintains reasonable specificity (~60–62%)
* Preserves overall accuracy

---

### **Business interpretation**

In lending, **missing a default is typically more costly than incorrectly flagging a safe loan**.

Using a lower threshold allows lenders to:

* Identify high-risk borrowers more effectively
* Reduce financial losses from defaults
* Accept a manageable increase in false positives

This demonstrates that **model thresholds should be driven by business costs, not default settings**.

---

## **Key drivers of default**

* **RealEstate (negative effect):** Loans backed by real estate are significantly less likely to default
* **Portion (negative effect):** Higher SBA guarantee reduces default risk
* **Recession (positive effect):** Loans issued during recessions are more likely to default

---

## **Scenario analysis**

Example loan predictions:

| Loan              | Default Probability | Decision (0.50 cutoff) |
| ----------------- | ------------------- | ---------------------- |
| Carmichael Realty | 0.0485              | Approve                |
| SV Consulting     | 0.5494              | Deny                   |

---

## **Business application**

This model can be used to:

* Support loan approval decisions
* Identify high-risk borrowers early
* Adjust lending strategies during economic downturns
* Optimize risk thresholds based on financial impact
