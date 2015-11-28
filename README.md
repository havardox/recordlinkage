# recordlinkage

This package, **recordlinkage**, is a Python package to link records in or between datasources. The package provides a set of additonal tools needed for record linkage such as indexing methods and similarity measures. The package is developed for research and linking of small or medium sized files. 

This project is inspired on the **Freely Extensible Biomedical Record Linkage (FEBRL)** project, which is a great project. This project takes advence of the **pandas** package. This flexible and powerful data analysis and manipulation library for Python makes the record linkage process much easier. 

One of the aims of this project is to make it easy to implement your own extensions for your own projects. Extensions like custom indeixng methods and data comparison methods. 

## Simple linking example
Import the ``recordlinkage`` module that contains all important tools for the linking of records. Also import two **pandas** dataframes with example data named ``censusdataA`` and ``censusdataB``. 

```python
import recordlinkage
from recordlinkage.sampledata import censusdataA, censusdataB
```

Next, we make pairs of records. Each pair contains one record of ``censusdataA`` and one record of ``censusdataB``. The number of record pairs can be large, therefore required that the record pairs are identical on the surname. 

```python
index = recordlinkage.Index(censusdataA, censusdataB)
pairs = index.block('surname')
```
For each record pair, we compare the records. 
```python
compare = recordlinkage.Compare()

compare.exact(pairs['name_A'], pairs['name_B'])
compare.exact(pairs['sex_A'], pairs['sex_B'])
compare.exact(pairs['dob_A'], pairs['dob_B'])
compare.exact(pairs['street_A'], pairs['street_B'])
compare.exact(pairs['place_A'], pairs['place_B'])
compare.exact(pairs['haircolor_A'], pairs['haircolor_B'])
```

The result of the comparison is found in 

```python
compare.comparison_vectors
```

```python
recordlinkage.FellegiSunter()
```



## Main Features
The main features of the **recordlinkage** package are:

  - Clean and standardise data
  - Make pairs of records with several indexing methods such as **blocking** and **sorted neighbourhood indexing**
  - Compare characteristics with a large number of comparison functions
  - Approximate string comparison methods such as jaro-winkler distance and levenshtein distance 
  - Fellegi and Sunter (1969) classifier implemented
  - Expectation-Conditional Maximisation algoritm implemented to estimate parameters for the Fellegi and Sunter framework

## Dependencies
The following packages are required. You probably have it already ;)
- [NumPy](http://www.numpy.org): 1.7.0 or higher
- [Pandas](https://github.com/pydata/pandas): 0.17.0 or higher

The following packages are optional
- [jellyfish](https://github.com/jamesturk/jellyfish): Needed for approximate string comparison. Version 0.5.0 or higher.
- [matplotlib](http://matplotlib.sourceforge.net/): Plotting graphs.


##Install 
It is not possible to install the package with ``pip``. You can download or clone the **recordlinkage** project and install it in the normal way

```sh
python setup.py install
```

## License
GPLv3

## Background
