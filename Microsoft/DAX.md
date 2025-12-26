# Data Analysis eXpressions (DAX)

## What is DAX?

- DAX computes formulas over a *data model*
- The relationships are always `LEFT OUTER JOINs`
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
- 

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
    - However, `RELATEDTABLE` only work in *many-to-many* relationships are in the same *cross-filter* direction
    - No functions are needed with *filter context*
- `SUMMARIZE` generates a table with the unique combinations of the specified columns, similar to SQL `GROUP BY`

## References

1. [The Definitive Guide to DAX, 2nd Edition by Marco Russo and Alberto Ferrari](https://www.sqlbi.com/books/the-definitive-guide-to-dax/)
2. [DAX Formatter by SQLBI](https://www.daxformatter.com/)