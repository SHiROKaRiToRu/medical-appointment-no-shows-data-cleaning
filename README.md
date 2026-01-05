Medical Appointment No-Shows — Data Cleaning & Preparation
Project Overview
This project focuses on cleaning and preparing the Medical Appointment No-Shows dataset for reliable analysis.
The original dataset contains inconsistencies in column naming, data types, invalid values, and logical date issues that can lead to incorrect insights if not handled properly.
Dataset source: Kaggle — https://www.kaggle.com/datasets/joniarroba/noshowappointments
Records: 110,527
Columns: 14
The goal of this project is to transform the raw data into an analysis-ready, logically consistent dataset.
________________________________________
Objectives
•	Standardize column naming conventions
•	Correct data types for identifiers, dates, and binary variables
•	Identify and flag invalid or illogical records
•	Engineer time-based features to support downstream analysis
________________________________________
Data Cleaning Pipeline
1. Column Standardization
•	Converted all column names from CamelCase to snake_case for Python consistency
•	Fixed known typos (e.g., handcap → handicap)
•	Applied regex-based renaming to ensure uniform formatting
________________________________________


2. Data Type Conversion
Identifiers
•	patient_id and appointment_id converted to categorical/string types
Rationale: These are identifiers, not numerical quantities. This prevents invalid operations such as averaging IDs and improves memory efficiency.
Binary Variables
Converted to Boolean (True / False):
•	scholarship
•	hipertension
•	diabetes
•	alcoholism
•	handicap
•	sms_received
Date Columns
•	scheduled_day
•	appointment_day
Parsed into datetime format for time-based calculations.
________________________________________
3. Logic & Validity Checks
Age Validation
•	Observed age range: -1 to 115
•	Created age_valid flag:
o	True if age is between 0 and 120
o	False otherwise
•	Only 1 invalid record detected
Appointment Date Logic
•	Calculated days_between_schedule_and_appointment
•	Identified a common edge case:
o	Same-day appointments may appear as -1 days due to time-of-day differences
•	Created appointment_date_valid flag:
o	Differences ≥ -1 considered valid
•	Added explicit same_day_appointment indicator for clarity
________________________________________

Feature Engineering
The following features were added to support analysis:
•	age_valid (bool): Flags unrealistic patient ages
•	days_between_schedule_and_appointment (int): Time gap between booking and appointment
•	same_day_appointment (bool): Indicates appointments booked and attended on the same day
•	appointment_date_valid (bool): Flags logically consistent scheduling records
________________________________________
Outcome
The dataset is now:
•	Type-safe and consistent
•	Free from critical logical errors
•	Ready for exploratory analysis, visualization, or modeling
•	Easier to filter using explicit validity flags instead of hard deletions
This approach preserves data integrity while allowing flexible downstream analysis.
________________________________________
Tools Used
•	Python
•	Pandas
•	NumPy
•	Jupyter Notebook
________________________________________
Notes
No rows were dropped during cleaning.
Instead, validity flags were used to preserve information and allow transparent filtering decisions during analysis.
