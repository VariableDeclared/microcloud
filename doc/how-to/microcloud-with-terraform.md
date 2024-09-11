# Single Node Microcloud deployment (Nested VMs)

## Prerequisites

- Single Ubuntu node with LXD installed
- A network of type bridged on the host, e.g. from lxc network list
```
+----------------+----------+---------+-----------------+---------------------------+-------------+---------+---------+
|      NAME      |   TYPE   | MANAGED |      IPV4       |           IPV6            | DESCRIPTION | USED BY |  STATE  |
+----------------+----------+---------+-----------------+---------------------------+-------------+---------+---------+
| br0            | bridge   | NO      |                 |                           |             | 17      |         |
+----------------+----------+---------+-----------------+---------------------------+-------------+---------+---------+
```

## Clone the terraform

Get the terraform from the [demos folder](../../demos/microcloud-deploy)

## Get started - init lxd - optional if already initialised

```
sudo lxd init --auto
```

## Init terraform

```
sudo snap install --classic terraform
terraform init
```

### Variables

| Variable Name            | Purpose                                               |
| ------------------------ | ----------------------------------------------------- |
| lxd_project              | LXD Project - will be created                         |
| bridge_nic               | The bridge interface created in the VM                |
| lookup_subnet            | The CIDR of bridge_nic, e.g. 10.10.32.0/24            |
| ovn_gateway              | The IP to use for the OVN Virtual network router      |
| ovn_range_start          | The start range of OVN to be created                  |
| ovn_range_end            | The end range of OVN to be created                    |
| ssh_pubkey               | The public SSH key to insert into the Microcloud VMs  |
| host_bridge_network      | The LXD Bridge network                                |

## Apply the plan

### Init Microcloud

The terraform will automatically trigger an initialisation, via the non-interactive method - more information can be found here: https://canonical-microcloud.readthedocs-hosted.com/en/latest/how-to/initialise/#non-interactive-configuration


```
terraform apply
```