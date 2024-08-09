# Lightrun for Gunicorn

To run a Gunicorn WSGI HTTP server with the Lightrun agent, follow these steps:

1. In your application folder, install the Python agent by running `python -m pip install lightrun`.
2. Add the following code to your application's `.py` file.
	```python
	try:
		import lightrun
		lightrun.enable(com_lightrun_server=<company_url>, company_key=<company_key>)
	except ImportError as e:
			print("Error importing Lightrun: ", e)
	```
3. Run your Gunicorn application as normal.

!!! important
	The Lightrun import statement must be outside your function but in the same file.

!!! Note
    If you are running Gunicorn inside a framework, add the Lightrun import statement to your `wsgi.py` file and run the file with Gunicorn.