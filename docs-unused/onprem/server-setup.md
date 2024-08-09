
# Launch the Management server 

The Lightrun Management server works best in a container environment. 

!!! note 
     The Management server defaults to port 8080 and requires HTTPS so the URL should look like this: [https://192.168.1.108:8080/](https://192.168.1.108:8080/)


!!! imp "Important"
     If port 8080 is already in use, change the port number from the docker-compose file.
     Be sure to change the port number if you changed the configuration from your docker-compose file. 
     SSL certificates can be applied to domains only. Therefore, the page loads with an HTTPS warning for on-premises installations.



Run the Management server on any host using `docker-compose` or any other container orchestration tool such as Kubernetes, Docker Swarm or Rancher etc. Copy the two `yml` files provided to you from Lightrun into an empty directory and execute them as follows: 

```
cd {docker-compose-directory}
docker-compose up -d
```

