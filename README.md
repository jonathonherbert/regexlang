# regex-utils

A few experimental utilities to help users read and write regular expressions, with a particular focus on users who do not write code for a living, and/or do not routinely use them.

## Why?

Regular expressions are notoriously difficult to write and maintain, especially for newcomers:
1. The syntax is terse, and in most cases not possible to derive from plain English (target users maybe remember that parentheses introduce a group, but are less likely to remember that `?:` marks it as non-capturing.)
2. Regular expressions are expressed as linear strings, making it difficult to express structure (heirarchy, different sections) without resorting to programming techniques that are environment-dependent.
3. It's not clear that what's written is correct.

See individual projects for more information:

- [regex-lang](./projects/regex-lang/README.md), a grammar for writing regular expressions in something closer to English
- [regex-explain](./projects/regex-lang/README.md), a program for explaining regular expressions in a way that is clearer to non-technical users
- [regex-matches](./projects/regex-lang/README.md), a program for showing the strings, or a subset of those strings, that a regular expression can match.

## regex-lang

`regex-lang` aims to help with 1.) and 2.) by providing a way of writing regular expressions that is closer to English:
1. Because it's easier to remember `or` than `|`, or `grouped as` than `(?:`, users can more easily discover and recognise features. An intellisense environment, or something similar,  will be necessary to help the user understand what is possible in a given context.
2. Permitting newlines and indentation allows the user to structure parts of the expression in ways that more closely match its structure.

Producing something readable as the complexity of the expression grows is difficult. Consider the expression `Camilla,? (Parker ?-?Bowles|the? Queen Consort)`. To produce this expression, the current grammar looks like:

```
'Camilla' then maybe ',' then ' ' then ('Parker' then maybe ' ' then maybe '-' then 'Bowles' or maybe 'the' then ' Queen Consort')
```

Structuring this makes it slightly easier to read:

```
'Camilla'
    then maybe ','
    then ' '
    then (
        'Parker'
        then maybe ' '
        then maybe '-'
        then 'Bowles'
        or maybe 'the'
        then ' Queen Consort'
    )
```

My hunch is that expressing an [FSA](https://en.wikipedia.org/wiki/Finite-state_machine) in natural language is an inherently problematic thing to do. Perhaps a better way forward is to produce tools that help users write regexes as they are ([regex-explain](../regex-explain/README.md), [regex-possibilities](../regex-explain/README.md).)
