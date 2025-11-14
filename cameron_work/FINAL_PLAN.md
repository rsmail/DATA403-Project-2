# FINAL PROJECT PLAN
## DATA 403 Project 2 - Loan Default Prediction

**Team:** Cameron Hafer, Charlie Jansen, Colin Hassett, Rory Smail

---

## 📋 CURRENT STATUS

### ✅ COMPLETED
- [x] Combined pipeline notebook created
- [x] Data loading (application_train, bureau, previous_application)
- [x] Data cleaning (missing indicators, imputation, type coercion)
- [x] Feature engineering (bureau aggregation, previous app counts)
- [x] Three models implemented (Logistic Regression, SVM, LDA)
- [x] Custom metric implementations (ROC-AUC, Accuracy, Precision, F1)
- [x] Basic model evaluation

### ❌ MISSING (Critical for Assignment)
- [ ] Train/Test/Validation splits (random, stratified, non-random)
- [ ] Cross-validation implementation (from scratch)
- [ ] Hyperparameter tuning
- [ ] Fairness analysis (gender, age)
- [ ] Model prediction comparison
- [ ] Threshold optimization (for 85% recall requirement)
- [ ] Feature scaling (to fix convergence issues)

---

## 🎯 PHASE 1: DATA SPLITTING (HIGHEST PRIORITY)

### 1.1 Implement Three Split Strategies
**Assignment Requirement:** "Try, at a minimum: random split, stratified split, non-random split"

**Implementation:**
- **Random Split:** 80% train, 20% validation (random sampling)
- **Stratified Split:** 80% train, 20% validation (stratified by TARGET to maintain class balance)
- **Non-Random Split:** 80% train, 20% validation (temporal split - if date available, or by SK_ID_CURR ranges)

**Deliverable:** Compare validation performance across all three split strategies

### 1.2 Cross-Validation Implementation (From Scratch)
**Assignment Requirement:** "Implement cross-validation from scratch"

**Implementation:**
- Create custom k-fold cross-validation function
- Use numpy/pandas only (no sklearn.cross_validate)
- Apply to all three models
- Report mean/std of metrics across folds

---

## 🎯 PHASE 2: MODEL OPTIMIZATION

### 2.1 Feature Scaling
**Issue:** Convergence warning, poor SVM performance
- Scale all features before training (StandardScaler)
- Apply to all three models

### 2.2 Hyperparameter Tuning
**Assignment Requirement:** "Decide what values of hyperparameters to use"

**For Each Model:**
- **Logistic Regression:** C (regularization), penalty (L1/L2), solver
- **SVM:** C, kernel (linear for comparison), gamma
- **LDA:** solver, shrinkage

**Method:** Grid search or manual tuning with cross-validation

### 2.3 Class Imbalance Handling
**Issue:** Models predicting majority class (92% class 0)
**Options:**
- Class weighting (`class_weight='balanced'`)
- Threshold optimization (see 2.4)
- SMOTE/undersampling (if time permits)

### 2.4 Threshold Optimization
**Proposal Requirement:** "85% recall requirement, then maximize precision"

**Implementation:**
- For each model, find threshold that achieves ≥85% recall
- Among thresholds meeting recall, select highest precision
- Compare final models at optimized thresholds

---

## 🎯 PHASE 3: MODEL COMPARISON & ANALYSIS

### 3.1 Prediction Similarity Analysis
**Assignment Requirement:** "Compare predictions from three algorithms. How similar are they?"

**Implementation:**
- Create confusion matrix comparison
- Calculate agreement rate between models
- Identify cases where models disagree
- Analyze disagreement patterns (by feature values, demographics, etc.)
- Visualizations: agreement heatmaps, disagreement case studies

### 3.2 Feature Importance Analysis
**Proposal Goal:** "Extract impact each feature has on classification"

**Implementation:**
- Logistic Regression coefficients
- Permutation importance (if time)
- Feature correlation with predictions

### 3.3 Model Selection
**Criteria:**
1. ROC-AUC (Kaggle metric)
2. Precision (at 85% recall threshold)
3. Fairness metrics (see Phase 4)
4. Prediction stability across splits

---

## 🎯 PHASE 4: FAIRNESS ANALYSIS (REQUIRED)

### 4.1 Protected Attribute Identification
**Assignment Requirement:** "Protected attributes: gender and age"

**Implementation:**
- Identify gender column (CODE_GENDER)
- Create age variable from DAYS_BIRTH
- Check feature correlations with protected attributes (as in proposal)

### 4.2 Fairness Metrics Implementation
**Assignment Requirement:** "Fairness metrics from DATA 401"

**Metrics to Implement:**
- Demographic Parity (equal positive rate across groups)
- Equalized Odds (equal TPR/FPR across groups)
- Calibration (equal PPV across groups)
- Individual Fairness (if applicable)

### 4.3 Fair Model Selection
**Assignment Requirement:** "Find best-performing model in terms of fairness"

