
# Hands-on with Rancher ! / Introduction to Rancher ?
## Overview

"Rancher is an open source project that provides a complete platform for
operating Docker in production" (github official page). It allow us:

- Infrastructure orchestration
- Container level orchestration and scheduling.
- Multi-host networking (IPSEC network overlay)

## Requirements

- Some Linux distribution (Debian, Ubuntu, CentOS, etc)
- [Docker version supported by rancher ](http://docs.rancher.com/rancher/v1.3/en/hosts/#supported-docker-versions)
- +1GB of RAM

## Architecture we are going to set up

![Architecture](https://drive.google.com/open?id=0B-vNtec_GTRbeUxFd0hPb0U5aFE)

## Step -1: Deploying the server (only Alejandro is going to do it)

Because To deploy the rancher server we only need to run:

``` sudo docker run -d --restart=unless-stopped -p 8080:8080 rancher/server ```

Spend at least 5 minutes playing with the rancher server interface, it will be
running under:

```http://<wait for URL/IP>:8080```

## Step 1: Deploying rancher agent

Deploying an agent is super easy in rancher, it is done through the web
interface, the steps are the following:

1. Select the environment where you want to deploy the agent.
2. Go to "Infrastructure -> Hosts" and click "Add Host"
3. Copy and paste the docker output (command) in the virtual machine you want to
run the agent

## Step 3: Creating our first stack

In rancher, a stack is a group of services (containers) which are grouped (usually
  deployed together)

We are going to create our first stack:

1. We need to click in "Stacks" -> "Add Stack"
2. Select an Stack name you want with some description (optional)
3. Copy and paste the following docker compose

```
wordpress:
  image: gravityrail/wordpress
  volumes:
    - src:/var/www/html
  links:
    - db:mysql
  ports:
    - 8080:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: example
```
**NOTE**: I might change this to something smaller to avoid everyone connecting to 
the internet to download some content


## Step 4: Manually adding services to our stack.




## To Go Further - Step 5: Assign labels to your agent and define constraints
to your stack

To assign labels to the agent we need to:

1. Select the environment where the agent is running and go to Infrastructure -> hosts
2. Click in the agent you want to assign a label and go

## Questions

## Further Reading

- [Rancher documentation](http://docs.rancher.com/)
