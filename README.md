# DEGO Project - Team 7

## Abstract (TO BE WRITTEN AFTER FINDINGS)

## Team Members 
- Benjamin Iby - Product Lead
- Filippo Deluchi - Governance Officer
- Maximilian Haussmann - Data Engineer
- Tim Schmitz - Data Scientist

## Project Descriptions
Credit scoring bias analysis for DEGO course

## Structure
- ‘ data /‘ - Dataset files
- ‘ notebooks /‘ - Jupyter analysis notebooks
- ‘ src /‘ - Python source code
- ‘ reports /‘ - Final deliverables

## Status Quo

At the current stage of the project, the data engineering and preparation pipeline is fully implemented and operational. This includes:

- Loading and cleaning raw datasets
- Handling missing and incomplete records
- Fixing inconsistent and invalid entries
- Data type corrections
- Duplicate handling
- Exporting structured `.csv` files
- Loading the processed data into MongoDB

The feature engineering phase has been completed, and the dataset has been adjusted accordingly for bias evaluation.

The bias analysis has been conducted, including:

- Implementation of bias formulas
- Calculation of relevant fairness metrics
- Visualization of results
- Interpretation of identified disparities

At this point, the univariate bias analysis is complete. However, multivariate bias analysis is still pending and will be the final analytical extension.

Overall, the technical pipeline (data ingestion → cleaning → feature engineering → bias metrics → visualization) is complete and reproducible.

## Next Steps

The remaining tasks are structured as follows:

* Extend bias evaluation to intersectional groups
* Compare results against univariate findings
* Document methodological approach and implications

- Governance & Ethical Framework

Starting today, the governance section will be developed. This includes:

* Ethical implications of identified bias
* Regulatory context (e.g., AI governance & fairness standards)
* Risk assessment
* Mitigation strategies
* Organizational accountability recommendations

- Final Deliverables

* Integrate multivariate findings
* Polish visualizations and explanations
* Record project presentation video
* Final project submission (target: Friday/Saturday)

With governance work beginning now and multivariate analysis completed in parallel, the project is on track to be fully wrapped up by the end of the week.

