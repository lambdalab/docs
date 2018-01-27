# Prerequisites

In order to install Insight.io, make sure you have the following pre-requisites before you start:

* A DockerHub account or a registry.lambdalab.io account (if you are in China)

* An Ubuntu machine with root access. Note that port80(http) and port22(ssh) need to be opened.

* The Ubuntu machine must fulfill the minimum system requirements:

    * 16G RAM
    * 200G Hard Drive (SSD preferred)

* Make sure max virtual memory is big enough by running

```bash
sudo sysctl -w vm.max_map_count=262144
```

If you intended to deploy the service in very huge scale (100G+ repo), you may want to talk with
insight.io team before proceeding.

**Important Security Notice**
Due to its service oriented architecture, Insight.io will use certain ports for communication between services. These ports are only used internally. It is highly recommended for you to NOT expose thse ports to external network to prevent these ports to be exploited by attackers. Here are a list of these ports:

| port |
|------|
|`8080`|
|`9000`|
|`10060`|
|`27017`|
|`28017`|
|`50000`|