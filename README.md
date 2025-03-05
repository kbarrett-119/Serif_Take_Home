# Serif_Take_Home

##OVERVIEW

I used the Jupyter notebook Serif_Take_Home.ipynb to process the data. The resulting table with processed and cleaned up data is saved in TakeHome.csv.

A large part of the code focuses on looking for inconsistencies between the hpt and tic files (which were minimal).

The code that searches for inconsistencies rests on a single variable 'Treatment_ID' that concatenates the values of every other variable with information on hospital, payer, the service, and the way the service is charged. It's not elegant, but it's easier than keeping track of all of the variables separately. The 'Treatment_ID' variable concatenates the following variables:

'hospital_name'
'hospital_id'
'payer_name'
'plan_name'
'code_type'
'raw_code'
'setting'
'description'
''modifiers'
'standard_charge_methodology'
'additional_payer_notes'
'additional_generic_notes'

 We would expect each unique value of Treatment_ID to have one and only value for the variables that describe cost:
 
 'standard_charge_gross'
 'standard_charge_discounted_cash'
 'standard_charge_negotiated_dollar'
 'standard_charge_negotiated_percentage'
 'standard_charge_min'
 'standard_charge_max'

Within an individual dataset (hpt or tic), we find that there are 75 Treatment_ID values that have multiple rows with conflicting values for one or more cost variable. If these rows are left as is, it causes conflicts between hpt and tic. However, if these rows are condensed so that each unique Treatment_ID has only one row, and the mean is taken over conflicting numerical values, the resulting hpt and tic dataframes have no differences in variables between one another.

The idea that taking a mean is appropriate is a big assumption! This would need to be investigated and confirmed as a legitimate interpretation before delivering such results to any stakeholders. Notably, the cases that had conflicting numbers were all of the "fee schedule" type of standard_charge_methodology. In the end, I chose to only use "Case Rate" values, so the table that I provided does not rely on any assumptions about taking means.

Assuming that taking the mean is a legitimate approximation to not get bogged down with this limited number of cases, I am not finding inconsistency between the hpt and tic data sources.

Most of the code works on this problem of checking for inconsistencies. The last few cells try to clean things up to a more manageable subset of information. I chose the following restrictions:

-Look at only CPT codes
-Look at only cases where the treatment is being offered both inpatient AND outpatient
-Look at rows that provide a 'Case Rate' charge methodology

With these restrictions, the rows of the table are more meaningfully comparable to one another and can be used to understand the differences between hospitals and payers. Although the time I spent was all devoted to wrangling, with more time, it would be very interesting to look at patterns in costs between different hospitals and payers.

##INSTRUCTIONS

This is pretty simple to run! In the second cell of the Jupyter notebook, set the working directory to the directory containing the raw csv files ('hpt_extract_20250213.csv' and 'tic_extract_20250213.csv'). Other than that no modifications are needed -- run the notebook and it will create the final table in the csv file TakeHome.csv in the working directory.

##OTHER NOTES

This notebook could be applied to data analysis/exploration by making changes to the definition of the 'Treatment_ID' variable. The notebook has functions that look for inconsistencies within and between dataframes, and it has the flexibility to call out such inconsistencies for any definition of 'Treatment_ID'. So a user can pick any definition of 'Treatment_ID' for which differences/inconsistencies should be flagged, and the code has some useful intermediate output within the Jupyter notebook.
~                        
