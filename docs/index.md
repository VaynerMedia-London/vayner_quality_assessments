# Getting Started
A Library built to work on generic pandas Dataframes and provide quality assessments such
as the number of nulls in certain columns, the recency of data row items or the number
of duplicates

## Library Installation
```
pip install vaynerqualityassessments
```
To upgrade the library after an update
```
pip install vaynerqualityassessments --upgrade
```
## Initialisation of the QualityAssessments class
An instance of the "QualityAssessments" class can be initiated with the ability to read/write with 
google sheets by being passed a UtilityFunctions object from the 
[veetility](https://github.com/VaynerMedia-London/veetility) library.
Please consult the documentation for that library in order to be able to create an instance of
the UtilityFunctions class

## Setup in code
Once the instance of the UtilityFunctions class has been created i.e. "util". This can then be passed
to the QualityAssessments initialisation.

```
import config as cf
from veetility import utility_functions
from vee_qa import quality_assessments as qa

util = utility_functions.UtilityFunctions(cf.google_sheet_auth_dict,cf.db_user, 
                                          cf.db_password,cf.db_host,
                                          cf.db_port, cf.db_name)

qual_assess = qa.QualityAssessments(util)
```
## Usage in code
Once a "QualityAssessments" class instance has been created e.g. "qual_assess" this can be used to access
quality assessment related functions such as checking for data recency.

There are three typical places where data quality assessment functions would be run

1. Pre-processing, when the data is raw from the input source such as from Tracer
2. Mid-processing, after a particularly complex function or after merging data, where a check for duplicates may be appropriate.
3. Post-processing, at the end of the script just before sending to the end destination

Most of the functions in this library return an error message, if no error has occured then the error message
will be a blank string. The error messages can then be concatenated together and passed to a notification function
like SlackNotifier from the veetility library.
