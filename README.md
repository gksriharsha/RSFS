# Python-RSFS

## Installation 

RSFS is divided into two parts based on functionality. 

1. **RSFS** This module contains the core RSFS logic. It can be installed by using
   ```shell
   pip install rsfs
   ```
1. **RSFS - Test Bench** This module is meant to perform grid search operation on RSFS and save the results to a
   csv file. This will be helpful to later perform optimization procedures to find the right set of hyperparameters for 
   the dimensionality reduction of a particular dataset.
   ```shell
   pip install rsfs-bench
   ```

## Usage Instructions

The package is imported and RSFS function in the package is executed with the appropriate parameters in the function call.
The example code in the RSFS file is as follows:
```python
import numpy
import rsfs
from sklearn.model_selection import train_test_split

Data = numpy.loadtxt(open(str('../Isolet.csv'), "rb"), delimiter=",", skiprows=1)
labels = Data[:, -1]
Data = Data[:, :-1]
train, test, train_labels, test_labels = train_test_split(
  Data, labels, test_size=0.33, random_state=42, stratify=labels)
data_train = train
data_test = test
label_train = train_labels
label_test = test_labels
Parameters = {
  'RSFS': {
      'Classifier': 'KNN',
      'Classifier Properties': {
          'n_neighbors': 3,
          'weights': 'distance'
      },
      'Dummy feats': 100,
      'delta': 0.05,
      'maxiters': 300000,
      'fn': 'sqrt',
      'cutoff': 0.99,
      'Threshold': 1000,
  },
  'Verbose': 1
}
print(rsfs.RSFS(train,test,train_labels,test_labels,Parameters))
```
### Labels

This package may give rise to unexpected behaviour if the labels are not contiguous natural numbers. Therefore, the dataset should
be cleaned before executing the RSFS function.

### Parameters dictionary

This dictionary acts as a configuration for RSFS algorithm to work. Use the format for the algorithm is work as expected.
If the 'Classifier Properties' sub-dictionary should be set to the default parameters, please include an empty value pair 
in the dictionary. If the key is not included, errors will be thrown.
```python
Parameters = {

        'RSFS': {

            'Classifier': 'KNN',

            'Classifier Properties': {

                'n_neighbors': 3,

                'weights': 'distance'

            },

            'Dummy feats': 100,

            'delta': 0.05,

            'maxiters': 300000,

            'fn': 'sqrt',

            'cutoff': 0.99,

            'Threshold': 1000,

        },

        'Classifier': 'KNN',

        'Classifier Properties':
        {
            'n_neighbors': 3
        },

        'Verbose': 1
    }
```
## Explanation

I have explained the working of RSFS in my medium [blog](https://gksriharsha.medium.com) and would be focusing on usage 
instructions in the README file.

### Note

This code utilizes unweighted average recall. If weighted average recall is to be used, feel free to create a Pull Request
or fork the repository.

## License

This is a python version of RSFS algorithm that is already
[available](http://users.spa.aalto.fi/jpohjala/featureselection/). I have translated the same code 
to Python meant to be used for research purposes. Kindly follow the license terms set by the
[author](https://www.linkedin.com/in/orasanen/?originalSubdomain=fi) to whom the 
Intellectual property belongs. Based on the sentences that the author has written in the original file, I assume that
most appropriate license is CC BY-NC-SA 4.0. Please contact the original author in case of commercial or usage for closed
source applications.