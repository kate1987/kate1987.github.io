# Log Statements Identified by the Lightrun LogOptimizer(™)

The following log statements categories are identified and flagged by the Lightrun LogOptimizer(™).

## Marker logs

Marker logs are log statements with a static message indicating that you have reached a certain point in your code. In some cases, marker logs also contain information that helps to identify the code context. For example,

```java
public String foo(int bar) {
	logger.info("Starting method foo")
	...
	
	logger.info("Querying user {} profile details", user.getId());

	...
	logger.info("Exiting method foo")
	return value;
}
```

Marker logs are only sometimes needed; they simply clog up your logs, hiding the more important information. Marker logs should be removed and replaced with a Lightrun conditional log that is only logged whenever there is important data, like a specific user identifier.

## State reflecting logs

State reflecting logs are log statements used to expose variables' values that might be interesting under certain circumstances. For example, state reflecting logs can be used to expose method input parameters, return values of method calls, data queried from a database, etc.

```py
def countries(language)
	print(f"Processing countries for language {language}")

	with open('countries.json', encoding='utf-8') as data_file:
    countries = json.load(data_file)

	print(f"Read {len(countries)} countries from the JSON file.")

```

State reflecting logs are only relevant when the values returned are not what you expect. Most of the time, the values returned by state reflecting logs are expected; hence not useful. These expected log statements can be very wasteful as data returned from variables or databases can contain lots of information. 

State reflecting logs should be replaced with a Lightrun snapshot which is only activated when the variable value is different from what you expect.  Using a snapshot has additional value as it allows you to easily view more complex variable types such as objects, arrays, and hashes.

## Duplicate log messages

Duplicate log statements are log statements that print out the same data in different variations. Duplicate log statements are usually the result of adding more and more log messages to the same piece of code without noticing what is already logged.

```java
private boolean authorize(User user, Action action) {
	logger.info("User {} is trying to perform action {}", user.getId(), action.getName());

	if (isAdmin(user)) {
		logger.info("User {} has super powers - can perform action {}", user.getId(), action.getName());
		return true;
	}

	...

	logger.info("User {} not allowed to perform action {}", user.getId(), action.getName());
}
```
In such cases, you can remove the redundant log statements and then consider replacing the remaining ones with a Lightrun dynamic log.

## Further reading

- [LogOptimizer(TM) Overview](/logoptimizer/overview/)
- [Get Started with the Lightrun LogOptimizer.](/logoptimizer/quickstart/)
