
### Q1
Describe the difference between the varchar and text data types.

`varchar` holds up a specified number of characters. It fill these characters with spaces if they are unfulfilled. `text` has no limit on how many characters can be stored and as a result has more flexibility.

## Q2
Describe the difference between the integer, decimal, and real data types.

`integer` is a whole number.
`decimal` or `numeric` is a number with a specified length and decimal point precision.
`real` is a floating point numbers that can contain fractional numbers.

## Q3
The largest figure that can be held in integer column is between -2147483648 and +2147483647.

## Q4
Describe the difference between the timestamp and date data types.

`timestamp` includes both the date and time e.g. `YYYY-MM-DD HH-MM-SSSS` whereas `date` only includes the `date` format, `YYYY-MM-DD`

## Q5
Can a time with a time zone be stored in a column of type timestamp?

No it can't but it can be added as `timestamp with time zone` for example:

```SQL
timestamp with time zone PST
```