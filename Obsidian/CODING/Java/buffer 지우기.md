### When using `Scanner.nextLine()`

- **Newline character handling**: The `Scanner.nextLine()` method consumes the newline character `\n` entered by the user by pressing Enter. Because of this, the input buffer is cleared from the newline character after the method call.
- **Buffer state**: After method execution, the input buffer does not contain newline characters and is initialized for the next input.

### When using `Scanner.next()`, `Scanner.nextInt()`, etc.

- **Newline handling**: These methods do not consume newline characters. Therefore, if you call `Scanner.nextLine()` after any of these methods, any remaining newline characters will be immediately read by `nextLine()`, resulting in it appearing as if `nextLine()` was skipped without input. You can.
- **Buffer status**: After using methods such as `Scanner.next()`, `Scanner.nextInt()`, a newline character remains in the buffer, and when `Scanner.nextLine()` is called later, this newline character is used. is consumed immediately.

Scanner.nextLine()을 사용하면 버퍼가 지워진다.