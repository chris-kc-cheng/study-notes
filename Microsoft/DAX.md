# Data Analysis eXpressions (DAX)

## What is DAX?

- DAX computes formulas over a *data model*
- The relationships are always `LEFT OUTER JOIN`s
- The arrows indicate the *cross filter* direction of each relationship
- Avoid bidirectional relationships unless absolutely necessary
- Filtering always happens from the *one-side* of the relationship to the *many-side*
- Similar to Excel's [*Format as Table*](## "e.g. =[@ColName], =SUM([ColName])") references but not limited to one table
- Must specify table name when referencing column
- *Iterators*, formulas that end with X like `SUMX`, iterate over a table, perform  a calculation on each row, and aggregate the result to produce a single value
- DAX requires theory, copying formulas from the web may not work as expected

## Introduction to DAX

- Syntax
  - Reference to column: `'Table Name'[Column Name]`, omit single quotes only if table name contains no spaces, and not a reserve word like `Date`
  - Always use the table name in column reference and always omit it in measure references
  - Single line comments `//`, `--`, and multi-line comments `/* */`, avoid comments at the end of an expression
- Data types
  - String, case-insensitive
  - Currency, 64-bit integer divided by 10,000
  - DateTime, floating-point number, number of days since December 30, 1899
  - Avoid implicit data type conversions
- Operators
  - `AND()` and `OR()` functions are equivalent to `&&` and `||` operators, more readable but limited to 2 parameters
- Table constructor: parentheses are optional for single column, `{"a", "b"}` is equivalent to `{("a"), ("b")}`
- *Calculated columns*
  - In *Import Mode* (default), calculated columns are computed at *data refresh* time and stored in the model, no not change value based on user selections
  - In *DirectQuery Mode*, calculated columns are computed on the fly at query time
  - Use calculated columns when:
    1. Placed in slicer, rows/columns of a matrix visual, or filter condition in DAX query
    2. Expression is bound to the current row
- *Measures*
  - Aggregates values from many rows
  - Computed at *query time*, the value depends of the user selections
  - Evaluated in *filter context*, i.e. context of visual element or query
  - Use measures when:
    1. Reflect user selections
    2. Presented as aggregates
- Variable `VAR` is computed using *lazy evaluation*
- `FILTER`, `ADDCOLUMNS` and `GENERATE` are also iterators even though they do not aggregate results

## Basic Table Functions

- `VAR` can also store table
- In nested table functions, the innermost function is evaluated first (different from `CALCULATE` AND `CALCULATETABLE`)
- *Calculated table* is not available in Excel
- `EVALUATE` can be used to inspect the result of a table
- `FILTER` is both a table function and an iterator
- `ALL` ignores *any* existing filter. We declare the columns we want. The paramemeter can be a table name or a list of column names
- Use `ALLEXCEPT` if we want to ignore *most* but not all columns of a table
- `VALUES` returns only the distinct visible values given the filter in the report. 
- `VALUES` considers the blank row as a valid row, but `DISTINCT` does not. Both also accpet a table as an argument
- `SELECTEDVALUE` is equivalent to `IF(HASONEVALUE(), VALUES())`
- `ALLSELECTED` removes filters applied outside the visual, but keeps filters applied inside the visual

<details>
<summary>Examples of <h5 style="display:inline-block">EVALUATION</h5></summary>

```DAX
EVALUATE
FILTER(
    'Table',
    'Table'[Column1] > 1
)

EVALUATE
{[Measure]}

EVALUATE
SUMMARIZECOLUMNS (
    FILTER(
        'Table',
        'Table'[Column1] > 1
    ),
    "Result", [Measure]
)
```
</details>

## Evaluation Contexts

- *Filter context* **filters**, it does not iterate
- *Row context* **iterates**, it does not filter
  - *Calculated columns* is always executed in a row context
  - Row context can also be created manually by starting an iteration
