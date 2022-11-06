# regularExpressions

In JavaScript, a **Reg**ular **Ex**pression (RegEx) is an object that describes a sequence of characters used for defining a search pattern. For example,

/^a...s$/

The above code defines a RegEx pattern. The pattern is: **any five letter string starting with** `a` **and ending with** `s`.

A pattern defined using RegEx can be used to match against a string.

| Expression  | String | Matched? |
| ----------- | ------ | -------- |
|             |     `abs`   |     No Match     |
|  |  `alias`      |    Match     |
|    `/^a...s$/`         |   `abyss`     |      Match    |
|             |     `Alias`   |      No Match   |
|             |   `An abacus`     |     No Match     |

---

## Create a RegEx

There are two ways you can create a regular expression in JavaScript.

1.  **Using a regular expression literal:**  
    The regular expression consists of a pattern enclosed between slashes `/`. For example,
    
    ```js
    cost regularExp = /abc/;
    ```
    
    Here, `/abc/` is a regular expression.
2.  **Using the** `RegExp()` **constructor function**:  
    You can also create a regular expression by calling the `RegExp()` constructor function. For example,
    
    ```js
    const reguarExp = new RegExp('abc');
    ```
    

For example,

```js
const regex = new RegExp(/^a...s$/);
console.log(regex.test('alias')); // true
```

In the above example, the string `alias` matches with the RegEx pattern `/^a...s$/`. Here, the `test()` method is used to check if the string matches the pattern.

There are several other methods available to use with JavaScript RegEx. Before we explore them, let's learn about regular expressions themselves.

---

## Specify Pattern Using RegEx

To specify regular expressions, metacharacters are used. In the above example (`/^a...s$/`), `^` and `$` are metacharacters.

---

### MetaCharacters

Metacharacters are characters that are interpreted in a special way by a RegEx engine. Here's a list of metacharacters:

**[] . ^ $ * + ? {} () \ |**

---

**[]** **- Square brackets**

Square brackets specify a set of characters you wish to match.

| Expression | String    | Matched?  |
|------------|-----------|-----------|
|            | `a`         | 1 match   |
| `[abc]`      | `ac`        | 2 matches |
|            | `Hey Jude`  | No match  |
|            | `abc de ca` | 5 matches |

Here, `[abc]` will match if the string you are trying to match contains any of the `a`, `b` or `c`.

You can also specify a range of characters using `-` inside square brackets.

`[a-e]` is the same as `[abcde]`.

`[1-4]` is the same as `[1234]`.

`[0-39]` is the same as `[01239]`.

You can complement (invert) the character set by using caret `^` symbol at the start of a square-bracket.

`[^abc]` means any character except `a` or `b` or `c`.

`[^0-9]` means any non-digit character.

---

. **- Period**

A period matches any single character (except newline `'\n'`).

| Expression | String | Matched?                          |
|------------|--------|-----------------------------------|
|            | `a`    | No match                          |
| `..`       | `ac`   | 1 match                           |
|            | `acd`  | 1 match                           |
|            | `acde` | 2 matches (contains 4 characters) |

---

**^** **- Caret**

The caret symbol `^` is used to check if a string **starts with** a certain character.

| Expression | String | Matched?                                           |
|------------|--------|----------------------------------------------------|
|            | `a`    | 1 match                                            |
| `^a`       | `abc`  | 1 match                                            |
|            | `bac`  | No match                                           |
| `^ab`      | `abc`  | 1 match                                            |
|            | `acb`  | No match (starts with `a` but not followed by `b`) |

---

**$** **- Dollar**

The dollar symbol `$` is used to check if a string **ends with** a certain character.

| Expression | String    | Matched?                                           |
|------------|-----------|----------------------------------------------------|
|            | `a`       | 1 match                                            |
| `a$`       | `formula` | 1 match                                            |
|            | `cab`     | No match                                           |

---

`*` **- Star**

The star symbol `*` matches **zero or more occurrences** of the pattern left to it.

| Expression | String  | Matched?                              |
|------------|---------|---------------------------------------|
|            | `mn`    | 1 match                               |
|            | `man`   | 1 match                               |
| `ma*n`     | `mann`  | 1 match                               |
|            | `main`  | No match (`a` is not followed by `n`) |
|            | `woman` | 1 match                               |

---

**+** **- Plus**

The plus symbol `+` matches one or more occurrences of the pattern left to it.

| Expression | String  | Matched?                              |
|------------|---------|---------------------------------------|
|            | `mn`    | No match (no `a` character)           |
|            | `man`   | 1 match                               |
| `ma+n`     | `mann`  | 1 match                               |
|            | `main`  | No match (`a` is not followed by `n`) |
|            | `woman` | 1 match                               |

---

**?** **- Question Mark**

The question mark symbol `?` matches **zero or one occurrence** of the pattern left to it.

| Expression | String  | Matched?                               |
|------------|---------|----------------------------------------|
|            | `mn`    | 1 match                                |
|            | `man`   | 1 match                                |
| `ma?n`     | `maan`  | No match (more than one `a` character) |
|            | `main`  | No match (`a` is not followed by `n`)  |
|            | `woman` | 1 match                                |

---

**{}** **- Braces**

Consider this code: `{n,m}`. This means at least `n`, and at most `m` repetitions of the pattern left to it.

| Expression | String       | Matched?                          |
|------------|--------------|-----------------------------------|
|            | `abc dat`    | No match                          |
|            | `abc daat`   | 1 match (at `daat`)               |
| `a{2,3}`     | `abc daaat`  | 2 matches (at `aabc` and `daaat`) |
|            | `abc daaaat` | 2 matches (at `aabc` and `daaat`) |

Let's try one more example. This RegEx `[0-9]{2, 4}` matches at least 2 digits but not more than 4 digits.

| Expression | String       | Matched?                          |
|------------|--------------|-----------------------------------|
|            | `ab123csde`  | 1 match (match at `ab123csde`)    |
| [0-9]{2,4} | `abc daat`   | 3 matches (`12`, `3456`, `73`)    |
|            | `abc daaat`  | No match                          |

---

**|** **- Alternation**

Vertical bar `|` is used for alternation (`or` operator).

| Expression | String       | Matched?                          |
|------------|--------------|-----------------------------------|
|            | `cde`        | No match                          |
| a\|b       | `ade`        | 1 match                           |
|            | `acdbea`     | 3 matches (at `acdbea`)           |

Here, `a|b` match any string that contains either `a` or `b`

---

**()** **- Group**

Parentheses `()` is used to group sub-patterns. For example, `(a|b|c)xz` match any string that matches either `a` or `b` or `c` followed by `xz`

| Expression    | String      | Matched?                          |
|---------------|-------------|-----------------------------------|
|               | `ab xz`     | No match                          |
| `(a\|b\|c)xz` | `abxz`      | 1 match (at `abxz`)               |
|               | `axz cabxz` | 2 matches (at `axzbc`and `cabxz`) |

---

`\` - Backslash**

Backslash `\` is used to escape various characters including all metacharacters. For example,

`\$a` match if a string contains `$` followed by `a`. Here, `$` is not interpreted by a RegEx engine in a special way.

If you are unsure if a character has special meaning or not, you can put `\` in front of it. This makes sure the character is not treated in a special way.
