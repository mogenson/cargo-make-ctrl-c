# cargo-make-ctrl-c
dummy project to demonstrate an issue for cargo-make

### Contents of Makefile.toml

```
# run cargo make debug-1, 2, or 3 to launch GDB
# type run to start program
# Ctrl-C should halt the program
# instead it kills cargo-make and leave GDB orphaned

[tasks.debug-1]
dependencies = ["build"]
command = "rust-gdb"
args = ["./target/debug/cargo-make-ctrl-c"]

[tasks.debug-2]
dependencies = ["build"]
command = "sh"
args = ["-c", "rust-gdb ./target/debug/cargo-make-ctrl-c"]

[tasks.debug-3]
dependencies = ["build"]
script = ["rust-gdb ./target/debug/cargo-make-ctrl-c"]
```

### Update

```
# this task runs GDB correctly
# it abuses the script command which swallows Ctrl-C
[tasks.debug-4]
dependencies = ["build"]
script = ["script -q /dev/null -c 'rust-gdb ./target/debug/cargo-make-ctrl-c'"]
```
