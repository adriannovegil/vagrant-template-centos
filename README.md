# Vagrant Template for CentOS

This file contains instructions on how to setup and manage a collection of [Vagrant instances](http://vagrantup.com).

## Creating Your First Server

Clone this repo.

```
$ git clone [REPO_URL]
```

Now, create the config file. You can copy the template file.

```
$ cp config.json.template config.json
```

Configure your instances. You can define a collection virtual machines.

Following you can see a example of the configuration of a instance.

### General Configuration

```
"base-01": {
    "enabled": true,
    "guest-ip": "10.0.3.40",
    "guest-hostname": "base01.vm.server",
    "box": "bento/centos-7.2",
    "box-url": "https://atlas.hashicorp.com/bento/boxes/centos-7.2/versions/2.3.1/providers/virtualbox.box",
    "timezone": "Europe/Madrid",
    "cpus": 1,
    "memory": 2048,
    "scripts": [
        "bootstrap.sh",
        "ssh.sh"
    ]
},
```

| Configuration         |  Value(s)                                                         |
| --------------------- | ----------------------------------------------------------------- |
| enabled               | True if we want to provision the machine, false otherwise.        |
| guest-ip              | IP of the server                                                  |
| guest-hostname        | Hostname of the server                                            |
| box                   | Vagrant Box                                                       |
| box-url               | URL to download the box                                           |
| timezone              | Server timezone                                                   |
| cpus                  | Number of CPUs                                                    |
| memory                | Instance memory                                                   |
| scripts               | List of script that we want to execute in the provisioning stage. |

### Network Configuration

```
"network": {
  "gw-ip": "192.168.0.1",
  "gw-if": "eth4",           
  "interfaces": [
    {
      "network-type": "private",
      "if-adapter": "eth1",
      "if-inet-type": "static",
      "if-address": "10.0.3.80",
      "if-netmask": "255.255.0.0"
    },
    {
      "network-type": "public",
      "if-adapter": "eth2",
      "if-inet-type": "static",
      "if-address": "192.168.0.157",
      "if-netmask": "255.255.0.0",
      "bridge-adapter": "enp1s0"
    }
  ]
}
```

#### General Network Configuration

| Configuration         |  Value(s)                                                         |
| --------------------- | ----------------------------------------------------------------- |
| gw-ip                 | The gateway IP                                                    |
| gw-if                 | The network interface that we want to use in the network route    |

#### Interface Configuration

| Configuration         |  Value(s)                                                         |
| --------------------- | ----------------------------------------------------------------- |
| network-type          | Private or Public [Vagrant documentation](https://www.vagrantup.com/docs/getting-started/networking.html) |
| if-adapter            | The name of the network adapter. i.e. eth0, eth1, etc.    |
| if-inet-type          | Static or nothing. [Vagrant documentation](https://www.vagrantup.com/docs/getting-started/networking.html) |
| if-address            | Ip address for the interface    |
| if-netmask            | Netmask for the interface    |
| bridge-adapter        | Indicates that the interface is a ```bridge``` interface. [Vagrant documentation](https://www.vagrantup.com/docs/networking/public_network.html)    |

Finally, run the following command:

```
 $ vagrant up
```

This will create the machines based off the configuration settings in `config.json`.

## Manage the Instance

### View the Instances Status

```
 $ vagrant status
```

### Connecting via SSH

```
 $ vagrant ssh [instance-id]
```

### Suspending the Server

```
 $ vagrant suspend [instance-id]
```

### Halting the Server

```
 $ vagrant halt [instance-id]
```

### Destroying the Server

```
 $ vagrant destroy [instance-id]
```
