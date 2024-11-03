# Kubernetes Sidecar Containers and Resource Quotas

![sure-how-about-this-for-your-youtube-thumbnail-pro-wLRSQwKfRoyjFN-MshmBmA-q_0yO9OtTrKTmBtA1HE1rg](https://github.com/user-attachments/assets/fcbecebd-2d12-423d-879b-fa0c4cce8eb7)


---

## Overview

This repository provides a comprehensive exploration of Kubernetes Sidecar Containers and the implementation of Resource Quotas within a Kubernetes cluster. It serves as a resource to understand how to effectively use sidecar containers to extend application capabilities while managing cluster resources efficiently.

## Contents

### Sidecar Containers

**Sidecar Containers Overview**: Explanation of Sidecar containers, their use cases, and how they complement the main containers.
# 1.  Init Containers
# Purpose:

Init containers are specialized containers that run before the main application containers in a pod. They perform initialization tasks that must be completed before the main application starts.

# Key Features:

•	Sequential Execution: Init containers run one after the other, and each must complete successfully before the next one starts. \
•	Failure Handling: If an init container fails, the pod is marked as failed, and the container will be restarted according to the pod's restart policy. \
•	Isolation: Init containers can use a different image than the main application containers, allowing for different tooling or environments.

# Use Cases
•	Database Migrations: Running scripts to set up or migrate databases before the main application starts. \
•	Configuration Fetching: Fetching necessary configurations or secrets from external systems. \
•	Data Initialization: Pre-populating data or setting up the necessary state for the application to function correctly.


# 2. Adapter Containers
# Purpose
Adapter containers act as a bridge between the main application container and external services or APIs. They modify or adapt the communication between the application and its external dependencies.

# Key Features:
•	Protocol Translation: Adapter containers can translate between different communication protocols, allowing the application to communicate with various services seamlessly. \
•	Service Abstraction: They can abstract away details of service discovery and load balancing, providing a consistent interface for the main application. \
•	Independent Deployment: Adapter containers can be updated or scaled independently of the main application. 

# Use Cases:
•	Service Mesh Integration: Adapting application traffic in service mesh architectures, such as Istio. \
•	Logging and Monitoring: Interfacing with external logging or monitoring solutions, modifying requests/responses as necessary. \
•	API Gateway Functions: Performing tasks such as authentication, rate limiting, or request modification before reaching the main application.


# 3. Ambassador Containers
# Purpose
Ambassador containers are a specific type of adapter container that primarily manage network traffic between the main application and other services, including external systems. They often provide a layer of abstraction for external communication.

# Key Features
•	Routing Traffic: Ambassador containers can route requests to different services based on rules, making them suitable for API gateway scenarios. \
•	Network Policy Enforcement: They can enforce network policies, security controls, and authentication measures before allowing traffic to reach the main application. \
•	Load Balancing: Ambassador containers can perform load balancing for incoming requests to distribute traffic across multiple instances of a service.

# Use Cases
•	API Gateways: Acting as a single entry point for client applications to access backend services. \
•	Load Balancing: Distributing incoming traffic among several instances of a microservice. \
•	Cross-Cutting Concerns: Managing security, logging, or rate limiting across multiple services in a microservices architecture.


# Summary
•	Init Containers: Run before the main application to perform initialization tasks, ensuring the application starts in a ready state. \
•	Adapter Containers: Serve as intermediaries that modify communication between the application and external services, handling protocol differences and service discovery. \
•	Ambassador Containers: A specialized form of adapter container focused on managing and routing network traffic, often used in API gateway patterns. \

#########################################################################################################################


### Resource Quotas

1. **Resource Quotas Overview**: Explanation of how Resource Quotas manage resource usage within namespaces.
   - **Resource Units**: Mi (Mebibyte), m (millicores), Gi (Gibibyte)
   - **Example Setup**: Configurations for applying Resource Quotas to namespaces like Development and Staging.

2. **Example**:
   - **Namespace Creation**: YAML files to create namespaces with Resource Quotas.
   - **Pod Creation**: Steps to deploy pods and observe resource restrictions.

## Getting Started

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/sidecar-containers-resource-quota.git
   ```

2. **Apply Kubernetes Configurations**:
   ```bash
   kubectl apply -f deployments/
   kubectl apply -f resource-quota/
   ```

3. **Check Logs and Resource Usage**:
   - View Init container logs:
     ```bash
     kubectl logs <init-container-pod> -c <init-container-name> -f
     ```
   - Monitor resource usage and quotas:
     ```bash
     kubectl describe namespace <namespace-name>
     ```

 # Hands-on Practicals:

 # Init Containers:

 # Init container started:
 ![init-cont](https://github.com/user-attachments/assets/7b2b0d98-82ba-4b11-a394-0fb5052b0ddf)

 # Init container executed and now application container started:
 ![init-cont2](https://github.com/user-attachments/assets/1df8b399-53d0-41b9-b001-9903cb58deaa)

 

 ![init-cont1](https://github.com/user-attachments/assets/7b7ed09e-c802-4711-9f73-bc01ac2b059d)



 # Hands-on Practicals:

 # Adapter Containers:

 ![adapter-cont](https://github.com/user-attachments/assets/db4a9f9c-9dc4-4f07-b441-52d2ba1337e7)



 ![adapter-cont1](https://github.com/user-attachments/assets/88c1c08e-a125-4f35-bfab-5e2762c99a19)

##########################################################################################################

 # Resource Quotas:

 # Currently no Resource quota applied:
 
 ![resourcequota](https://github.com/user-attachments/assets/c39db61d-5d05-4a7a-84b2-9dd501cefcc1)


# After Reource quota is applied and Hard limit set for pod creation is 2:

 ![resourcequota1](https://github.com/user-attachments/assets/6899fc62-f43d-4cd0-8f1f-d8d4bc49ebdd)




# Now when we tried to create the third pod, it gave an error as exceeded quota:

 ![resourcequota2](https://github.com/user-attachments/assets/25ae77b0-e080-4098-920c-3f94cbe815aa)


 
![resourcequota3](https://github.com/user-attachments/assets/ca91bc9b-8182-4cc4-8bdd-c00f59276897)



# Now after applying Reource Quotas on namespace level and Limits on container level:

![resourcequota limits](https://github.com/user-attachments/assets/ed0b9348-ad2c-4ebe-afa3-e25abe5e296d)




## Resources

- [Kubernetes Documentation on Sidecar Containers](https://kubernetes.io/docs/concepts/workloads/pods/#sidecar-containers)
- [Kubernetes Documentation on Resource Quotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

---
