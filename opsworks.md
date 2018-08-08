# OpsWorks

App mgmt service using chef.

![alt](./images/opsworks.png)

automation:
- scale on time or load
- monitoring
- permissions and policy management

Chef server stores recipes as well as other config data

Client is installed on each server, VM, container, or networking device (nodes). Client polls server for latest policies.

- Stacks
  ```
  Container of resources, ELBs, EC2, RDS
  ```
  - can't mix linux and windows
  - can't change VPC/Region
  - default OS can be changed, but applies to new instances only
- Layers
  ```
  Layer exists within a stack and consists of things like a web app layer, app processing layer or database layer
  Create layer -> opsworks takes care of provisioning/configuring resources
  ```
  - types
    - opsworks
    - ECS
    - RDS
      ```
      For integration with existing RDS databases
      RDS instance can only be associated with one OPSWorks stack (?)
      Stack clone operation doesn't copy an existing RDS instance
      ```
  - 1 or more layers in the stack
  - instance must be assigned to a least 1 layer
  - which chef layers run, are determined by the layer the instance belongs to
  - preconfigured layers include:
    - Apps
    - DBs
    - ELBs
    - Caching
  - multiple apps per stack and per layer
- OpsWorks instances
- OpsWorkd Application
- Resources
  ```
  In this section you can register already existing resources (Elastic IP's, Volumes, RDS)
  ```

Under the hood:
- OpsWorks Agent (CHEF)
  - machine config
- OpsWorks automation engine
  - creating/updating/deleting various AWS infra
  - handling LB
  - autoscaling
  - auto healing
  - lifecycle events

![alt](./images/chef-recipy-example.png)

## Instances

Instance types:
- 24/7 instances
- time based instances
- load based instances
    - first setup per-layer scaling configuration

## Lifecycle events

### Events:

- Setup
  ```
  Event occurs when an instances has finished booting
  Like install PHP/Apache
  ```
- Configure
  ```
  When: Enters/Leaves online, EIP associate/disassociate, LB attach/detach
  Runs on all instances (in all layers)
  ```
- Deploy
  ```
  App deploy to layer instances
  ```
- Undeploy
  ```
  ```
- Shutdown
  ```
  Graceful shutdown before termination
  ```

Events can be manually executed by the stack `run` command functionality. When event occurs, opsworks runs the set of recipes assigned to that event. Each layer has its own recipes for each event.

## Applications

- App name
- Document Root
- Data srouces
- Application srouce (git/http/s3)
- Env variables
- Domain names
- SSL settings

Deploy:
- executues deploy recipes
- application-id passed to the command
- app params are passed into the chef env
- deploy recipe accesses the app source info and pulls the app payload onto instance
- 5 versions of the app are maintained, current and four historic

## Create-deployment command

`aws opsworks --region abc create-deployment`

- `--stack-id`
- `--app-id`
- `--instance-ids`
- `--comment`
- `--generate-cli-skeleton`
- `--cli-input-json`
- `--command`
  * install_dependencies/update_dependencies
  * upgrade_operating_system (RHEL/Amazon Linux)
  * update_custom_cookbooks
  * execute_recipies
  * configure
  * setup
  * deploy/undeploy/rollback
  * start/stop/restart

##  Steps followed when provisioning an RDS instance

the layer can represent only existing RDS instances.

- create RDS instance
- register RDS with the stack
- attach layer to an app, which adds RDS instance's connection information to the app's deploy attributes
- use info from deploy attributes to connect app to the RDS instance

### To register RDS instances with a stack

- In the AWS OpsWorks Stacks console, click Layer in the navigation pane, click + Layer or Add a layer to open the Add Layer page, and then click the RDS tab.
- If necessary, update the stack's service role, as described in Updating the Stack's Service Role.
- Click the RDS tab to list the available Amazon RDS instances.
- Select the appropriate instance, set User and Password to the appropriate user and password values and click Register to Stack.

If you change a registered Amazon RDS instance's password, you must manually update the password in AWS OpsWorks Stacks and then redeploy your apps to update the stack configuration and deployment attributes on the stack's instances.