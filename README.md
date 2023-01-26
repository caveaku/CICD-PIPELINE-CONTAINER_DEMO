# CICD-PIPELINE-CONTAINER_DEMO
# kojitechs-ci-cd-demo-infra-pipeline-tf

## connect to jenkins server:
```
http://<publicIP>:8080/
```
## Install plugins
Go to `manage jenkins`, `manage plugins` 
- sonarqube scanner 
- slack notification
- Quality Gates
- aws steps

## Edit jenkins bash profile
```
vi ~/.bash_profile

M2_HOME=/opt/maven/apache-maven-3.8.7/bin
PATH=$PATH:$HOME/bin:$M2_HOME
export PATH
```
sourec ~/.bash_profile
## make sure you only have java 11 instead java 17
```
openjdk version "17.0.6" 2023-01-17 LTS
OpenJDK Runtime Environment Corretto-17.0.6.10.1 (build 17.0.6+10-LTS)
OpenJDK 64-Bit Server VM Corretto-17.0.6.10.1 (build 17.0.6+10-LTS, mixed mode, sharing)
```
## install java 11
```
sudo yum install java-11-amazon-corretto-headless
sudo yum remove java-17-amazon-corretto-headless
```
## verify make make sure you have java 11
```
java -version
```
## Expect this
```
openjdk version "11.0.18" 2023-01-17 LTS
OpenJDK Runtime Environment Corretto-11.0.18.10.1 (build 11.0.18+10-LTS)
OpenJDK 64-Bit Server VM Corretto-11.0.18.10.1 (build 11.0.18+10-LTS, mixed mode)
```

