# Command Line


## Getting Help

On the command line, help is always at hand: you can either type `man <command>` or `<command --help>` to receive detailed documentation about the command in question.

## Directories

`pwd` -> Display path of current working directory.
`cd <directory>` -> Change directory to `<directory>`.
`cd ..` -> Navigate to parent directory.
`ls` -> List directory contents
`ls -la` -> List detailed directory contents, including hidden files.
`mkdir <directory>` -> Create new directory named `<directory>`.

## Output

`cat <file>` -> Output the contents of `<file>`.
`less <file>` -> Output the contents of `<file>` using the less command (which supports pagination etc.).
`head <file>` -> Output the first 10 lines of `<file>`.
`<cmd> > <file>` -> Direct the output of `<cmd>` into `<file>`.
`<cmd> >> <file>` -> Append the output of `<cmd>` to `<file>`.
`<cmd1> | <cmd2>` Direct the output of `<cmd1>` to `<cmd2>`.
`clear` -> Clear the command line window.