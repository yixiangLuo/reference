## Data structure and indexing

1. One bracket selection
	- `df['col_name']` or `df.col_name`, selects only one column -> `pd.Series`
	- `df[['col_name']]`, `df[['col_name1', 'col_name2']]` a list instead of a single column name -> `pd.Dataframe`
	- `df[0:3]` selects row 0 to row 2. Note this is not a list `0:3`, but the exact form `start:end`. The `start` and `end` can be either indices or row names.
	- `df[[list of boolean values of length = number of rows]]`. Now this is a list. It must be a boolean list of length = number of rows. Selects rows. e.g. `df[df['col'] > 0]`
2. `df.loc[]`, select by names. Note it is bracket `[]`, not parenthesis `()`.
	- `df.loc[rows]` (just like `df[cols]`)
		- `df.loc['row_name']` -> `pd.Series`
		- `de.loc[['row_name']]` -> `pd.Dataframe`
	-  `df.loc[rows, cols]`
		- `df.loc[:, 'col_name']`: all row, `pd.Series`
		- `df.loc[[list of row names], [list of col names]]`, sub dataframe
3. `df.iloc[]`, select by location inded. Note it is bracket `[]`, not parenthesis `()`.
	- `df.iloc[row_index]` (just like `df.loc[rows]`, but with index)
		- `df.iloc[0]` -> the first row, `pd.Series`
		- `de.loc[[row_index]]` -> `pd.Dataframe`
	-  `df.loc[rows, cols]`
		- `df.loc[:, col_index]`: all row, `pd.Series`
		- `df.loc[[list of row indices], [list of col indices]]`, sub dataframe

## Basic operations
1. Filter
2. mutate
3. sort
4. rename

## Advanced operations
1. group by
2. aggregate function
3. apply function
4. sliding window
5. pivot/melt
6. append
7. join

## Visualization by plotly