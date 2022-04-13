# Cli

The Cli is all about the REPL (Read-Eval-Print Loop)

The repl gets kicked off in main.rs with a call to *evaluate_repl*

In *repl.rs* there is a call to

```rust
let input = line_editor.read_line(prompt);
```

Which grabs the input from the user as a string and then calls *eval_source*.

### eval_source

Eval_source is the most critical piece of code in Nushell.

Its main job is to do two things:

* *parsing* which takes in the user input string and creates a block
* *evaluation* which creates values from pipelines and expressions by calling eval_block
