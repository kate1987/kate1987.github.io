!!! Important
	Most Java compilers exclude debugging symbols by default to reduce the generated binary size and improve performance and optimization. This action can prevent Lightrun from working as the Lightrun agent needs to find several symbols, including your project's variables, to insert [Lightrun actions](../actions.md) into your project.

	To ensure that the required debugging information is included in your compiled files, you must add the following debug options to your Java compiler.

	* **-g:source**
	* **-g:lines**
	* **-g:vars**

	You can learn more about the debugging symbols [here](https://www.ibm.com/docs/en/adfz/fafz/14.1?topic=analyzer-compiling-java-optimal-debugging). For more information on specifying debugging symbols in your Maven or Gradle project, see [Build tools (Maven and Gradle)](/jvm/build-tools/)

	*Note - The added debug options do not impact compiler optimization or performance; they only enhance the bytecode with additional debug information.*