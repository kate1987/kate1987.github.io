## No code found

The `No code found at line # in <path>` error may occur even if the action (for example, a log) is inserted at a line that contains executable code.

![No code found error](/assets/images/no-code-found-error.png){: style="width:70%"}

**Symptoms and causes**

This error typically happens when inserting a log in a code line that doesn't have executable code. The probable cause of the error is that a log action, in most cases, triggers at the line preceding the log insertion position. If the previous line is empty or contains no executable code, then the `No code found` error is displayed.

**Suggested solution**

Try moving the action insertion position to the line following the one for which the log is intended to trigger.
