# Configure Lightrun with Google App Engine

Google App Engine is the umbrella name for two distinct cloud hosting services from Google:

* Standard environment - everything is managed by Google
* Flexible environment - a bit more flexibility in terms of what you can do. Based on Docker

The standard environment isn't supported by Lightrun since there is no access to the underlying JVM. 

Flexible environment is essentially a docker install and can be used via the same process as outlined [here](../../docker.md).
