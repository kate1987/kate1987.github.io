#### Counter

An example Lightrun Counter output is shown in the code sample below:

```bash
CounterData Log{counterId='9b1e6b80-b5ec-42dd-b411-28bbb3e44059', name=counter1::*, count=751, m1_rate=49.51307448246653, m5_rate=53.94779140968095, m15_rate=54.77571845490024, mean_rate=35.71689054874403}
```

The following table describes the data present in a Counter output.

| Column| Description |
|-------|-------------|
| counterId | A unique identifier assigned to the counter by the system. |
| name | The counter label. |
| count | The number of times the specified code was executed (hit count). |
| m1_rate | The average amount of counter metrics hit recorded per second for one minute. |
| m5_rate | The average amount of counter metrics hit recorded per second for five minutes. |
| m15_rate | The average amount of counter metrics hit recorded per second for fifteen minutes. |
| mean_rate | The mean rate of hits recorded per second during the entire duration of the Lightrun action. |


#### Time measurements

An example Lightrun Time measurement output is shown in the code sample below:

```bash
TicToc Log {TicTocId='670a505f-33c1-4c8c-846b-57afaa9a236c', name='MeasurementName', count='17', max='5', min='0', mean='0.46618461992518356', stddev='1.1864864756822397'}
```

The following table describes the data present in a Time measurement output.

| Column| Description |
|-------|-------------|
| TicTocId | A unique identifier assigned to the time measurement by the system. |
| name | The time measurement label. |
| count | The number of times the specified code was executed. |
| max | Maximum amount of time measured by the time measurement metric in milliseconds. |
| min | Minimum amount of time measured by the time measurement metric in milliseconds.|
| mean | Mean amount of time measured by the time measurement metric in milliseconds. |
| stddev | Standard deviation of the times recorded by the time measurement metric. |

!!! note 
	- When you create a time measurement metric, Lightrun measures the execution time of the code you’ve selected not just once but every time a thread passes through the specified code. For various reasons, like the CPU being busy with different things at a time, this often results in a slightly different execution time for each code invocation. Lightrun’s time measurement metrics data includes not just one number but enough data to understand how much time is spent in that part of your code. 
	- Lightrun time measurement metrics output is not displayed for each invocation; instead, the recorded time measurement data is sent to your configured output target (Plugin or Stdout) every second. This ensures that the system collecting and processing the data, typically a time series database like Prometheus, will have a constant stream of data to process. This also means you’ll see Time measurements data being produced regularly, even when the code isn’t executed.
