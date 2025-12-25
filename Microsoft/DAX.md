# Data Analysis eXpressions (DAX)

## What is DAX?

- DAX computes formulas over a *data model*
- The relationships are always `LEFT OUTER JOINs`
- The arrows indicate the *cross filter* direction of each relationship
- Filtering always happens from the *one-side* of the relationship to the *many-side*
- Similar to Excel's [*Format as Table*](## "e.g. =[@ColName], =SUM[ColName]") references but not limited to one table
- Must specify table name when referencing column
- *Iterators*, formulas that end with X like `SUMX`, iterate over a table, perform  a calculation on each row, and aggregate the result to produce a single value
- DAX requires theory, copying formulas from the web may not work as expected

## References

[The Definitive Guide to DAX, 2nd Edition by Marco Russo and Alberto Ferrari](https://www.sqlbi.com/books/the-definitive-guide-to-dax/)

[DAX Formatter by SQLBI](https://www.daxformatter.com/)