- The two evaluation contexts can exist at the same time, but they do not interact
- Aggregators only use the filter context, and they ignore the row context
- The newly created (inner) row context hides the previous existing (outer) row context. To access the outer row context, use variables (preferred) or  `EARLIER`/`EARLIEST`
- *Row context* does not propagate through relationships automatically. Use the following relationship functions to access related tables
    - `RELATED` can access the *one-side* from the *many-side* of a relationship
    - `RELATEDTABLE` can access the *many-side* from the *one-side* of a relationship
    - Both functions work for *one-to-one* relationships
    - However, `RELATEDTABLE` only work in *many-to-many* relationships through a bridge table if both *cross-filters* are in the same direction
    - No functions are needed with *filter context*
- `SUMMARIZE` generates a table with the unique combinations of the specified columns, similar to SQL `GROUP BY`

## `CALCULATE` and `CALCULATETABLE`

- `CALCULATE` returns a scalar value, while `CALCULATETABLE` returns a table
- Both functions create new *filter contexts* by merging its filter parameters with the existing filter contexts
- If multiple filter arguments affect the same column, they are merged together using an `AND` operation
- Any previously existing filter contained in the filter argument is **overwritten** by the new filter. It does not overwrite other filters outside the filter argument
- Once the function ends, the previous *filter context* is restored
- `CALCULATE` accepts list of values `Table[Column1] IN {"1", "2"}` or boolean conditions
- Boolean conditions in the filter arguments syntactic sugar for `FILTER` function. However, it only works on a single column
- For complex conditions involving multiple columns, use `FILTER` function explicitly
- Use `ALL` inside `CALCULATE` to **remove** all the filters on specific columns or entire tables. You can use multiple `ALL` functions in a single `CALCULATE`. It does not behave as a table function here. `REMOVEFILTERS` is equivalent to `ALL` inside `CALCULATE`.
- To remove all filters from any table, use `ALL` with the *fact table*
- Use `VALUES` inside `CALCULATE` to restore part of the *filter context*
- `KEEPFILTERS` **adds** the new filter to the existing ones instead of overwriting them
- A filter argument referencing multiple columns require an explicit table expression
- For better performance, avoid table filters and always use a filter with the smallest number of columns
- `CALCULATE` evaluates its filter arguments first before evaluating the measure
- All filter arguments are executed in the filter context outside of `CALCULATE`, and each filter is evaluated independently
- In nested `CALCULATE` statements, the outermost filter are applied first, and the innermost later
- `CALCULATE` invalidates any *row context*. It automatically adds as filter arguments all the columns that are currently being iterated in any row context
- Every *measure* reference always has an implicit `CALCULATE` surrounding it
- Hidden circular dependencies may occur when there are more than one *calculated columns* when the *context transition* add each other as filter arguments, unless the table contains one column with unique values and DAX is aware of that because it is on the *one-side* of a one-to-many relationship
- `USERELATIONSHIP` temporarily activates an inactive relationship, deactiviating the active one outside of `CALCULATE`
- `CROSSFILTER` allows changing the relationship between two tables to either `NONE`, `ONEWAY`, or `BOTH`
- Modifiers like `USERELATIONSHIP`, `CROSSFILTER`, and `ALL*` are always applied before any explicit filter arguments

<details>
<summary>Examples of <h5 style="display:inline-block">CALCULATE</h5></summary>

### Boolean conditions in the filter arguments
```DAX
CALCULATE (
    [Measure],
    'Table'[Column1] > 1
)
```
is equivalent to
```DAX
CALCULATE (
    [Measure],
    FILTER(
        All('Table'[Column1]),
        'Table'[Column1] > 1
    )
)
```

### Filter with complex conditions
```DAX
CALCULATE (
    [Measure],
    Table[Column1] * Table[Column2] > 100
)
```
is invalid, and should be written as
```DAX
CALCULATE (
    [Measure],
    FILTER(
        ALL(Table[Column1], Table[Column2]),
        Table[Column1] * Table[Column2] > 100
    )    
)

```
</details>

## Variables