## configure maven maven on jenkins 
```sh
echo $M2_HOME
/opt/maven/apache-maven-3.8.7
```
## Now go to manage cred
- create a token for sonarqube
- create a token for slack(it's only me!!)





## Sonarqube weebhook
```
http://3.145.169.209:8080/sonarqube-webhook/
```
### jenkins weebhook with github
Setting up webhook configuration for jenkins and github
```hcl
http://174.129.86.6:8080/github-webhook/
```
### Configuring maven 

## Assign shell to jenkins user 
```sh
vi /etc/passwd 
change shell from /bin/fasle to /bin/bash
```
```
maven {
    3.8.1
}
```
### Slack notification
```
slack notification
global configuration
```
### configuring sonarqube server
```
manage plugin
SonarQube ScannerVersion
2.15
Sonar Quality GatesVersion
1.3.1
Blue OceanVersion
1.27.0
```
configure system.
```
SonarQube servers
add SonarQube
name: sonar 
Server URL: http://18.206.246.242:9000
```
3. 
Go to SonarQube server and generate a token 
- sign in
username: admin
password: admin
- Create a jenkins user 
- generate a token

4. 
###  Configure quality Gate
Go to sonarqube server 
- create a webhook 
administration
webhooks
- create webhook
name: jenkins
URL: http://18.205.191.218:8080/sonarqube-webhook/

### Tools to connect with eks cluster 
```
aws-cli 
kubectl
```
## How to connect to eks cluster 
```
aws eks --region us-east-1 update-kubeconfig  --name ci-cd-demo-eks-demo
```
## Troubleshooting
```sh
rm ~/.kube/config

```
# Kubernetes  - PODs
```sh
- managed EKS cluster as the main an Admin using RBAC and kubernetes Role and Role binding to fine-Grain access to the cluster. 
- Using helm to create stable charts release and deploy  applications to EKS cluster
- Setup cloudwatch inside and Data Dog to get inside on application running on the cluster
```

<!-- preety ignore start -->
<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >=1.1.0 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | ~> 4.0 |
| <a name="requirement_kubectl"></a> [kubectl](#requirement\_kubectl) | >= 1.7.0 |
| <a name="requirement_kubernetes"></a> [kubernetes](#requirement\_kubernetes) | 2.16.1 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | ~> 4.0 |
| <a name="provider_kubernetes"></a> [kubernetes](#provider\_kubernetes) | 2.16.1 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_vpc"></a> [vpc](#module\_vpc) | terraform-aws-modules/vpc/aws | n/a |

## Resources

| Name | Type |
|------|------|
| [aws_ecr_repository.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ecr_repository) | resource |
| [aws_eks_cluster.eks_cluster](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/eks_cluster) | resource |
| [aws_eks_node_group.eks_nodegroup](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/eks_node_group) | resource |
| [aws_iam_instance_profile.instance_profile](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_instance_profile) | resource |
| [aws_iam_instance_profile.jenkins_instance_profile](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_instance_profile) | resource |
| [aws_iam_policy.policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_policy) | resource |
| [aws_iam_policy.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_policy) | resource |
| [aws_iam_role.eks_master_role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role.eks_nodegroup_role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role.jenkins_ssm_fleet_ec2](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role_policy_attachment.ec2_policy_attach](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.eks-AmazonEC2ContainerRegistryReadOnly](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.eks-AmazonEKSClusterPolicy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.eks-AmazonEKSVPCResourceController](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.eks-AmazonEKSWorkerNodePolicy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.eks-AmazonEKS_CNI_Policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.role_policy_attach](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_instance.jenkins-server](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance) | resource |
| [aws_instance.sonarqube-server](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance) | resource |
| [aws_security_group.jenkins_sg](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [aws_security_group.sonarqube_sg](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [aws_security_group_rule.egress_access_from_everywhere](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.egress_access_saonrqube_from_everywhere](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.ingress_access_on_http](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.ingress_sonarqube_access_on_http](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [kubernetes_cluster_role_binding_v1.eksdeveloper_clusterrolebinding](https://registry.terraform.io/providers/hashicorp/kubernetes/2.16.1/docs/resources/cluster_role_binding_v1) | resource |
| [kubernetes_cluster_role_v1.eksdeveloper_clusterrole](https://registry.terraform.io/providers/hashicorp/kubernetes/2.16.1/docs/resources/cluster_role_v1) | resource |
| [kubernetes_config_map_v1.aws_auth](https://registry.terraform.io/providers/hashicorp/kubernetes/2.16.1/docs/resources/config_map_v1) | resource |
| [aws_ami.ami](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/ami) | data source |
| [aws_availability_zones.available](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/availability_zones) | data source |
| [aws_caller_identity.current](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/caller_identity) | data source |
| [aws_eks_cluster_auth.cluster](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/eks_cluster_auth) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_cluster_endpoint_private_access"></a> [cluster\_endpoint\_private\_access](#input\_cluster\_endpoint\_private\_access) | Indicates whether or not the Amazon EKS private API server endpoint is enabled. | `bool` | `false` | no |
| <a name="input_cluster_endpoint_public_access"></a> [cluster\_endpoint\_public\_access](#input\_cluster\_endpoint\_public\_access) | Indicates whether or not the Amazon EKS public API server endpoint is enabled. When it's set to `false` ensure to have a proper private access with `cluster_endpoint_private_access = true`. | `bool` | `true` | no |
| <a name="input_cluster_endpoint_public_access_cidrs"></a> [cluster\_endpoint\_public\_access\_cidrs](#input\_cluster\_endpoint\_public\_access\_cidrs) | List of CIDR blocks which can access the Amazon EKS public API server endpoint. | `list(string)` | <pre>[<br>  "0.0.0.0/0"<br>]</pre> | no |
| <a name="input_cluster_service_ipv4_cidr"></a> [cluster\_service\_ipv4\_cidr](#input\_cluster\_service\_ipv4\_cidr) | (optional) describe your variable | `string` | `null` | no |
| <a name="input_cluster_version"></a> [cluster\_version](#input\_cluster\_version) | Kubernetes minor version to use for the EKS cluster (for example 1.21) | `string` | `null` | no |
| <a name="input_component_name"></a> [component\_name](#input\_component\_name) | (optional) describe your variable | `string` | `"ci-cd-demo"` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_aws-ecr-repo"></a> [aws-ecr-repo](#output\_aws-ecr-repo) | the name of aws ecr repo |
| <a name="output_cluster_arn"></a> [cluster\_arn](#output\_cluster\_arn) | The Amazon Resource Name (ARN) of the cluster. |
| <a name="output_cluster_certificate_authority_data"></a> [cluster\_certificate\_authority\_data](#output\_cluster\_certificate\_authority\_data) | Nested attribute containing certificate-authority-data for your cluster. This is the base64 encoded certificate data required to communicate with your cluster. |
| <a name="output_cluster_endpoint"></a> [cluster\_endpoint](#output\_cluster\_endpoint) | The endpoint for your EKS Kubernetes API. |
| <a name="output_cluster_iam_role_arn"></a> [cluster\_iam\_role\_arn](#output\_cluster\_iam\_role\_arn) | IAM role ARN of the EKS cluster. |
| <a name="output_cluster_iam_role_name"></a> [cluster\_iam\_role\_name](#output\_cluster\_iam\_role\_name) | IAM role name of the EKS cluster. |
| <a name="output_cluster_id"></a> [cluster\_id](#output\_cluster\_id) | The name/id of the EKS cluster. |
| <a name="output_cluster_oidc_issuer_url"></a> [cluster\_oidc\_issuer\_url](#output\_cluster\_oidc\_issuer\_url) | The URL on the EKS cluster OIDC Issuer |
| <a name="output_cluster_primary_security_group_id"></a> [cluster\_primary\_security\_group\_id](#output\_cluster\_primary\_security\_group\_id) | The cluster primary security group ID created by the EKS cluster on 1.14 or later. Referred to as 'Cluster security group' in the EKS console. |
| <a name="output_cluster_version"></a> [cluster\_version](#output\_cluster\_version) | The Kubernetes server version for the EKS cluster. |
| <a name="output_jenkins-host-ip"></a> [jenkins-host-ip](#output\_jenkins-host-ip) | Jenkins host public IP address |
| <a name="output_node_group_public_arn"></a> [node\_group\_public\_arn](#output\_node\_group\_public\_arn) | Node Group ARN |
| <a name="output_node_group_public_id"></a> [node\_group\_public\_id](#output\_node\_group\_public\_id) | Node Group ID |
| <a name="output_node_group_public_status"></a> [node\_group\_public\_status](#output\_node\_group\_public\_status) | Public Node Group status |
| <a name="output_node_group_public_version"></a> [node\_group\_public\_version](#output\_node\_group\_public\_version) | Public Node Group status |
| <a name="output_private_subnets"></a> [private\_subnets](#output\_private\_subnets) | n/a |
| <a name="output_sonarqube-host-ip"></a> [sonarqube-host-ip](#output\_sonarqube-host-ip) | Jenkins host public IP address |
| <a name="output_vpc_id"></a> [vpc\_id](#output\_vpc\_id) | n/a |
<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
<!-- preety ignore end -->

## Authors
This module was build and maintained by [kojibello](kojibello058@gmail.com).
For any further questions you and reach me on [Number](+12024288812)