**Process:**
1. Evaluate all three models on fairness metrics
2. Select model with best fairness performance
3. Compare fair model's prediction performance vs. best-performing model
4. Analyze trade-offs

### 4.4 Ethical Considerations
**Assignment Requirement:** "Ethical considerations with use of model"

**Analysis:**
- Which features might proxy for protected attributes?
- Impact of model on different demographic groups
- Recommendations for deployment

---

## 🎯 PHASE 5: EVALUATION & METRICS

### 5.1 Required Metrics
**Assignment Requirement:** "ROC-AUC + at least 3 other metrics"

**Current Metrics:**
- ✅ ROC-AUC (custom implementation)
- ✅ Accuracy (custom)
- ✅ Precision (custom + sklearn)
- ✅ F1 (custom)

**Additional Metrics to Add:**
- Recall (sensitivity) - needed for 85% requirement
- Specificity
- Confusion Matrix
- Precision-Recall Curve

### 5.2 Comprehensive Evaluation
**For Each Model:**
- Performance on all split strategies
- Cross-validation results
- Metrics at optimized threshold
- Fairness metrics
- Prediction agreement with other models

---

## 🎯 PHASE 6: DELIVERABLES PREPARATION

### 6.1 Presentation (10 min, Nov 14)
**Content:**
- Data prep and feature selection process
- Model fitting and assessment procedure
- Split strategy comparison
- Model selection rationale
- Fairness analysis
- Final recommendations

### 6.2 Written Report (2-5 pages, Nov 17)
**Required Sections:**
- How features and hyperparameters were chosen
- How decision was made between LR/SVM/LDA
- Final model evaluation
- Ethical considerations

### 6.3 Code Notebook (Nov 17)
**Required Elements:**
- ✅ Three classification algorithms (implemented)
- ✅ Custom metric implementations (done)
- ✅ Cross-validation from scratch (TODO)
- ✅ Prediction comparison (TODO)
- ✅ Fairness analysis (TODO)
- ✅ Well-commented code (mostly done)
- ✅ Tables and graphs for findings (partial)

---

## 📊 IMPLEMENTATION PRIORITY ORDER

### Week 1 (Immediate)
1. **Implement train/test splits** (random, stratified, non-random)
2. **Implement cross-validation from scratch**
3. **Scale features** (fix convergence)
4. **Add recall metric** (for 85% requirement)

### Week 2 (Core Analysis)
5. **Threshold optimization** (85% recall → max precision)
6. **Hyperparameter tuning**
7. **Prediction comparison analysis**
8. **Fairness metrics implementation**

### Week 3 (Finalization)
9. **Fair model selection and analysis**
10. **Comprehensive evaluation tables/graphs**
11. **Presentation preparation**
12. **Report writing**

---

## 🔍 KEY QUESTIONS TO ANSWER

### From Assignment:
1. How does changing split strategy impact validation performance?
2. Which split approach makes you most confident about Kaggle performance?
3. How similar are the three models' predictions? Why do they agree/disagree?
4. Is there a conflict between fairness and prediction performance?

### From Proposal:
1. Which features have strongest impact on classification?
2. Can we maintain 85% recall while maximizing precision?
3. How do we avoid discrimination based on age/gender?

---

## 📝 NOTES

- **Kaggle Competition:** Only one submission allowed - be careful!
- **Code Style:** Must be well-commented, avoid inefficient loops
- **Comparability:** All three models must use same features
- **From Scratch:** Cross-validation and metrics must be custom implementations
- **Focus:** ROC-AUC is primary metric (Kaggle), but need others for analysis

---

## ✅ CHECKLIST FOR COMPLETION

### Data & Features
- [x] Data loading and cleaning
- [x] Feature engineering (bureau, previous apps)
- [ ] Feature correlation with protected attributes
- [ ] Feature scaling

### Splits & Validation
- [ ] Random split implementation
- [ ] Stratified split implementation
- [ ] Non-random split implementation
- [ ] Cross-validation from scratch
- [ ] Split strategy comparison

### Models
- [x] Logistic Regression
- [x] SVM
- [x] LDA
- [ ] Hyperparameter tuning
- [ ] Class imbalance handling

### Metrics & Evaluation
- [x] ROC-AUC (custom)
- [x] Accuracy (custom)
- [x] Precision (custom)
- [x] F1 (custom)
- [ ] Recall (custom)
- [ ] Additional metrics
- [ ] Threshold optimization

### Analysis
- [ ] Prediction comparison
- [ ] Model agreement/disagreement analysis
- [ ] Feature importance
- [ ] Fairness metrics
- [ ] Fair model selection
- [ ] Ethical considerations

### Deliverables
- [ ] Presentation slides
- [ ] Written report
- [ ] Final notebook with all analyses
- [ ] Tables and graphs
- [ ] Kaggle submission (if ready)

---

**Last Updated:** Based on assignment requirements, project proposal, and current notebook status

