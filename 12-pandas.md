# Pandas

## Object creation

Creating a Series by passing a list of values, letting pandas create a default integer index. Creating a DataFrame by passing a NumPy array, with a datetime index and labeled columns. Creating a DataFrame by passing a dictionary of objects that can be converted into a series-like structure. The columns of the resulting DataFrame have different dtypes. If you’re using IPython, tab completion for column names (as well as public attributes) is automatically enabled. Here’s a subset of the attributes that will be completed. As you can see, the columns A, B, C, and D are automatically tab completed. E and F are there as well; the rest of the attributes have been truncated for brevity.

## Viewing data

Here is how to view the top and bottom rows of the frame. Display the index, columns. DataFrame.to_numpy() gives a NumPy representation of the underlying data. Note that this can be an expensive operation when your DataFrame has columns with different data types, which comes down to a fundamental difference between pandas and NumPy: NumPy arrays have one dtype for the entire array, while pandas DataFrames have one dtype per column. When you call DataFrame.to_numpy(), pandas will find the NumPy dtype that can hold all of the dtypes in the DataFrame. This may end up being object, which requires casting every value to a Python object. For df, our DataFrame of all floating-point values, DataFrame.to_numpy() is fast and doesn’t require copying data. For df2, the DataFrame with multiple dtypes, DataFrame.to_numpy() is relatively expensive. describe() shows a quick statistic summary of your data. Transposing your data. Sorting by an axis and soring by value. 

## Selection

While standard Python / NumPy expressions for selecting and setting are intuitive and come in handy for interactive work, for production code, we recommend the optimized pandas data access methods, .at, .iat, .loc and .iloc. See the indexing documentation Indexing and Selecting Data and MultiIndex / Advanced Indexing.

**Getting** Selecting a single column, which yields a Series, equivalent to df.A. Selecting via [], which slices the rows. 

**Selection by label** For getting a cross section using a label. Selecting on a multi-axis by label. Showing label slicing, both endpoints are included. Reduction in the dimensions of the returned object. For getting a scalar value. For getting fast access to a scalar (equivalent to the prior method).

**Selection by position** Select via the position of the passed integers. By integer slices, acting similar to NumPy/Python. By lists of integer position locations, similar to the NumPy/Python style. For slicing rows explicitly. For slicing columns explicitly. For getting a value explicitly. For getting fast access to a scalar (equivalent to the prior method).

[Read more with examples](https://pandas.pydata.org/pandas-docs/stable/user_guide/10min.html)