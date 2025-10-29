# ZNEUS_TASK_1
# DATASET: DIABETES 130-US

## 1. EXPLORATORY DATA ANALYSIS
This dataset represents ten years woth of clinical care data at 130 US hospitals and integrated delivery networks. The instances represent hospitalized patient records diagnosed with diabetes, who underwent laboratory, medications, and stayed up to 14 days.

source: https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008

The dataset contains 50 columns and over 100 000 rows, which is great for machine learning. From our initial analysis, it would seem that the dataset contains mostly data, about which drugs the patient took during their medication and data about the patient's diagnosises.

What makes the dataset difficult is the fact we are working with sensitive data, which means that some values have been redacted due to the private nature of it. Thus, we will have to work around this data. Our leading design will be to remove as much of the redundant redacted columns as possible.

As far as data goes, the dataset contains mostly columns with Up/Down/Stable/Np values, to show which drugs the patient took. We can easily convert these into an integer form for smoother training.

There is also some data, which we won't most likely need, such as encounter_id and patient_nbr, which exist solely for indexing.

There are also two columns; _max_glu_serum_ and _A1Cresult_ which contain explicit null-values. We will be wither deleting or replacing these values in the future.

From the heatmap, we have deducted, that the numerical data might be heavily irrelevant, we'll be picking out a handful of them, however we will mainly be focusing on the drugs taken and the amount of procedures taken.

Our goal will be to binary classify patients, based upon if the treatment was succesfull. We will be looking at the drugs taken, number of procedures and diagnosses to access, if the patient can be let out. Our main hurdle will be in handling sensitive data and filling up the missing data with something. We propose to delete any sensitive data marked with a "?" and claddify each record in the drug columns to find out if the patient can succesfully be discharged.

According to the lecturer's note, we inspected the _readmitted_ column, finding that it contains three values: (<30, >30, NO). All of these values have enough representation to be relevant, however we'll have to scale the weights of <30, since NO has 5x more instances, than it.
