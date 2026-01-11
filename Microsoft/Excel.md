# Excel

Despite being more than 40 years old, Microsoft Excel remains one of the most widely used applications in the world because it continues to evolve. Below is a summary of some of the latest and most impactful features.

## Dynamic Array Formulas

| Lookup  | Lambda    | Shaping    | Summarizing | Miscellaneous |
|---------|-----------|------------|-------------|---------------|
| XLOOKUP | LAMBDA    | VSTACK     | FILTER      | LET           |
| XMATCH  | MAP       | HSTACK     | SORT        | SEQUENCE      |
|         | REDUCE    | TOROW      | SORTBY      | RANDARRAY     |
|         | SCAN      | TOCOL      | UNIQUE      | STOCKHISTORY  |
|         | BYROW     | WRAPROWS   | GROUPBY     |
|         | BYCOL     | WRAPCOLS   | PIVOTBY     |
|         | MAKEARRAY | TAKE       |
|         | ISOMITTED | DROP       |
|         |           | CHOOSEROWS |
|         |           | CHOOSECOLS |
|         |           | EXPAND     |

Since Excel introduced dynamic arrays that spill multiple values into adjacent cells, the use of legacy Control-Shift-Enter formulas has become obsolete.

## Python in Excel 🐍

`=PY()` function allows users to run Python code directly within Excel cells, enabling advanced data analysis and visualization capabilities.

However, it requires an internet connection, executes more slowly due to cloud-based processing , supports only a limited set of Python packages, with no access to local files, or databases.