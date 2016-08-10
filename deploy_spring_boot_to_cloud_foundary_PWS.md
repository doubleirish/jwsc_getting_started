


## To download CF CLI as binary
you can download the CF CLI from  https://github.com/cloudfoundry/cli#downloads
or use the curl command below

```
cd ~/bin
curl -L "https://cli.run.pivotal.io/stable?release=linux64-binary&source=github" | tar -zx
```


## use the spring CLI to create a simple Spring boot webapp
spring init -d=web,actuator,hateoas --package=edu.uw.jwsc -groupId=edu.uw.jwsc -name=hello hello
cd hello

## run the app  
 mvn spring-boot:run

## test app
http://localhost:8080/actuator
 
## build Spring boot app 
mvn package


## Login to CF /Select a target 
```
cf login -a https://api.run.pivotal.io -u <your_pws_username_aka_email>  
```
it will ask for a password and choose a default organization and space e.g development



## Deploy your application  
```
 cf push hello-world-double-irish -p target/hello-0.0.1-SNAPSHOT.jar
``` 
near the end of the deploy logs , you will evntally see a line that begins with  "urls :" 
e.g 
```
urls: hello-world-double-irish.cfapps.io
```

## Test Cloud app in browser 
Access your app by entering the following URL into your browser:
http://hello-world-double-irish.cfapps.io/actuator

## View Cloud app in the Web console
https://console.run.pivotal.io


 
## Stop and Delete your Cloud webapp
you may want to stop and delete your application using the PWS web console 
so you don't get charged 


## Other references 
https://spring.io/guides/gs/sts-cloud-foundry-deployment/


https://docs.run.pivotal.io/starting/
