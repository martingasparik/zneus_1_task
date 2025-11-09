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

## 2. DATA PRE-PROCESSING
We first dropped all columns with any sensitive data in it, becuse we can't replace them with any alternative metrics. We also dropped any columns irrelevant to the experiment, such as patient and case IDs. What was left were the columns representing the drugs administred and the readmitted variable, showcasing the state of patients after their teratment.

Using a simple encoder, we represented the four values in the drugs columns (Up, Down, Steady, NO) with numerical values. We did the same with the readmitted varaible, however in this caase we only took into account if the patient needed to be readmitted in less than 30 days (if the patient got readmitted after a month, we'd consider that the same success as if not being readmitted at all).

During our presentation we notices severe under perfomance form our neural network, thus we decided to drop any drug columns with only a NO value and compared their correlation. None of the drugs correlated hugely together, meaning we had to use as much of them s apossible. We also found out, that the data isn't scaled properly, so we applied a scaler on it.

# ADD COMMENT ABOUT SMOTE

## 3. ASSEMBLING THE NEURAL NETWORK
We decided to opt for ReLU, because we are working with simple numerical data (both the drug columns and readmitted use a simple encoding) and at the end we use a sigmoid to determine the binary classification. Adam and Cross Entropy were chosen after running the experiment a number of times. We also added a stopper function, which will stop the Neural Network after not being able to learn better, then in the last three epochs, making sure it stops before getiing overfitted.
