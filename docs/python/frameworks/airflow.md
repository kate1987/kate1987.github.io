# Lightrun for Apache Airflow

To run Lightrun for Python with Apache Airflow you must select one or more  tasks in the DAG that you want to debug.

**Instructions**

1. With the same Python interpreter used by Airflow, install the Python agent, by running `python -m pip install lightrun`.
2. Within your Airflow task definition, add the `@lightrun_airflow_task` decorator; for example:

    ~~~py
    @lightrun_airflow_task(company_key="1111-2222-3333")
    def foo():
        # Do something
        pass
    ~~~

!!! note

    To import the decorator, add following line:
      
    ```py
    from lightrun.decorators import lightrun_airflow_task
    ```

## Decorator parameters

The following table lists the available parameters for the `lightrun_airflow_task` decorator.

|Parameter|Explanation|
|------|------|
|`company`| The Lightrun registered company to which the user belongs. Must be supplied with either this parameter or the `LIGHTRUN_COMPANY` environment variable.|
|`company_key`| The company's secret API key. Must be supplied  with either this parameter or the `LIGHTRUN_KEY` environment variable.|
|`config_path`| [Optional] The filesystem path of a configuration for the lightrun agent|
|`initial_sleep_ms`| The time, in milliseconds, to sleep after initializing the agent. If this parameter is set to a low value, the agent might have insufficient time to initialize before the task begins execution, which will result in missing breakpoints inserted in lines that are executed before the agent finishes initialization.|

!!! info "You may need more agents"
    A separate agent is required for each Airflow task that you want to apply simultaneously with other tasks. <a href="mailto:support@lightrun.com" target="_blank"> Contact us</a> if you need more agents.
