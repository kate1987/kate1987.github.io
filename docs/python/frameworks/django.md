# Lightrun for Django

To run a Django web server with the Lightrun agent, follow these steps:

1. In your application folder, install the Python agent by running `python -m pip install lightrun`
2. Add the following code to your `manage.py` file:

    ```python
    try:
        if os.environ.get('RUN_MAIN') or '--noreload' in sys.argv:
            import lightrun
             lightrun.enable(company_key="<COMPANY_SECRET>")
    except ImportError as e:
        print("Error importing Lightrun: ", e)
    ```

3. Run your Django application as normal.

!!! info

    An alternative `enable()` argument is: 
    
    ```bash
    lightrun.enable(com_lightrun_server="https://<SERVER_DOMAIN>/")/company_key<COMPANY_SECRET>
    ```
