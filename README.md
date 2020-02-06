# Overview

This terraform configuration is used to build a [Rancher Kubernetes Engine (RKE)](https://github.com/rancher/rke) cluster on [cloud.ca](https://cloud.ca/) infrastructure.

## Table of Content

- [Resources](#resources)
- [Requirements](#requirements)
- [Available Kubernetes Versions](#available-kubernetes-versions)
- [Inputs](#rinputs)
- [Outputs](#outputs)
- [Usage](#usage)
- [License](#license)

## Resources

It will create the required infrastructure:

- one or several k8s master node(s)
- two or several k8s worker nodes

## Requirements

- [Terraform](https://www.terraform.io/downloads.html) 0.12+
- [Terraform Provider for cloud.ca](https://github.com/cloud-ca/terraform-provider-cloudca) 1.5+
- [Terraform Provider for RKE](https://github.com/yamamoto-febc/terraform-provider-rke) 0.14.1
- [terraform-docs](https://github.com/segmentio/terraform-docs) 0.5+

## Available Kubernetes Versions

Version of Kubernetes to be used in the RKE cluster can be controlled with [kubernetes_version](#kubernetes_version), which depends on the version of terraform-provider-rke being used in which depends on the version of RKE binary beind used in that provider version.

To get the list of available (and the default) version of Kubernetes take a look at release notes of [terraform-provider-rke](https://github.com/yamamoto-febc/terraform-provider-rke/releases) and [RKE](https://github.com/rancher/rke/releases) respectively.

<!-- terraform-docs starts -->

## Providers

| Name | Version |
|------|---------|
| cloudca | ~> 1.5 |
| local | n/a |
| rke | 0.14.1 |
| template | n/a |
| tls | n/a |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:-----:|
| api\_key | cloud.ca API key to use | `any` | n/a | yes |
| environment\_id | The environment ID to create resources in | `any` | n/a | yes |
| kubernetes\_version | Kubernetes version to install in the cluster | `string` | `"v1.15.3-rancher1-1"` | no |
| master\_count | Number of master node(s) to create | `number` | `1` | no |
| network\_id | The network ID to create resources in | `any` | n/a | yes |
| node\_prefix | Prefix to be used in name of instances, e.g. `cca` in `cca-foo-service01` | `string` | `"cca"` | no |
| node\_service | Service to be used in name of instances, e.g. `service` in `cca-foo-service01` | `string` | `"rke"` | no |
| node\_type | Type to be used in name of instances, e.g. `foo` in `cca-foo-service01` | `string` | `"cluster"` | no |
| node\_username | The username to create in the nodes with SSH access | `string` | `"rke"` | no |
| worker\_count | Number of worker node(s) to create | `number` | `2` | no |

## Outputs

| Name | Description |
|------|-------------|
| master\_ips | List of private IP of master node(s) |
| worker\_ips | List of private IP of worker node(s) |

<!-- terraform-docs ends -->

## Usage

1. Clone the repository into an appropriate name:

    ```bash
    git clone https://github.com/khos2ow/cloudca-rke-cluster.git cloudca-rke-cluster
    ```

2. Create `terraform.tfvars` containing:

    ```toml
    api_key = "<cloud_ca_API_KEY>"
    ```

3. Execute the following command to initialize the repository:

    ```bash
    make init plan
    ```

## License

```text
MIT License

Copyright (c) 2019 Khosrow Moossavi

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
