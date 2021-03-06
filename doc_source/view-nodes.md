# View nodes<a name="view-nodes"></a>

The Amazon EKS console shows information about all of your cluster's nodes, including Amazon EKS managed nodes, self\-managed nodes, and Fargate\. Nodes represent the compute resources provisioned for your cluster from the perspective of the Kubernetes API\. For more information, see [Nodes](https://kubernetes.io/docs/concepts/architecture/nodes/) in the Kubernetes documentation\. To learn more about the different types of Amazon EKS nodes that you can deploy your [workloads](view-workloads.md) to, see [Amazon EKS nodes](eks-compute.md)\.

**Prerequisites**
+ You must be an AWS IAM user that has IAM permissions to manage your Amazon EKS cluster\.
+ The IAM user or IAM role that you assume must have Kubernetes RBAC permissions to manage the resources in the namespaces that you want to view\. For more information, see [Managing users or IAM roles for your cluster](add-user-role.md)\.

**To view nodes using the AWS Management Console**

1. Open the Amazon EKS console at [https://console\.aws\.amazon\.com/eks/home\#/clusters](https://console.aws.amazon.com/eks/home#/clusters)\.

1. In the left navigation panel, select **Clusters**, and then in the **Clusters** list, select the cluster that you want to view compute resources for\.

1. On the **Overview** tab, you see a list of all compute **Nodes** for your cluster and the nodes' status\.
**Note**  
Each pod that runs on Fargate is registered as a separate Kubernetes node within the cluster\. This is because Fargate runs each pod in an isolated compute environment and independently connects to the cluster control plane\. For more information, see [AWS Fargate](fargate.md)\.

1. In the **Nodes** list, you see a list of all of the managed, self\-managed, and Fargate nodes for your cluster\. Selecting the link for one of the nodes provides the following information about the node:
   + The Amazon EC2 **Instance type**, **Kernel version**, **Kubelet version**, **Container runtime**, **OS** and **OS image** for managed and self\-managed nodes\.
   + Deep links to the Amazon EC2 console and the Amazon EKS managed node group \(if applicable\) for the node\.
   + The **Resource allocation**, which shows baseline and allocatable capacity for the node\.
   + **Conditions** describe the current operational status of the node\. This is useful information for troubleshooting issues on the node\. 

     Conditions are reported back to the Kubernetes control plane by the Kubernetes agent `kubelet` that runs locally on each node\. For more information, see [kubelet](https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/) in the Kubernetes documentation\. Conditions on the node are always reported as part of the node detail and the **Status** of each condition along with its **Message** indicates the health of the node for that condition\. The following common conditions are reported for a node:
     + **Ready** – This condition is **TRUE** if the node is healthy and can accept pods\. The condition is **FALSE** if the node is not ready and will not accept pods\. **UNKNOWN** indicates that the Kubernetes control plane has not recently received a heartbeat signal from the node\. The heartbeat timeout period is set to the Kubernetes default of 40 seconds for Amazon EKS clusters\.
     + **Memory pressure** – This condition is **FALSE** under normal operation and **TRUE** if node memory is low\.
     + **Disk pressure** – This condition is **FALSE** under normal operation and **TRUE** if disk capacity for the node is low\.
     + **PID pressure** – This condition is **FALSE** under normal operation and **TRUE** if there are too many processes running on the node\. On the node, each container runs as a process with a unique *Process ID*, or PID\.
     + **NetworkUnavailable** – This condition is **FALSE**, or not present, under normal operation\. If **TRUE**, the network for the node is not properly configured\.
   + The Kubernetes **Labels** and **Annotations** assigned to the node\. These could have been assigned by you, by Kubernetes, or by the Amazon EKS API when the node was created\. These values can be used by your workloads for scheduling pods\.