# WLS on Docker

### Prerequisites

- You need to have a docker account.  Set up an account [here](https://hub.docker.com/signup).

### Downloading the image:

- Navigate to the WLS Docker image on docker Hub:

  - https://hub.docker.com/_/oracle-weblogic-server-12c

  "Proceed to checkout" and check required boxes to get to the actual page with the download link

  ![image-20191209221349230](/Users/jleemans/dev/github/how_to_by_jan/image-20191209221349230.png)

- Before pulling down the image, be sure to log into docker : 

  ```
docker login
  ```
  
  
  
- Now pull down the image :

  ```
docker pull store/oracle/weblogic:12.2.1.3-dev-190111
  ```
  
  



### Running the container

- Create a local file called **domain.properties** with following content :

```
username=weblogic
password=welcome1
```

- Run the container : 

```
docker run -d -p 7001:7001 -p 9002:9002 \
      -v $PWD:/u01/oracle/properties store/oracle/weblogic:12.2.1.3-dev-190111
```

- Validate the WLS domain is running by connecting to the admin console : 
  
  https://localhost:9002/console/

  - You will have to ackowledge a security exception
  - Wait for the admin console to start, and log in with the username / password you specified

### Run a Sample application

Now let's deploy a very simple sample app.

- Download the war file : https://github.com/AKSarav/SampleWebApp/raw/master/dist/SampleWebApp.war.  See [here](https://www.middlewareinventory.com/blog/sample-web-application-war-file-download/) for more info on this application.
  - 
- In the WLS console, navigate to "Deployments"

- Click "Install"
  - Use the "Upload your file" link in the "Note" text to upload the war file you downloaded before
  - Hit Next, choose the default 'Install as application" option, then Finish
  - Check parameters in the "Testing" tab, you should see your app deployed on 7001/SampleWebApp

- Now access the app in your browser : http://localhost:7001/SampleWebApp/

Other samples can be found here : https://github.com/oracle/docker-images/tree/master/OracleWebLogic/samples