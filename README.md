# jupyterlabel
> A library to label data in Jupyter Notebooks


## Why should you use this? 

Developing a deep understanding and intuition for a dataset is important for any Data Science or Machine Learning project. An underappreciated way of accomplishing this is to label data yourself.

When people think of Exploratory Data Analysis (EDA), plotting many beautiful graphs comes to mind. But eyeballing the data, coming up with heuristics, labeling the data, and evaluting those heuristics are valuable too. At worst you learn a lot about your dataset and at best you realize your heuristic is good enough you may not even need to resort to an ML model!

jupyterlabel aims to streamline this process.

## Installation 

`pip install jupyterlabel`

## Usage 

### Load dataset

Load dataset containing at least one target variable into a pandas dataframe. 

```python
import pandas as pd
from IPython.display import Image

from jupyterlabel import jupyterlabel as labeler
```

```python
input_file = '../data/FIFA 2018 Statistics.csv'
output_file = '../data/labels.csv'
df = pd.read_csv(input_file)
df.columns
```




    Index(['Date', 'Team', 'Opponent', 'Goal Scored', 'Ball Possession %',
           'Attempts', 'On-Target', 'Off-Target', 'Blocked', 'Corners', 'Offsides',
           'Free Kicks', 'Saves', 'Pass Accuracy %', 'Passes',
           'Distance Covered (Kms)', 'Fouls Committed', 'Yellow Card',
           'Yellow & Red', 'Red', 'Man of the Match', '1st Goal', 'Round', 'PSO',
           'Goals in PSO', 'Own goals', 'Own goal Time'],
          dtype='object')



### Define features and target variable to explore

If the target variable is continuous, you'll want to bucket the values since jupyterlabel only supports explicit labels for target variables.

```python
target_var = 'Man of the Match'
features = [
    'Goal Scored', 'Ball Possession %',
    'On-Target', 'Off-Target',
    'Blocked',
    'Corners',
    'Offsides', 
    'Free Kicks', 
    'Saves',
    'Pass Accuracy %',
    'Passes'
]
labeler = labeler.Labeler(df, target_var, features=features, output_path=output_file)
```

### Label data one row at a time

Notice that the target variable is excluded from the data frame row. The available options are the labels in the target variable column. After entering save, a csv file is written if an output path is defined and a confusion matrix is displayed to give feedback on your labelling efforts. Happy labelling!

```python
Image(filename="../images/jupyterlabel.gif.png")
```




![png](docs/images/output_14_0.png)


