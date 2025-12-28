# Power Query (M language)

> [!NOTE]
>  Power Query is also incorporated into [Azure Data Factory](https://learn.microsoft.com/en-us/azure/data-factory/control-flow-power-query-activity), [Dataflows](https://learn.microsoft.com/en-us/power-query/dataflows/overview-dataflows-across-power-platform-dynamics-365), [Power BI Report Builder](https://learn.microsoft.com/en-us/power-bi/paginated-reports/report-builder-power-bi) and SQL Server Data Tools

- M is case sensitive
- list and record expressions are evaluated using Lazy evaluation, all other expressions are evaluated using eager evaluation
- Every value has a *metadata record*
- Comments: `//` and `/*…*/`
- Escape sequence: `#(#)(`

## Values

- List: `{123, true, "A"}`, `{1..N}`
- Record: `[A=1, B=2, C=3]`
- Table: `#table({"A", "B"}, {{1, 2}, {3, 4}})`
  - Search: `myTable{0}`, `myTable{[A="1"]}`
- Function: `(x) => x + 1`
  - Simplify as `each _ + 1`
  - prefix `@` when calling a function recursively

## Operators

- Lookup: `[A]`
- Positional index: `{0}`
- `&` can concatenate text, list or merge record

## Expression

- The `let`…`in` in M is similar to `VAR…RETURN` in DAX. The `let` expression can be nested
- `if…then…else`
- Error handled by `try` can be acceseed by `result[HasError]` and `result[Error][Message]`. Can be used with an optional `otherwise` clause

## List functions

- `List.Generate`
- `List.Accumulate({1, 2, 3}, 0, (x, y) => x + y)`
- `List.Transform({1, 2, 3}, each _ * 2)`

## Common use cases

1. [Decompress a zip file from a web URL](https://community.fabric.microsoft.com/t5/Desktop/How-to-unzip-and-decompress-data-extract-URL-in-PBI-Query-Editor/td-p/3161254)

## Reference

1. [Collect, Combine, and Transform Data Using Power Query in Power BI and Excel, 2nd Edition](http://www.powerquerybook.com/), by Daniil Maslyuk, Gil Raviv
2. [Power Query M formula language](https://learn.microsoft.com/en-us/powerquery-m/)