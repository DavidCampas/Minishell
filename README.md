# Minishell

A minimal Bash-like shell written in C, built on GNU Readline: it tokenizes, parses and executes command lines with pipes, redirections, heredocs, environment-variable expansion and a set of built-in commands.

![C](https://img.shields.io/badge/C-00599C?logo=c&logoColor=white)
![Readline](https://img.shields.io/badge/GNU%20Readline-4EAA25?logo=gnu&logoColor=white)
![42 Barcelona](https://img.shields.io/badge/42-Barcelona-000000?logo=42&logoColor=white)

## About

Minishell recreates the core behavior of a Unix shell from scratch. It reads a line with Readline, runs it through a hand-written lexer and parser to build a pipeline of command blocks, then executes each command by forking external binaries (resolved through `PATH`) or dispatching to built-ins. Along the way it handles quoting, variable expansion, multiple redirections, heredocs and interactive signal management, tracking the exit status of the last command like a real shell.

## Features

- Interactive prompt with command history via GNU Readline
- Lexer with single- and double-quote handling and word-boundary detection
- Parser that splits a line into a pipeline of command blocks and their redirections
- Pipes (`|`) chaining an arbitrary number of commands
- Redirections: input (`<`), output (`>`), append (`>>`) and heredoc (`<<`)
- Environment-variable expansion, including `$?` (last exit status), with quote-aware rules
- Built-in commands: `cd`, `echo`, `pwd`, `env`, `export`, `unset`, `exit`
- Environment management: copy, sort and update of the env, plus `PATH` resolution for external commands
- Signal handling (`Ctrl-C`, `Ctrl-\`) for both interactive and child contexts
- Own libft static library and clean, leak-conscious memory management

## Build & run

```bash
# Compile (also builds the bundled libft)
make

# Launch the shell
./minishell

# Other targets
make clean    # remove object files
make fclean   # remove objects and the binary
make re       # rebuild from scratch
```

Requires a C compiler and the GNU Readline development library (`libreadline-dev`).

Example session:

```bash
$ ./minishell
minishell$ echo "hello $USER" | cat -e
hello david$
minishell$ export GREETING=hi
minishell$ echo $GREETING > out.txt && cat < out.txt
minishell$ cat << EOF
> heredoc line
> EOF
```

## Concepts

C, processes & `fork`/`execve`, pipes, file descriptors & redirections, signals, GNU Readline, lexing & parsing, environment variables, memory management, Makefile.

_42 Barcelona · Common Core project._
