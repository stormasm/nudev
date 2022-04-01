# Parser

The parser creates Expressions...   
There are no Values in the parser.

The file parse_keywords.rs simply are helper functions for the parser...

There are different ways to understand how the parser works in the outside world meaning other how other crates inside nushell uses the parser.

The simplest way to see where the parser is referenced is to:

```rust
rg nu_parser
```

One fairly clean example is inside formats/from/nuon:

```rust
let (lexed, err) = nu_parser::lex(string_input.as_bytes(), 0, &[b'\n', b'\r'], &[], true);
error = error.or(err);

let (lite_block, err) = nu_parser::lite_parse(&lexed);
error = error.or(err);

let (mut block, err) = nu_parser::parse_block(&mut working_set, &lite_block, true, &[]);
error = error.or(err);
```
