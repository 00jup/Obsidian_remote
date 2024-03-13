### Terminal Command Operators: `|` vs `&&`

- **Pipeline (`|`)**: Used to pass the output of one command as input to another.
  - Example: `command1 | command2`
  - `command2` is executed with the output of `command1` as its input.

- **AND Operator (`&&`)**: Used to execute a command only if the preceding command is successful.
  - Example: `command1 && command2`
  - `command2` is executed only if `command1` completes successfully (without errors).