# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an academic project for a Master of Science in Applied Data Science and AI program, specifically for the "Essential Math for Data Science and AI" course. The project implements **Naive Bayes Classification for Email Spam Detection** with a focus on mathematical foundations and algorithm comparison.

## Project Structure

### Core Files
- `email_dataset.csv` - Original email server log dataset (5,000 records)
- `generate_synthetic_email_data.py` - Synthetic data generator maintaining statistical distributions
- `synthetic_email_dataset.csv` - Generated synthetic dataset for safe academic use

### Dataset Schema
Both datasets contain 12 fields:
- **Target Variable**: `Spam Detection` (empty = legitimate, "Moderate" = spam)
- **Key Features**: `Spam Score` (0-156), `Status` (email processing state), `Subject`, `From (Header)`
- **Supporting Fields**: `From (Envelope)`, `To`, `Sent Date/Time`, `IP Address`, `Attachment`, `Route`, `Info`

### Statistical Properties
- **Total Records**: 5,000 emails
- **Class Balance**: ~50% legitimate, ~50% spam (ideal for Naive Bayes)
- **Feature Types**: Numerical (`Spam Score`), categorical (`Status`), text (`Subject`, `From`)

## Development Commands

### Data Generation
```bash
# Generate new synthetic dataset
python3 generate_synthetic_email_data.py

# Analyze dataset statistics
python3 -c "
import csv
from collections import Counter
with open('synthetic_email_dataset.csv', 'r') as f:
    reader = csv.DictReader(f)
    rows = list(reader)
    print(f'Total: {len(rows)}')
    spam_count = sum(1 for r in rows if r['Spam Detection'] == 'Moderate')
    print(f'Spam: {spam_count}, Legitimate: {len(rows)-spam_count}')
"
```

### Python Environment
```bash
# Create virtual environment
python3 -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# No external dependencies required - uses Python standard library only
# Per assignment requirements: csv, random, datetime, re, typing
```

## Assignment Requirements

### Academic Constraints
- **Libraries**: Python built-in libraries only (no numpy, pandas, sklearn for implementation)
- **Allowed Tools**: Weka, Orange, scikit-learn for comparison/validation only
- **Implementation**: Hand-coded Naive Bayes classifier required

### Expected Deliverables
1. **Hand-coded Naive Bayes Classifier**
   - Manual probability calculations P(feature|class), P(class)
   - Bayes' theorem implementation from scratch
   - Feature extraction from text fields

2. **Sklearn Comparison**
   - Direct comparison with sklearn.naive_bayes
   - Performance metrics analysis
   - Algorithm validation

3. **Mathematical Analysis**
   - Feature independence assumption discussion
   - Conditional probability analysis
   - Optimization techniques exploration

## Code Architecture Notes

### Synthetic Data Generator Design
- **SyntheticEmailGenerator Class**: Main orchestrator with statistical preservation
- **Distribution Preservation**: Maintains original dataset proportions using probability sampling
- **Feature Correlation**: Realistic relationships (e.g., high spam scores → spam classification)
- **Reproducibility**: Fixed seed (42) for consistent academic results

### Feature Engineering Opportunities
```python
# Text features from Subject field
- Word count, capitalization patterns
- Spam keywords frequency
- Punctuation analysis

# Email features from From fields
- Domain reputation patterns
- Email address structure analysis
- Sender authenticity indicators

# Numerical features
- Spam Score thresholds
- IP address geolocation patterns
- Temporal patterns from datetime
```

### Naive Bayes Implementation Strategy
1. **Data Preprocessing**: Clean text, extract features, handle missing values
2. **Probability Calculation**:
   ```python
   P(spam|features) = P(features|spam) * P(spam) / P(features)
   ```
3. **Laplace Smoothing**: Handle zero probabilities for unseen feature combinations
4. **Classification**: Apply Bayes' theorem for prediction
5. **Validation**: Cross-validation, confusion matrix, accuracy metrics

## Mathematical Focus Areas

### Probability Theory Application
- **Conditional Probability**: P(feature|class) calculations
- **Bayes' Theorem**: Posterior probability computation
- **Prior Probabilities**: Class distribution analysis

### Independence Assumption Analysis
- **Feature Correlation**: Analyze violations of independence assumption
- **Impact Assessment**: How correlations affect classification accuracy
- **Mitigation Strategies**: Techniques to handle dependent features

### Optimization Concepts
- **Maximum Likelihood Estimation**: Parameter optimization
- **Log Probabilities**: Numerical stability in calculations
- **Cross-Validation**: Model selection and hyperparameter tuning

## Testing Strategy

### Validation Approach
```bash
# Split synthetic dataset for training/testing
# Implement k-fold cross-validation manually
# Compare hand-coded vs sklearn results
# Analyze feature importance and independence violations
```

### Performance Metrics
- Accuracy, Precision, Recall, F1-Score
- Confusion Matrix analysis
- ROC curves (if implementing probability scores)
- Feature importance ranking

## Academic Documentation Standards

### Code Requirements
- Comprehensive comments explaining mathematical concepts
- Clean, readable code structure suitable for academic evaluation
- Test cases on small examples as specified
- Mathematical derivations in comments where applicable

### Analysis Requirements
- In-depth independence assumption discussion
- Detailed comparison methodology
- Mathematical justification for design decisions
- Performance analysis with statistical significance

## Development Tips

### Feature Extraction Best Practices
- Extract meaningful features from text fields for better classification
- Consider TF-IDF style calculations using only built-in libraries
- Implement stemming/normalization manually if needed for assignment requirements

### Implementation Notes
- Use log probabilities to avoid numerical underflow
- Implement Laplace smoothing for robust probability estimation
- Handle edge cases (empty features, unknown words)
- Maintain academic code quality standards throughout