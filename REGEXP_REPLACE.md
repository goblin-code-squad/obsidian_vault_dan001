
```
REGEXP_REPLACE
     (
      string_expression,
      pattern_expression [, string_replacement [, start [, occurrence [, flags ] ] ] ]
     )
```


Returns a modified source string replaced by a replacement string, where the occurrence of the regular expression pattern found. If no matches are found, the function returns the original string.

syntaxsql

```
REGEXP_REPLACE
     (
      string_expression,
      pattern_expression [, string_replacement [, start [, occurrence [, flags ] ] ] ]
     )
```

Note

Regular expressions are available in Azure SQL Managed Instance with the **SQL Server 2025** or **Always-up-to-date** [update policy](https://learn.microsoft.com/en-us/azure/azure-sql/managed-instance/update-policy).

[](https://learn.microsoft.com/en-us/sql/t-sql/functions/regexp-replace-transact-sql?view=sql-server-ver17#arguments)

## Arguments

[](https://learn.microsoft.com/en-us/sql/t-sql/functions/regexp-replace-transact-sql?view=sql-server-ver17#string_expression)

#### _string_expression_

An expression of a character string.

Can be a constant, variable, or column of character string.

Data types: **char**, **nchar**, **varchar**, or **nvarchar**.

Note

The `REGEXP_LIKE`, `REGEXP_COUNT`, `REGEXP_INSTR`, and `REGEXP_SUBSTR` functions support LOB types (**varchar(max)** and **nvarchar(max)**) up to 2 MB for the _string_expression_ parameter.

[](https://learn.microsoft.com/en-us/sql/t-sql/functions/regexp-replace-transact-sql?view=sql-server-ver17#pattern_expression)

#### _pattern_expression_

Regular expression pattern to match. Usually a text literal.

Data types: **char**, **nchar**, **varchar**, or **nvarchar**. _pattern_expression_ supports a maximum character length of 8,000 bytes.

[](https://learn.microsoft.com/en-us/sql/t-sql/functions/regexp-replace-transact-sql?view=sql-server-ver17#string_replacement)

#### _string_replacement_

String expression that specifies the replacement string for matching substrings and replaces the substrings matched by the pattern. The string_replacement can be of char, varchar, nchar, and nvarchar datatypes. If an empty string (`''`) is specified, the function removes all matched substrings and returns the resulting string. The default replacement string is the empty string (`''`).

The string_replacement can contain \n, where n is 1 through 9, to indicate that the source substring matching the n'th parenthesized group (subexpression) of the pattern should be inserted, and it can contain `&` to indicate that the substring matching the entire pattern should be inserted. Write \ if you need to put a literal backslash in the replacement text.

For example

SQL

```
REGEXP_REPLACE('123-456-7890', '(\d{3})-(\d{3})-(\d{4})', '(\1) \2-\3')
```

Returns:

Output

```
(123) 456-7890
```

If the provided `\n` in `string_replacement` is greater than the number of groups in the _pattern_expression_, then the function ignores the value.

For example:

SQL

```
REGEXP_REPLACE('123-456-7890', '(\d{3})-(\d{3})-(\d{4})', '(\1) (\4)-xxxx')
```

Returns:

Output

```
(123) ()-xxxx
```

[](https://learn.microsoft.com/en-us/sql/t-sql/functions/regexp-replace-transact-sql?view=sql-server-ver17#start)

#### _start_

Specify the starting position for the search within the search string. Optional. Type is **int** or **bigint**.

The numbering is 1-based, meaning the first character in the expression is `1` and the value must be `>= 1`. If the start expression is less than `1`, returns error. If the start expression is greater than the length of _string_expression_, the function returns _string_expression_. The default is `1`.

[](https://learn.microsoft.com/en-us/sql/t-sql/functions/regexp-replace-transact-sql?view=sql-server-ver17#occurrence)

#### _occurrence_

An expression (positive integer) that specifies which occurrence of the pattern expression within the source string to be searched or replaced. Default is `1`. Searches at the first character of the _string_expression_. For a positive integer `n`, it searches for the `nth` occurrence beginning with the first character following the first occurrence of the _pattern_expression_, and so forth.

[](https://learn.microsoft.com/en-us/sql/t-sql/functions/regexp-replace-transact-sql?view=sql-server-ver17#flags)

#### _flags_

One or more characters that specify the modifiers used for searching for matches. Type is **varchar** or **char**, with a maximum of 30 characters.

For example, `ims`. The default is `c`. If an empty string `(' ')` is provided, it will be treated as the default value `('c')`. Supply `c` or any other character expressions. If flag contains multiple contradictory characters, then SQL Server uses the last character.

For example, if you specify `ic` the regex returns case-sensitive matching.

If the value contains a character other than those listed at [Supported flag values](https://learn.microsoft.com/en-us/sql/t-sql/functions/regexp-replace-transact-sql?view=sql-server-ver17#supported-flag-values), the query returns an error like the following example:

Output

```
Invalid flag provided. '<invalid character>' are not valid flags. Only {c,i,s,m} flags are valid.
```

[](https://learn.microsoft.com/en-us/sql/t-sql/functions/regexp-replace-transact-sql?view=sql-server-ver17#supported-flag-values)

##### Supported flag values

|Flag|Description|
|---|---|
|`i`|Case-insensitive (default `false`)|
|`m`|Multi-line mode: `^` and `$` match begin/end line in addition to begin/end text (default `false`)|
|`s`|Let `.` match `\n` (default `false`)|
|`c`|Case-sensitive (default `true`)|

[](https://learn.microsoft.com/en-us/sql/t-sql/functions/regexp-replace-transact-sql?view=sql-server-ver17#return-value)

## Return value

Expression.

(https://learn.microsoft.com/en-us/sql/t-sql/functions/regexp-replace-transact-sql?view=sql-server-ver17#examples

## Examples

Replace all occurrences of `a` or `e` with `X` in the product names.

SQL

```
SELECT REGEXP_REPLACE(PRODUCT_NAME, '[ae]', 'X', 1, 0, 'i')
FROM PRODUCTS;
```

Replace the first occurrence of `cat` or `dog` with `pet` in the product descriptions

SQL

```
SELECT REGEXP_REPLACE(PRODUCT_DESCRIPTION, 'cat|dog', 'pet', 1, 1, 'i')
FROM PRODUCTS;
```

Replace the last four digits of the phone numbers with asterisks

SQL

```
SELECT REGEXP_REPLACE(PHONE_NUMBER, '\d{4}$', '****')
FROM CUSTOMERS;
```