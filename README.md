# Azure Route Table Module

This module create all required resources for deploy a route table and the associated routes to be used in a Kubernetes Cluster.

## Usage

```bash
module "az_lb" {
  source = "https://github.com/walmartdigital/k8s-rt-module.git?ref=0.0.1"

  resource_group = "my-resource-group"
  cluster_name   = "my-cluster-name"
  environment    = "staging"
  name_suffix    = "abc123"

  route_table_name       = "my-route-table"
  route_names            = ["route1", "route2", "route3"]
  route_prefixes         = ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]
  route_nexthop_types    = ["VirtualAppliance", "VirtualAppliance", "VirtualAppliance"]
  next_hop_in_ip_address = ["10.20.0.1", "10.20.0.2", "10.20.0.3"]
}
```

## Arguments

* **resource_group**: A string representing the resource group where all resources will be provisioned (required).
* **cluster_name**: A string used as the name of the cluster.
* **environment**: A string used as environment where the cluster is deployed.
* **name_suffix**: A string used as name suffix (type: string).
* **route_table_name**: A string used as the name of the RouteTable being created.
* **disable_bgp_route_propagation**: Boolean flag which controls propagation of routes learned by BGP on that route table. True means disable and that's the default.
* **route_names**: A list of public subnets inside the vNet.
* **route_prefixes**: The list of address prefixes to use for each route.
* **route_nexthop_types**: A list types of Azure hop the packet should be sent to for each corresponding route. Valid values are _VirtualNetworkGateway_, _VnetLocal_, _Internet_, _VirtualAppliance_, _None_.
* **next_hop_in_ip_address**: A list of the IP addresses packets should be forwarded to. Next hop values are only allowed in routes where the next hop type is _VirtualAppliance_.

## Outputs

* **routetable_id**: The ID of the route table created.