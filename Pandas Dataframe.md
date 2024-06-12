## Data structure and indexing

1. One bracket selection
	- `df['col_name']` or `df.col_name`, selects only one column -> `pd.Series`
	- `df[['col_name']]`, `df[['col_name1', 'col_name2']]` a list instead of a single column name -> `pd.Dataframe`
	- `df[0:3]` selects row 0 to row 2. Note this is not a list `0:3`, but the exact form `start:end`. The `start` and `end` can be either indices or row names.
	- `df[[list of boolean values of length = number of rows]]`. Now this is a list. It must be a boolean list of length = number of rows. Selects rows. e.g. `df[df['col'] > 0]`
	- Hierarchical indexing: tuple index `df[('col_level1', 'col_level2')]`
1. `df.loc[]`, select by names. Note it is bracket `[]`, not parenthesis `()`.
	- `df.loc[rows]` (just like `df[cols]`)
		- `df.loc['row_name']` -> `pd.Series`
		- `de.loc[['row_name']]` -> `pd.Dataframe`
	-  `df.loc[rows, cols]`
		- `df.loc[:, 'col_name']`: all row, `pd.Series`
		- `df.loc[[list of row names], [list of col names]]`, sub dataframe
2. `df.iloc[]`, select by location instead. Note it is bracket `[]`, not parenthesis `()`.
	- `df.iloc[row_index]` (just like `df.loc[rows]`, but with index)
		- `df.iloc[0]` -> the first row, `pd.Series`
		- `de.loc[[row_index]]` -> `pd.Dataframe`
	-  `df.loc[rows, cols]`
		- `df.loc[:, col_index]`: all row, `pd.Series`
		- `df.loc[[list of row indices], [list of col indices]]`, sub dataframe

## Basic operations

1. Filter: `df[[list of boolean values of length = number of rows]]`
3. mutate: `df['new_col'] = pd.Series`
4. sort: `df.sort_values(by = [col1, col2], ascending = [True, False])`, by default, `inplace = False`.
5. rename:
	 - row `df.index.names = [list of names]`, `df.rename(index={1: 'a'})`
	 - col `df.columns.names = [list of names]`, `df.rename(columns={'B': 'BB'})`
6. slice: `df.head(n = 5)`

## Advanced operations

1. apply functions to dataframe and series
   -  some built-in methods of dataframe: `df.sum()` takes summation on each column
   - `apply` apply functions to each **column** (on df) or **element** (on series)
     - `df['col'].apply(lambda x: x+1)` here `x` is a scalar. if the function returns a list, the result will be a series of `n` elements each of which is a list.
     - `df.apply(lambda x: x+1)` here `x` is a series. if the function returns a list, the result will be a dataframe with rows being the returned lists for each column.
     - to apply multiple functions, do `obj.apply([list of functions])`
     - use `axis = 1` to apply to each row in a dataframe
   - `agg`
     - when used in the same syntax as `apply`, does the same thing
     - allow applying different functions to different columns, unmentioned columns are purged
       `df.agg({'col1': [lambda x: sum(x), 'mean'], 'col2': 'max})` here `x` is a series (column), will use hierarchical index if apply multiple functions to one column `('col1', 'function_name')`.
2. group
   `groups = df.groupby(by = ['col1', 'col2'], as_index = False)`, `as_index = True` (default) to make group key row index, `as_index = False` to make group key columns (SQL-style).
	- `groups.apply(lambda x: x.iloc[:, 0:2])` here `x` is the sub-**dataframe** in each group including the group key columns. So not like before, when apply to groups, the function applies to the entire dataframe instead of each column. If returns a dataframe, the result is a union of all the returned dataframe with hierarchical row index `('group key value', 'returned df row index')`.
	  Only one function is allowed. Can't do `groups.apply([list of functions])`
	  Can do `groups[['col1', 'col2']].apply(lambda x: x.iloc[:, 0:2])` do select sub-dataframe after grouping.
	- `agg` behaves in the same way as being applied to dataframe:
	  `groups.agg('sum')`, `groups.agg([lambda x: sum(x), 'mean'])` applies functions to each column of the sub-dataframe in each group, here `x` is a series (column)
	  `groups.agg({'col1': [lambda x: sum(x), 'mean'], 'col2': 'max})` apply different functions to different columns
	- Other useful techniques
		- group by outside keys: `df.groupby(by = [1,1,0,...,0])`, list must have length = `n_row`. group key will not appear as index or column in the result.
		- pick the largest three rows in each group
		  `groups.apply(lambda x: x.sort_values(by = 'col', ascending = False)).head(3)`
3. sliding window
2. pivot/melt
3. append
4. join

## Visualization by plotly