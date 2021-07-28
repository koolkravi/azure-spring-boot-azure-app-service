# Deploy Spring Boot Application uisng azure app service

## Prerequisite
- [sprig boot application and app registration ](https://github.com/koolkravi/azure-spring-boot-azure-ad/tree/master/oauth-2.0-implicit-code-flow)


## Step 1: Create web app and App Service Plan

All Services- > web -> App Services-> Create Web App
```
RG = koolkwebapp-rg
Web app name: koolkdemo  //.azurewebsites.net
Publish : Docker Container
Runtime stack : Tomcat 9, java 8
Operating System : linux
region : central US

App Service Plan : 
	New App Service Plan name : koolkappservice
	Sku and size : for Prod -> Premium V2 P1v2  (210 total ACU, 3.5 GB memory)
			P1V2  210 total ACU(Azure Compute Units )  3.5 GB memory Dv2-Series compute equivalent 4873.28 INR/Month (Estimated) 
	
create	
```

## Step 2: Deploy WAR file  
```
/home/site/wwwroot

POST request to https://koolkdemo.scm.azurewebsites.net/api/wardeploy

Get and reset app-level credentials 
App Services > <any_app> > Deployment center > FTP/Credentials
Username : 
Password : 
```

## Step 3 : Deploy using ftp - TODO 
```
ref : https://docs.microsoft.com/en-us/azure/app-service/deploy-ftp

All Services->app service - > koolkdemo
Deployment Center > FTP > Dashboard.

FTPS Endpoint : ftps://waws-prod-dm1-129.ftp.azurewebsites.windows.net/site/wwwroot
username : 
password : 
```

## Step 4: Test
koolkdemo | Advanced Tools

When applicationn is deployed as root context
### Testing on local machine
1st application : http://localhost:8091/
                  http://localhost:8091/login/oauth2/code/azure

URL :             https://koolkdemo.azurewebsites.net/
	              https://koolkdemo.azurewebsites.net/demo/login/oauth2/code/azure


## Issues
- 1. Reply url comes as http instead of https - Did not work
```
ref: https://stackoverflow.com/questions/60365017/redirect-url-for-spring-oauth2-app-on-azure-with-active-directory-invalid-redir

fix:
add server.forward-headers-strategy=native in applications.properties

and app registrtation -> manifest -> oauth2AllowIdTokenImplicitFlow  true
									 oauth2AllowImplicitFlow 
```

## Reference

### Deploy your app to Azure App Service with a ZIP or WAR file / using FTP/S 
```
https://docs.microsoft.com/en-us/azure/app-service/deploy-zip
```

###  Spring Boot war Packaging Example
```
https://howtodoinjava.com/spring-boot2/war-packaging-example/
```


