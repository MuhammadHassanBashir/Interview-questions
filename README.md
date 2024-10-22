# Interview-questions

  **What it is: A task definition is like a blueprint for your application. It defines how your container(s) should be configured and run.**
  What it contains: It includes details like:
  Docker image(s) to use.
  CPU and memory requirements.
  Environment variables.
  Networking settings.
  Logging configuration.
  Volumes (shared storage).
  Versioned: Task definitions are versioned, so whenever you update the configuration, a new version is created.
  Static: A task definition doesn’t execute by itself. It just specifies the configuration and is used to launch tasks.
  Example: You might define a task definition for a web application that uses a specific Docker image, allocates 1 vCPU, 512MB of memory, and exposes port 80.
  
  2. Task:
  What it is: A task is an instance of a task definition in action. It is a running unit, often containing one or more containers.
  What it does: When a task is launched, ECS uses the task definition as a blueprint to spin up and run containers in an ECS cluster.
  Dynamic: A task represents the actual, running containers. You can have many tasks running from the same task definition.
  Managed: Tasks can be run manually, scheduled, or controlled by services like AWS ECS services.
  Example: A task could be a running instance of your web application, with the configuration and resources specified in the task definition.
  
  Key Differences:
  Feature	Task Definition	Task
  Purpose	Blueprint for how containers should run.	A running instance of a task definition.
  Configuration	Defines image, resources, environment, etc.	Executes based on the task definition's configuration.
  State	Static (doesn’t run on its own).	Dynamic (running containers).
  Scope	Defines the behavior of containers but doesn’t run.	Represents a specific execution of a task definition.

**In summary, a task definition is a template that defines the configuration for running containers, while a task is the actual execution of that configuration (the running container).**

  in simple word: A task definition is like a blueprint for your application. It defines how your container(s) should be configured and run.  

  **task definition blueprint ha for your application. jo k define krta ha k jb service ma task create hoga tu us ma container kis traha sa configure or run hoga..**

Instance group(an Instance Group is a collection of virtual machine (VM) instances that are managed together for better scalability and availabilit)
-----------------

Type	                           Key Features	                                                                                    Use Cases
Managed Instance Group (MIG)	   Auto-scaling, auto-healing, load balancing, rolling updates, uses instance templates.	          Web servers, scalable services.
Unmanaged Instance Group	       Manually managed, no auto-scaling or auto-healing, instances can have different configurations.	Heterogeneous VMs, specific manual control.
Zonal Managed Instance Group	   Operates within a single zone, not highly available across zones.	                              Development environments, non-critical apps.
Regional Managed Instance Group	 Operates across multiple zones, highly available, distributes traffic across zones.	            Production workloads requiring high availability.

 Why jenkins is deprecated and gitops(argocd) is helpfull
-------------------------------------------------------

Due to security concerns, many are shifting away from using Jenkins for deployments and moving towards GitOps tools like ArgoCD. Jenkins operates on a push-based mechanism, where it requires access to the cluster for deployments. To enable this, cluster authentication credentials must be provided to Jenkins. However, this poses a security risk, as these credentials can potentially be exposed, leaving the cluster vulnerable.

In contrast, ArgoCD uses a pull-based mechanism, which is more secure. An ArgoCD agent is deployed inside the Kubernetes cluster, and it continuously syncs (or pulls) the manifests from a Git repository. Since the agent is already within the cluster, it does not need external access credentials to authenticate with the cluster, significantly reducing the security risks.

What is the main difference b/w continous delivery and continous deployment
--------------------------------------------------------------------------

Continuous Delivery ensures that code is always ready to be deployed, **but requires human approval for production releases**.

Continuous Deployment goes further, automatically deploying code to production as soon as **it's tested and approved by the automated pipeline**.


Statefull set uses what network service
---------------------------------------

A StatefulSet in Kubernetes typically uses a Headless Service for network access to its pods.

Headless Service: **Unlike a regular service, a headless service does not load-balance requests. Instead, it provides each pod in the StatefulSet with a stable, unique DNS name based on the pod's name, allowing clients to connect directly to individual pods**. This is important for stateful applications because each pod often needs a stable identity and direct access, such as for databases or other services requiring state persistence.
Each pod in a StatefulSet can be accessed via a DNS name in the format:

 <statefulset_name>-<pod_ordinal>.<service_name>

This ensures that the pods have stable network identities even after restarts.

