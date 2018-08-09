# Beanstalk

zip -> beanstalk -> AWS resources
----

* removes/simplifes infra management
* allows SSH access to instances

Apps are the high level structure in beanstalk.

- Entire app is one EB application
- Each logical component of you app, can be a EB app or a EB env within an application.

App can have multiple env or functional type
* single vs scalable
* web servers envs or worker envs
* each app have its own URL, URLs can be swapped between apps

----

* app version are unique packages which represent versions of apps
* app is uploaded to EB as a app bundle - zip
* app can have many versions
* app versions can be deployed to environments within an Application

![alt](./images/beanstalk.png)

## Env types

### web server
- present app to users/interact with outher services, generating outputs for processing
### worker
- process output from other envs

## Apps

* node
* php
* python
* ruby
* tomcat
* .net (IIS)
* java
* go
* packer
docker:
* glassfish
* go
* python
generic:
* docker
* multi-container docker