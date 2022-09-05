# Amazon Elastic Container Service (ECS)

**Amazon ECS** is a fully managed container orchestration service that makes it easy for you to deploy, 
manage, and scale containerized applications.

### Launch types:
  - **Fargate launch type:**  
    This is a serverless pay-as-you-go option. You can run containers without needing to manage your 
    infrastructure.  
    
    **Usage:**  
      - Large workloads that need to be optimized for low overhead;
      - Small workloads that have occasional burst;
      - Tiny workloads;
      - Batch workloads;
    
    **Pros:**
      - no management and configs;
      - pay for the working time;
      - auto scaling;
        
  - **EC2 launch type:**   
    Configure and deploy EC2 instances in your cluster to run your containers.
    
    **Usage:**  
      - Workloads that require consistently high CPU core and memory usage;
      - Large workloads that need to be optimized for price;
      - Your applications need to access persistent storage;
      - You must directly manage your infrastructure;
        
    **Pros:**
      - configuration management access;
      - more cheap;

[![](../../../../../../../images/containers_types.drawio.png)](../../../../../../../images/containers_types.drawio.png)

## EKS vs ECS
[![](../../../../../../../images/8ec72d9c-58b3-4846-a120-86d37fcebb2d_Screen-Shot-2020-07-30-at-10.15.21-AM.avif)](../../../../../../../images/8ec72d9c-58b3-4846-a120-86d37fcebb2d_Screen-Shot-2020-07-30-at-10.15.21-AM.avif)
