# Parser

The parser creates Pipelines and Expressions and stores them in a Block.

There are no Values in the parser.

Once the parser creates the block it is passed along to the evaluation
step whose job it is to evaluate these blocks and create Values which
can be displayed to the user in different ways.

The file parse_keywords.rs simply are helper functions for the parser...

There are different ways to understand how the parser works in the outside world meaning how other how other crates inside Nushell uses the parser.

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