CRONJOB
-------

   When you set a cron job in Linux to run at a specific time, it will execute on the Linux system as per the defined schedule. However, if that cron job is intended to perform actions on a Kubernetes node (like applying a configuration, deploying an application, or running a script), and the Kubernetes server or nodes are down at that time, the following scenarios can occur:
   
   Scenarios When Kubernetes Nodes Are Down
   Job Execution Fails:
   
   If the cron job attempts to execute commands that interact with the Kubernetes API or the nodes, and those nodes are down, the commands will fail. For instance, any kubectl commands will not execute successfully because they can't communicate with the Kubernetes control plane.
   Delayed Effect:
   
   If your cron job is designed to retry or is idempotent (safe to run multiple times without changing the result beyond the initial application), it may eventually succeed once the Kubernetes nodes are back up. You might want to incorporate a retry mechanism or a check for the status of the Kubernetes cluster before executing commands.
   Failure Notifications:
   
   If the cron job is configured to send notifications upon failure (for example, sending an email or logging an error), you will receive alerts that the commands did not execute as expected.
   No Changes Made:
   
   If the cron job attempts to apply a configuration change, and the nodes are down, no changes will be made to the Kubernetes cluster. This means that once the nodes come back online, the state of the cluster will remain unchanged.
   Best Practices to Mitigate Issues
   Check Cluster Health: Implement a pre-check in the cron job to determine if the Kubernetes cluster is healthy before executing any commands. You can do this by running kubectl cluster-info and checking the output.
   
   Use Kubernetes CronJobs: Instead of using a Linux cron job, consider using Kubernetes CronJobs. This allows Kubernetes to manage the scheduling and execution of jobs within the cluster. If the cluster is down when the job is scheduled to run, the job won't execute, but you can configure it to run again once the cluster is back up.
   
   Logging and Alerts: Ensure that your cron job logs its output and errors so you can troubleshoot any issues that arise. You might also want to set up alerts for when jobs fail.
   
   Fallback Mechanism: If the job is critical, implement a fallback mechanism or manual intervention steps for when the job fails to execute as planned.
   
   By planning for these scenarios, you can minimize the impact of downtime on your scheduled tasks and ensure that your Kubernetes environment remains stable and responsive.

What is the difference b/w AWS VPC and GCP VPC
----------------------------------------------

    AWS VPC (Virtual Private Cloud) and GCP VPC (Google Cloud Virtual Private Cloud) are both services that allow users to create isolated networks within their respective cloud environments. While they serve similar purposes, there are key differences in their features, architecture, and functionality. Here's a breakdown of the main differences:
    
    1. Network Structure
    AWS VPC:
    
    A VPC can be divided into subnets (public and private) within a specific region.
    Subnets can span across multiple Availability Zones (AZs) for high availability.
    AWS provides the option to use a range of IP addresses (CIDR blocks) when creating a VPC.
    
    GCP VPC:
    
    GCP offers a global VPC model, meaning that a single VPC can span multiple regions, allowing for a more flexible and simplified network structure.
    Subnets in GCP are regional and can be created in specific zones within that region.
    
    2. IP Addressing
    AWS VPC:
    
    IP addressing is done within the CIDR block specified when creating the VPC.
    AWS uses private IP addressing for instances launched within the VPC.
    GCP VPC:
    
    GCP uses both internal (private) and external (public) IP addresses.
    When creating a subnet, you define the range of internal IPs, but external IPs can be dynamically assigned or reserved.
    
    3. Routing
    AWS VPC:
    
    Each VPC has an associated route table that controls traffic routing for subnets.
    Users can configure route tables to control routing between subnets, to the internet, and to other VPCs (via VPC peering).
    GCP VPC:
    
    GCP automatically creates a default route to allow traffic to the internet (if an external IP is assigned) and allows you to create custom routes.
    VPC routes are automatically updated when you add or remove subnets.
    
    4. Peering and Interconnectivity
    AWS VPC:
    
    VPC peering allows you to connect two VPCs privately. You can have multiple VPC peering connections.
    AWS also offers Transit Gateway for connecting multiple VPCs and on-premises networks.
    GCP VPC:
    
    VPC peering is also available in GCP, allowing private connectivity between VPC networks.
    GCP provides Cloud Interconnect for connecting on-premises infrastructure directly to GCP.
    
    5. Security
    AWS VPC:
    
    AWS provides security groups and network ACLs (Access Control Lists) to control inbound and outbound traffic at the instance and subnet levels.
    Security groups are stateful, while network ACLs are stateless.
    GCP VPC:
    
    GCP uses firewall rules to manage access to instances in the VPC, which are global and can be applied to all VMs or specific instances.
    GCP’s firewall rules are also stateful.
    
    6. Network Services
    AWS VPC:
    
    AWS offers various network services, such as Elastic Load Balancing, AWS Direct Connect, and VPN Gateway for connecting to on-premises resources.
    GCP VPC:
    
    GCP provides similar services like Cloud Load Balancing, Cloud VPN, and Cloud Interconnect for connecting to on-premises networks.
    
    7. Pricing Models
    AWS VPC:
    AWS charges for data transfer between VPCs, NAT Gateway usage, and other specific features.
    GCP VPC:
    GCP has a simplified pricing model where egress (data leaving GCP) is charged, but ingress (data entering GCP) is typically free.
    
    Summary
    In summary, while both AWS VPC and GCP VPC provide mechanisms for creating isolated network environments in their respective cloud platforms, they differ in their structure, routing, security models, and interconnectivity options. The choice between AWS VPC and GCP VPC may depend on your specific use cases, existing infrastructure, and preferences for cloud provider features.












