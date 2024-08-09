# C# expressions support in .NET agent

As C# developers, leveraging Lightrun's capabilities to integrate C# expressions within actions enhances your debugging efficiency. Proceed to review the supported expressions, Lightrun's processing methods, and considerations regarding limitations.

!!!imp "Important"
    During the evaluation of C# expressions, Lightrun does not modify or affect any application data.

## Supported C# expression types in Lightrun actions

Lightrun facilitates various C# expressions within actions. Supported expressions include:

- **Log format**: Enclose expressions with curly braces to log variable values or method returns during runtime. For example, when adding a log, an expression can appear inside curly braces `({})` such as `My variable` value is `{myVar}` and my method returned `{myMethod()}`, resulting in the printed valiues of the corresponding variable or expression.

- **Conditions**: Utilize standard Boolean expressions within action expressions.
- **Watch expressions**: Query and monitor specific variables and method invocation results during runtime. 

## C# expression guidelines and limitations

### Supported C# syntax

The following C# language syntax is supported when setting expressions in actions:

| Category            | Supported syntax                                                |
|---------------------|-----------------------------------------------------------------|
| Logical Operators   | `\`,`\`, `&&`, `\`, `^`, `&`, `==`, `!=`                                      |
| Comparison Operators| `<`, `>`, `<=`, `>=`                                                    |
| Shift Operators     | `<<`, `>>`                                                           |
| Arithmetic Operators| `+`, `-`, `*`, `/`, `%`                                                    |
| Unary Operators     | `+`, `-`, `!`                                                          |
| Index Operators     | `Array[index]`, `List[index]`, `Dictionary[key]`                      |
| Method Calls        | `Method(args)`, `this.Method(args)`, `object.Method(args)`, `delegate(args)` |
| Field Access        | `Field`, `this.Field`, `object.Field`                                 |
| Property Access     | `Property`, `this.Property`, `object.Property`                        |
| Literals            | `Integer`, `Double`, `Float`, `Character`, `String`, `true`/`false`/`null` literals |

### Interface Duck Typing support

Lightrun offers Interface Duck Typing support for setting C# expressions. This dynamic evaluation process enables expressions like `myVar.myField.myMethod()` to function seamlessly, even if the `myField` field is declared as an object. This flexibility enhances the versatility of the developer’s debugging experience.

As demonstrated in the following example, despite `myField` being declared as an 
Object, Lightrun support for Interface Duck Typing allows the invocation of       
`myMethod()`on `myField`. 

```bash
object myField = new MyClass();
var myVar = new MyContainer(myField);

// Interface Duck Typing supported by Lightrun
var result = myVar.myField.myMethod();
```

### .NET IL Code Instruction limitations

From version 1.32, Lightrun supports a subset of .NET IL code instructions. Instructions involving native pointers are not supported due to their unsafe nature. To ensure safety, Lightrun implements essential operations internally or delegates them directly to the host VM when appropriate.

The following IL code instructions are not supported:

- Operations involving native Ints and pointers, primarily associated with unsafe code:

  - `Ldind_I`
  - `Conv_Ovf_I_Un`
  - `Conv_Ovf_U_Un`
  - `Ldelem_I`
  - `Stelem_I`
  - `Conv_I`
  - `Conv_Ovf_I`
  - `Conv_Ovf_U`
  - `Stind_I`
  - `Arglist`
  - `Ldvirtftn`
  - `Localloc` 

- Operations working with native memory, which cannot be controlled by the Lightrun VM:

  - `Cpblk` 
  - `Initblk` 

- Long arrays, collections, or objects limitation

    Due to performance constraints, Lightrun does not support long arrays, collections, or objects fully. If these data structures exceed certain thresholds, Lightrun may display partial information. To overcome this limitation, it's recommended to use more precise expressions for querying specific data. 

### Type representations limitation

Certain types, such as booleans and chars, lack special representations in IL code and are encoded as integers or unsigned integers. Consequently, in some cases, the type inference process may fail, leading to expressions like `a > b` to be represented as integer `0 or 1` instead of their original types. 
