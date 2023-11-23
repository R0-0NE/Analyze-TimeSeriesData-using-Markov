# Analyze-Time-Series-Data-Using-Markov-Transition-Fields
A Markov transition field (MTF) is a matrix that indicates the transition probability of the datapoints at different time steps. A Markov transition field is constructed by unwrapping the Markov Matrix and assigning the transition probabilities to corresponding time steps.

* **pandas**: This library will be used for managing the dataset.

* **NumPy**: This library will be used for mathematical functionalities.

* **Scikit-Image**: This library will be used for processing the data matrix.

* **measure**: This module is used to measure different aspects of the data matrix.

* **pyts**: This library is used to process the time series data.

* **preprocessing.discretizer**: This module allows us to discretize a given dataset in bins.

* **Matplotlib**: This library is used for visualization purposes. We will use the following packages:

* **pyplot**: This module will be used for creating inline plots.

* **color**: This module will be used for mapping numbers to RGB colors.

* **cm**: This module will be used for colormap functionalities.

The Electricity Transformer Temperature (ETT) dataset comprises the measurements of different parameters of transformers in China. The data was collected from July 2016 to July 2018. For this project, you will use the ETT-small dataset, which contains the data of two transformers. It consists of the following data columns:

|    Column     |           Description            |
| ------------- | -------------------------------- |
| date          | The date of the recorded sample  |
| HUFL          | High Useful Load                 |
| HULL          | High Useful Load                 |
| MUFL          | High Useful Load                 |
| MULL          | High Useful Load                 |
| LUFL          | High Useful Load                 |
| LULL          | High Useful Load                 |
| OT            | Oil Temperature                  |

* Import the ETT-small dataset from the following URL in a pandas DataFrame: 
https://raw.githubusercontent.com/zhouhaoyi/ETDataset/main/ETT-small/ETTh1.csv

* Verify it by printing a few rows of the DataFrame.

* Find the number of samples in the DataFrame.

Since the the table consists of approximately 17,000 samples. For convenience, let’s truncate the DataFrame to reduce the number of datapoints.

* Truncate the DataFrame to reduce the number of datapoints.

In order to encode the analog data in a matrix, you will first need to discretize it in quantile bins. Quantile binning will ensure that the same number of datapoints are assigned to each bin.

* Discretize the HUFL column of the DataFrame in 10 quantile bins.

Use the KBinsDiscretizer() method of the pyts library for discretizing the data.

* Add the discretized HUFL values in a new DataFrame column, HUFL_disc.

To add an array, new_data to a pandas DataFrame, df, with the label, use the following command:

df.['label'] = new_data

* View the resulting DataFrame.

An adjacency matrix encodes the dynamics of the time series such that each element indicates the number of times a bin transitions into another bin. The column index represents the previous bin, while the row index represents the next bin.

* Create an adjacency matrix, from the HUFL_disc data column.

* Print the adjacency matrix.

A Markov matrix indicates the probability of moving from one datapoint to another. So, the only difference between an adjacency matrix and a Markov matrix is that the columns of the latter are normalized, such that the sum of the probabilities of moving to some datapoint from a certain datapoint is always 1.

* Normalize the columns of the adjacency matrix.

* Print the resulting matrix.

The Markov matrix depicts the relation between different datapoints of the time series data. However, it provides little information about the temporal relationship between datapoints. For this purpose, you will need to construct the Markov transition field of the given time series data.

A **Markov transition field (MTF)** is a matrix that indicates the transition probability of the datapoints at different time steps. A Markov transition field is constructed by unwrapping the Markov Matrix and assigning the transition probabilities to corresponding time steps.

* Construct a Markov transition field of the HUFL_disc data.

A number of following observations can be drawn about the times series data by observing the plot of the Markov transition field:

Now that you’ve created the Markov transition field, plot it so that you can have a graphical representation of the 
1000 × 1000 matrix. This will aid you in qualitatively observing the data pattern in the matrix.
 
* The diagonal entries are generally brighter than the off-diagonal entries. This indicates that many samples self-transition instead of transitioning to other bins.

* The entries adjacent to the diagonal are generally brighter than the entries far away from the diagonal. This indicates that there is no abrupt change in the time series data, a fact that can be verified by looking at the time series data plotted earlier.

* The probability is highest in the second-last quarter of the Markov transition field (as indicated by the yellow square in the plot), which represents the self-transition of the corresponding datapoint for a very long time. This observation can be verified as a long horizontal line in the second-last quarter of the time series plot.

The Markov transition field created in the previous step is of the size, 1000 x 1000. Operations performed with a matrix this large are computationally intensive. You need to downsample the matrix to reduce its size and preserve its essential properties.

Piecewise Aggregate Approximation (PAA) is a data-reduction technique in which an n-sized data is divided into w blocks, and each block contains the mean of the comprising samples.

* Reduce the 1000×1000 Markov transition field to a 100×100 matrix using Piecewise Aggregate Approximation.

* Display the resulting matrix.

Self-transition probability is an important parameter of the time series data, which represents the probability of a datapoint to transition to itself after a time step. In a Markov transition field, this is depicted by the diagonal entries of the matrix.

* Plot the self-transition probabilities from the downsampled Markov transition field on the corresponding datapoints of the time series plot.
