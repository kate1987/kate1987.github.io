## Expression not allowed

Lightrun blocks expressions that are considered harmful to your server, can overload the Lightrun agent and server, or expressions that carry a large performance penalty.

This includes:

- Expressions that change the state of your application. i.e., setting object fields, static fields, and changing array elements.
- Expressions that involves calling a native method.
- Expressions involving the creation of a global variable.
- Expressions that implements Division by zero, infinite recursions, out-of-bound reads, and null pointer reference.
- Expressions that halt CPU.
- Expressions that try to access external resources.
