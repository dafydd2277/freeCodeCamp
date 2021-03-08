# Regular Expressions

- [link][]

`myString = 'An arbitrary string'`
`myRegex = /An unquoted pattern/`

`myRegex.test(myString);` or `myString.match(myRegex)`, whichever makes more
sense in context.

- [Greedy and Lazy matching][greedy]
- Class shortcuts.
    /\w/ === /[a-zA-Z0-9_]/
    /\W/ === /[^a-zA-Z0-9_]
    /\d/ === /[0-9]/
    /\D/ === /[^0-9]/
    /\s/ === /[ \r\t\f\n\v]/
    /\S/ === /[^ \r\t\f\n\v]/
- [Username restrictions][username]
- Use `\1` - `\9` for paren-wrapped matches.
- Replacment:
    `myReplace = 'Replacement text'`
    `myString.replace(myRegex, myReplace)`

In this case, paren-wrapped matches are given in the replacment strings with
`$1`, `$2`, etc.


[greedy]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/regular-expressions/find-characters-with-lazy-matching
[link]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/#regular-expressions
[username]: https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/regular-expressions/restrict-possible-usernames
