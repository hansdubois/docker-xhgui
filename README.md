#XHGUI Docker container. 

This is a docker container running XHGUI with PHP 7.

## Running the container as daemon:
To run XHGUI run the following command:
```
docker run -p <YOUR_PORT_NUMBER>:80 -d hansdubois/xhgui
```

## Running the box with docker compose sharing profiles:
You can run XHGUI next to your PHP container by adding them to docker compose.
To import the profiles you need to share the volumes between the PHP container and XHGUI. 

An example configuration:
```
 php:
   image: <YOUR_PHP_IMAGE>
 xhgui:
    image: hansdubois/xhgui
    volumes:
      - ./profile:/var/www/xhgui/profiles
    ports:
     - <YOUR_PORT_NUMBER>:80
```

This assumes you have a ```profile``` folder in your project where it stores the profiles from XHGUI

## Importing the report in XHGUI
To view the report you first need to import in into XHGUI by executing the following code, to do so you first need to 
  find the id of the docker container where XHGUI is running on by executing the following code on the command line.

```
docker ps

CONTAINER ID        IMAGE                 COMMAND                 
**************************************************************************************
90cfbe04ef9f        hansdubois/xhgui      "docker-php-entryp..."  <------- Here it is 
```

Then execute the following:
```
docker exec -it <DOCKER_CONTAINER_ID> php /var/www/xhgui/external/import.php -f /var/www/xhgui/profiles/<NAME_OF_YOUR_PROFILE>
```

## Viewing the reports in XHGUI
The report can be viewed with XHGUI which is available on:
```
http://localhost:<YOUR_PORT_NUMBER>
```
