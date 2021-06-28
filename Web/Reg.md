- g, i, m
| Modifier | Description                                                   |
| -------- | ------------------------------------------------------------- |
| g        | Perform a `global` match                                      |
|          | (find all matches rather than stopping after the first match) |
| i        | Perform `case-insensitive` matching                           |
| m        | Perform `multiline` matching                                  |


- m: match the beginning (^) and end ($) **each** line of a string (delimited by \n or \r)

```javascript
const patt = /^is/m; // Tìm 'is' là bắt đầu của dòng

const result = "\nIs th\nis it?".match(patt); 
// ["is", index: 7, input: "\nIs th\nis it?", groups: undefined, length: 1]
"\nIs th\n is it?".match(patt); // null

const patt1 = /is$/m; // Tìm 'is' là kết thúc của dòng
"Is\nthis\nhis\n?".match(patt1);
// ["is", index: 5, input: "Is\nthis\nhis\n?", groups: undefined, length: 1]

```

- [abc]
  [abcde..] - Any character between the brackets
  [A-Z] - Any character from uppercase A to uppercase Z
  [a-z] - Any character from lowercase a to lowercase z
  [A-z ]- Any character from uppercase A to lowercase z
- [^abc]
