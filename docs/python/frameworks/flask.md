# Lightrun for Flask

To run a Flask web app with the Lightrun agent, follow these steps:

1. In your application folder, install the Python agent by running `python -m pip install lightrun`
2. Add the following code to your application's main `init.py` or `app.py` (The import statement must be added to  the main code, not to a specific routed method):

   ```python
   try:
       import lightrun
       lightrun.enable(company_key="<COMPANY_SECRET>")
   except ImportError as e:
       print("Error importing Lightrun: ", e)

   # Example route
   @app.route("/")
   def hello_world():
   return "Hello world!"
   ```
