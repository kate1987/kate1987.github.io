# Known Issues

The following documentation lists the set of known issues in the Lightrun components - Lightrun Server, Lightrun  Agents and Lightrun Plugins, including the version in which they were discovered, and the version in which they were fixed (if relevant). 

## Known issues and limitations

When considering an upgrade to your system, we recommend that you review the Known Issues below to help you determine which is the right upgrade for your system.

The following table lists the issues found in the Lightrun product per Lightrun component.

| Known Issues/Limitations                               | Lightrun component | Description                                                                                                                              | Found in release  | Fix version  |
|---------------------------------------------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------|-------------------|--------------|
| IIS on .NET limitation| .NET Agent| `DebugType` portable was supported on IIS using a workaround. |1.36.2 and lower | 1.36.3|
| .NET Agent installation | .NET Agent| An internal issue related to the .NET agent.| 1.36.0| 1.36.1|
| Java Agent | Java Agent| An internal issue related to the Java Agent in JetBrains. | 1.34.x| 1.35.2, 1.34.4|
| .NET Agent  | .NET Agent|An internal issue related to the .NET agent.| 1.34.x| 1.35.2|
| Python 3.11.0 limitation | Python Agent| Only one active action is permitted within a code object at any given time. | 1.27||
| Python 3.11.0 limitation | Python Agent| Actions can't be added to Generator funtions. | 1.27||
| Python 3.11.0 limitation | Python Agent| The `dis.dis()` function, serving as a disassembler for Python bytecode functions, may produce incorrect results in specific scenarios, after adding an action to a corresponding code object. | 1.27||
| Python 3.11.0 limitation | Python Agent| Actions within nested functions will only be triggered during executions of their 'outer' functions that occur after the action has been added.| 1.27||
| Lightrun Action limitations| .NET Agent| Actions cannot be added to constructors.| 1.26| | |
| Lightrun Action limitations| .NET Agent| Cannot watch for a property defined on an interface.| 1.26| | |
|Lightrun expression limitations |.NET Agent| HashSet content cannot be viewed. |1.26| 1.31|
|Lightrun expression limitations |.NET Agent| Properties with code in the getter functions are only collected when they are requested in evaluated expressions.|1.26| |
| Lightrun expression limitations| .NET Agent | .Net agent does work when the application is executed by the IDE. |1.26 |
| Unable to select agent pools while indexing is running | JetBrains Plugin | During IntelliJ's indexing, selecting Lightrun agent pools is not possible. However, you can select agent pools once indexing has completed. | 1.26 | 1.33 <br> See <br> [Profile Chaining](/dotnet/profile-chaining/).|
| Data Delay & actions cannot be viewed when there is a source mismatch | JetBrains Plugin | When a source mismatch occurs, users will experience a data delay. Action results will not be viewable.                                | 1.24 and lower    | 1.25         |
| Debugging decompiled Java classes is not supported         | Java Agent         | Debugging decompiled Java Classes is not supported. This limitation becomes relevant when you lack the source code.                     | All Lightrun versions | Not applicable |
| Java agent not supported on CentOS 7.0 | Java Agent | The Java agent is not functional on CentOS version 7.0  | 1.23 - 1.26 | 1.27|
| PII redaction is not supported for certain runtime versions | Python Agent, Node.js Agent | Agent side PII redaction is not supported for the following runtimes: <br> - Python version 3.8 and lower <br>- NodeJS version 10.0.0 and 11.0.0 | 1.22  |
| GraalVM 21 compatibility limitation                     | Java Agent         | Lightrun and GraalVM are compatible as long as GraalVM is used only as a JVM and does not include GraalVM native images.                  | All Lightrun versions |               |
| Python Alpine Linux  limitation| Python Agent| Running the Python agent on Alpine Linux failed. Note that new version requires installing dependencies prior to installing the agent.| 1.8|1.30|
| `babel-watch` npm package is not supported | Node.js Agent| Lightrun Node.js agents do not work with Node.js applications loaded using [babel-watch](https://www.npmjs.com/package/babel-watch).| All Lightrun versions |
