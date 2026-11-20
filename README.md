# Classification: When 90% Accurate Is Worthless

## Objective
I tested why accuracy fails as a measure when loan defaults are rare and chose a decision threshold from what each kind of error costs a lender.

## Methodology
- I worked with 6,000 simulated loan applications with a default rate of 9.6%, where a rule that approves everyone is already 90.4% accurate.
- I fitted a logistic regression in a pipeline with a scaler and scored it at the usual 0.5 threshold.
- I read the coefficients as log-odds and as odds ratios, and showed that one odds ratio means different changes in probability at different starting points.
- I traced precision and recall across six thresholds.
- I chose a threshold by minimising the expected cost of the two errors, picking it on the training rows and pricing it on the test rows once.
- I wrote a small function, precision_recall_at(), that gives a classifier's precision and recall at any threshold.

## Key Findings
- At the usual 0.5 threshold the model was 90.4% accurate with 0 predicted defaults, exactly as good as approving everyone.
- The odds ratio for one more prior default was 1.63, which moves the probability of default by different amounts depending on where it starts.
- The cost-minimising threshold was 0.121, close to the closed-form threshold of 0.118 and far below 0.5.
- The expected cost was 944 per applicant at the chosen threshold, against 1,147 per applicant at 0.5.
- At the closed-form threshold, precision was 0.181 and recall was 0.477.
