# Lightrun for Celery

To run Celery with the Lightrun agent, follow these steps:

1. In your application folder, install the Python agent by running `python -m pip install lightrun`.
2. Add the following to the `.py` file where Celery is initiated (where there is a call to `Celery()`, usually `celery.py`).
    ```python
    from celery.signals import task_prerun

    @task_prerun.connect()
    def task_prerun(**kwargs):
        try:
            import lightrun
            lightrun.enable(company="<COMPANY_NAME>" , company_key="<COMPANY_SECRET>")
        except ImportError as e:
            print("Error importing Lightrun: ", e)
    ```
3. Run your Celery processes as normal.

!!! note
    The Celery `task_prerun` signal dispatch before a task is executed. This signal ensures that a Lightrun agent has been created before the Celery task is executed.

!!! Imp
    You might need to provide the `lightrun_extra_class_path` configuration parameter to ensure that Lightrun is able to index all the functions.

