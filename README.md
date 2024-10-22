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


Type	                           Key Features	                                                                                    Use Cases
Managed Instance Group (MIG)	   Auto-scaling, auto-healing, load balancing, rolling updates, uses instance templates.	          Web servers, scalable services.
Unmanaged Instance Group	       Manually managed, no auto-scaling or auto-healing, instances can have different configurations.	Heterogeneous VMs, specific manual control.
Zonal Managed Instance Group	   Operates within a single zone, not highly available across zones.	                              Development environments, non-critical apps.
Regional Managed Instance Group	 Operates across multiple zones, highly available, distributes traffic across zones.	            Production workloads requiring high availability.