- Variables improve readability and performance
- Variables can be defined during an iteration
- DAX Variable is *constant* and cannot be modified
- Variables are evaluated once in the scope of definition `VAR`
- One should access the columns of table variable using their *original* names. Variable name is not an alias of the underlying table
- One frequent scenario is to save the results of a calculation and use it later when filter context changes

## Iterators

- *Iterator cardinality* is the number of rows being iterated
- Iterators requires you to always define, in this order:
  1. The granularity
  2. The expression
  3. The kind of aggregation
- `ADDCOLUMNS` and `SELECTCOLUMNS` are iterators that return a table, often used when authoring fast measures

## Window Functions

- Window functions sort and partition input table through `ORDERBY` and `PARTITIONBY` helper functions
- They are the only DAX functions that implement *apply semantics*
- `INDEX` returns the n-th row of a sorted table, more flexible than `TOPN`
- 

## Time Intelligence

- `Date` is a reserved word, while Dates is not
- Most time intelligence functions require a separate *date table*
- Avoid using Auto Date/Time feature because it generates one table per date column (unrelated to on another) and the tables are hidden and cannot be modified
- Best practices
  1. Contains all dates, no gaps
  2. *Date* data type is preferred
  3. Marked as a *Date table*, DAX will automatically add `ALL`
- `CALENDARAUTO` scans all date columns which may not be desiable. It accept an optional argument for fiscal year end
- `CALENDAR` requires the date range
- Use `ADDCOLUMNS` to create additional columns
- Design options:
  1. Multiple relationship to the same date table (preferred)
     - Inactive relationships can be activated through the `USERELATIONSHIP` modifier in `CALCULATE`
     - Role-playing dimension
  2. Creating multiple data tables
     - Use this design only if you need to intersect the same measure by different dates in the same visualization
- `DATESYTD`, `DATESQTD`, `DATESMTD` returns a table with all dates and requires the use of `CALCULATE`
- `TOTALYTD`, `TOTALQTD`, `TOTALMTD` hides the `CALCULATE`
- `SAMEPERIODLASTYEAR` is a specialized version of the more generic `DATEADD`
- `PARALLELPERIOD`, `PREVIOUS…`, `NEXT…` returns the full period instead
- If multiple periods are selected, `PARALLELPERIOD` shifts result of all of them, e.g. Q1 = Dec + Jan + Feb
- Intelligence functions can be cascaded, however a wrong nesting order may produce unexpected result if the date table does not contain a row in the `NEXTDAY`
- `DATESINPERIOD` is usually the best option for the moving calculation
- `LASTDATE`, `LASTNONBLANK` are often used in semi-additive calculations (e.g. last balance)

## Calculation Groups

> [!TIP]
> User-defined functions should be considered the primary tool for reusing code

- *Calculation group* is a collection of *calculation items*
- Inside a *calculation item*, you can use `SELECTEDMEASURE` as a placeholder of the measure being modified
- *Calculation group* looks like a table, and *calculation items* is like a row. User can place *calculation items* on rows/columns in a matrix
- DAX starts with the *calculation group* with the highest precedence
- `ISSELECTEDMEASURE` (preferred) and `SELECTEDMEASURENAME` provide information about the selected measure
- Avoid using `CALCULATE` inside *calculation items*

## Filter Context

- `HASONEVALUE` detects multiple selection
- `ISFILTERED` checks whether a *column* has a *direct* filter on it
- `ISCROSSFILTERED` checks whether a *table* is cross-filtered
- A column is filtered is also cross-filtered, but not the opposite
- `VALUES` returns values visible in filter context, while `FILTER`  return values that are currently being filtered by the filter context
- `VALUES` and `ALL` can be used together to produce the desired result
- With `ALL` inside `CALCULATE`, the DAX optimizer will not perform any *context transition*
- `ISEMPTY` is more efficient than `COUNTROWS() = 0`
- `TREATAS` can change the *linage* of a column

## Hierarchies

