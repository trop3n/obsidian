> Learn about where we get data and what we need to consider ethically.

- The importance of ethics in data collection
- How data may be collected
- Common sources of freely available datasets

#### Data Ethics and Data Privacy

> Much of the data available to us comes from individuals and would be considered **personally identifiable**, meaning we could use it to identify someone. Many people use the acronym PII (pronounced 'pie') for the term 'personally identifiable information'

Examples of PII:

- Social Security numbers
- credit card numbers
- phone numbers
- medical records

> We all have an obligation to protect PII.

Ethical issues regarding data collection may be divided into the following categories:

- **Consent**: Individuals must be informed and give their consent for information to be collected.
- **Ownership**: Anyone collecting data must be aware that individuals have ownership over their information
- **Intention**: Individuals must be informed about what information will be taken, how it will be stored, and how it will be used.
- **Privacy**: information about individuals must be kept secure. This is especially important for any and all personally identifiable information. 

#### Data Collection

>We collect, process, and analyze data to better understand our world and make more informed decisions. The first step in any data work is to collect the data itself. Data can come from a lot of places, including research, governments, technology, observation, or directly from individuals — the list is endless.

Finding data that doesn't exist yet can involve measuring it by using:

- Surveys
- Observational studies
- Recording experiment results

**Static** data is data that is collected once and does not change.

Data can also be live and ever-changing based on the most up-to-date information. For example, apps and websites can track clicks and time spent on pages across multiple users at the same time without a human actively recording all the data points.

We can also use data that was previously recorded by other people or for some other purpose. 

#### Data Sources

Datasets are often kept private or can only be accessed for a fee. This may be done for reasons like protecting the identity of individuals, keeping valuable information from competitors, or making a profit from data collection.

#### Data Types and Quality

> Data can mean a lot of things, but within data science, it typically means a collection of organized observations.

There are two types of organization:

- Methodology 
- Shape

**Methodology** is how the data was collected
**Shape** is how the data is presented
- The most common shape for data is a spreadsheet or table.

> The things we are measuring (**variables**) are in the columns, and the individual instances (**observations**) are in the rows. 

**Observations** are also called **entities** or **instances**. These names are used interchangably.

> Good variables measure only one characteristic and should not be a characteristic themselves. 

#### Variable Types

- Variables that are measured are **numerical** variables
- Variables that are categorized are **categorical** variables

**Numerical Variables**

> Numerical variables are are combination of the measurement and the unit. 
> Without the unit, a numerical variable is just a number.

Counting gives us whole numbers and **discrete** variables

Measuring gives us potentially partial numbers and **continuous** variables

**Categorical Variables**

>Categorical variables describe characteristics with words or relative values.

**Nominal variables** mean "named value."

**Dichotomous variables** only have two logical possibilities, "on/off", "yes/no", "true/false", "0/1"
There is no middle ground or third option

**Ordinal variables** are subjective variables that are ordered and ranked.

A **likert scale** is really popular in survey design and conveys subjective data. 
- Likert scales don't represent measurements or counts, they represent categories.

#### Dealing with Messy Data

**Messy Data Problems**

- Typos
- Missing data
- Inconsistent coding (spelled numbers(three) vs. actual numbers(3)) 

#### Missing Data

Data that is missing because it wasn't entered properly is considered **Missing Completely at Random**

> We don't always know if there's a deeper meaning to missing data, so it should be treated like a mystery to solve. 

More generally, we can predict if one value is missing based on the value in another variable. 
This is called **Missing at Random**.
- This can be confusing, because it's not missing at random in the normal meaning of the word.

Data can also be **Structurally Missing**, meaning would wouldn't expect it to be there in the first place. 

*What should I do about missing data?*

When trying to recover missing data, it is important to remember that anything you do will affect the rest of your analysis. 

Once data goes missing, it can't be recovered, so whatever decision you make becomes part of your result and your analysis (even doing nothing will affect the analysis).

Because of this, it is best practice to keep track of which values were missing just in case you ever need to revisit your data.

#### Data Accuracy

We collected our measurements, made decisions about what to do with the missing data, now we need to ask ourselves if the dataset we have really describes the world. 

**Accuracy** is a measure of how well records reflect reality.

Without a standard measurement unit and standard *method*, comparing data or even getting a good average is impossible. 

**Standardization** is essential for accuracy, but it's not the only way that accuracy can be compromised. 

There are a few ways to think about data accuracy during a critical evaluation:

- Thinking about the data against expectations and common sense is crucial for spotting issues with accuracy. You can do this inspecting the distribution and outliers to get clues about what the data looks like.
- Critically considering how error could have crept in during the data collection process will help you group and evaluate the data to uncover systematic inconsistencies. 
- Identifying ways that duplicate values could have been created goes a long way towards ensuring that reality is only represented once in your data. A useful technique is to distinguish between what was human collected versus programmatically generated and using that distinction to segment the data. 

>In the end, the only way to improve a dataset's accuracy is to use real-world knowledge to be sure that the dataset reflects reality. 
>	But even then, the reason that we collect data is generally to learn something new about the world. Sometimes the data will surprise you, but distinguishing between a new finding and inaccuracy is the work of skilled data scientist.

#### Validity

> We have to make sure our data actually measures what we think its measuring. This is the **validity** of our dataset.

**Validity** is not just about the dataset, it's about the relationship between the dataset and its purpose.
	A dataset can be valid for one question and invalid for another. 

Using proxies and inappropriate time spans are just two ways to compromise the validity of a dataset. There are infinite ways in which a given dataset is not valid for answering a given question. The best way to spot issues with the validity of a dataset is to ask: Does this variable measure what I think it does?

#### Representative Samples

A **convenience sample** is great for preliminary understanding, but not good for representing a broader population.

> The goal of a sample is to represent a population. Any time a sample is made that doe NOT reflect the entire population, it is a sampling error. 
> 	The best practice is to create a *sample* that represents the entire *population*