- Ratio-to-parent is simple to create with visual calculations, but not so in DAX
- `ISINSCOPE` check if the column passed as argument is filtered and is part of columns used to perform the grouping
- Flattening parent/child hierarchy into regular column-based hierarchy
  1. `PATH` creates a *calculated column* with a full path separated by the `|` character
  2. `PATHITEM` and `LOOKUPVALUE` can be used to create additional *calculated columns*.
  3. Transform the set of level columns into a hierarchy
- To improve presentation
  1. `PATHLENGTH` computes the depth of each node
  2. Sum of `ISINSCOPE` computes the current browsing depth of the report visual
  3. Check if the node is a leaf

## Working with Tables

- `CALCULATETABLE` first changes the filter context and later evaluate the expression
- `ADDCOLUMNS` is an *iterator* that returns all rows and columns of the first argument, adding newly created columns
- `SUMMARIZE` scans a table, performs a group by on any number of columns reachable following the relationships
- `CROSSJOIN` returns the cartesian product of two tables, useful for joinning for an *OR* condition, or to speed up calculations
- `UNION` does not remove duplicates, `DISTINCT` removes duplicates but has loses the data *lineage* if values come from different tables. Use `TREATAS` to control the data lineage
- `INTERSECT` returns only the rows that apear in both tables
- `EXCEPT` implements *set subtraction* by removing the rows present in the second table
- `SELECTCOLUMNS` is similar to SQL `SELECT` which implements *projection* of columns and it can add columns, may contain duplicates
- `ROW` is useful to create a table with a single row
- Static table can be created with the *table constructor* `{(),()}`
- `DATATABLE` create a table data type `{{},{}}` but limited to constant values (no DAX expression)
- `GENERATESERIES` generates series of values from the lower bound to the upper bound (inclusive) with a step, useful in slicer

## User Defined Functions (UDFs)

> [!NOTE]
> DAX user-defined functions are currently in preview. Enable this feature in Options, then use the `DEFINE FUNCTION` syntax in the DAX Query View.

```DAX
FUNCTION <function name> = ([parameter name] : [parameter type] [parameter subtype] [parameter passing mode], ...) => <function body>
```

- User can centralize the DAX code in a single location
- A function is basically a DAX formula with parameters
- There are 2 parameter passing modes:
  - `VAL` for *Value*, the caller evaluates value parameters before the function is executed, default mode
  - `EXPR`for *expression*, evaluated in the evaluation context where it is used in the function body, which may have different values in different parts of the function body
- ⚠️ Unlike measures, there is no automatic *context transition* for parameters
- Add column name as a parameter in addition to table name to make the function *model independent*
- You can also specify the subtypes of parameters

Type     | Subtype | Passing mode
---------|---------|-------------
`ANYVAL` |         | `VAL`
`SCALAR` | `VARIANT`, `INT64`, `DECIMAL`, `DOUBLE`, `STRING`, `DATETIME`, `BOOLEAN`, `NUMERIC` | `VAL`/`EXPR`
`TABLE`  |         | `VAL`/`EXPR`
`ANYREF` |         | `EXPR`

- Function name should be in PascalCase, dot (`.`) is recommended for delineating categories. Parameter names in camelCase
- Use triple slash `///` for comments describing functions

## Visual Calculations

- A visual calculation is a virtual DAX calculated column added to a Power BI visual instead of the model
- The virtual table consists of only rows and columns, there is no hierarchy nor have any sort order
- It does not have access to the semantic model and cannot be shared among visuals
- `RUNNINGSUM`, `FIRST`, `LAST`, `RANGE`, `PREVIOUS`, `NEXT` are syntactic sugar over window functions

## References

1. [The Definitive Guide to DAX](https://www.microsoftpressstore.com/store/definitive-guide-to-dax-mastering-the-semantic-model-9780138244804), by Marco Russo and Alberto Ferrari (3rd Edition was published in Dec 2025)
2. [DAX Guide](https://dax.guide/)
3. [DAX Formatter by SQLBI](https://www.daxformatter.com/)
4. [DAX Lib](https://daxlib.org/)
5. [DAX Patterns](https://www.daxpatterns.com/)