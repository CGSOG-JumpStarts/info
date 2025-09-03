Directory Structure:

└── ./
    ├── infrastructure
    │   ├── compute.md
    │   ├── cycle-cloud.md
    │   ├── governance.md
    │   ├── management.md
    │   ├── networking.md
    │   ├── security.md
    │   ├── storage.md
    │   └── well-architected.md
    ├── platform
    │   ├── architectures.md
    │   ├── governance.md
    │   ├── management.md
    │   ├── networking.md
    │   ├── resource-selection.md
    │   └── security.md
    ├── center-of-excellence.md
    ├── govern.md
    ├── index.md
    ├── manage.md
    ├── plan.md
    ├── ready.md
    ├── secure.md
    ├── strategy.md
    └── toc.yml



---
File: /infrastructure/compute.md
---

---
title: Compute recommendations for AI workloads on Azure infrastructure (IaaS)
description: Learn how to select compute for AI workloads on Azure infrastructure (IaaS).
author: stephen-sumner
ms.author: rajanaki
ms.date: 04/09/2025
ms.topic: conceptual
---

# Compute recommendations for AI workloads on Azure infrastructure (IaaS)

This article provides compute recommendations for organizations running AI workloads on Azure infrastructure (IaaS). The preferred approach is to start your AI adoption with [Azure AI platform-as-a-service (PaaS) solutions](../platform/architectures.md). However, if you have access to Azure GPUs, follow this guidance to run AI workloads on Azure IaaS.

AI workloads require specialized virtual machines (VMs) to handle high computational demands and large-scale data processing. Choosing the right VMs optimizes resource use and accelerates AI model development and deployment. The following table provides an overview of recommended compute options.

| AI phase             | Virtual Machine Image  | Generative AI | Nongenerative AI (complex models)  | Nongenerative AI (small models)  |
|----------------------|------------------------|----------------------------|------------------------------------|----------------------------------|
| Training AI models   | [Data Science Virtual Machines](/azure/machine-learning/data-science-virtual-machine/overview/)     | GPU (prefer ND-family. Alternatively use NC family with ethernet-interconnected VMs) | GPU (prefer ND-family. Alternatively use NC family with ethernet-interconnected VMs) | [Memory-optimized](/azure/virtual-machines/sizes/memory-optimized/m-family) (CPU) |
| Inferencing AI models| [Data Science Virtual Machines](/azure/machine-learning/data-science-virtual-machine/overview/)     | GPU (NC or ND family)  | GPU (NC or ND family) | [Compute-optimized](/azure/virtual-machines/sizes/compute-optimized/f-family) (CPU) |

## Pick the right virtual machine image

Choose a suitable virtual machine image, such as the Data Science Virtual Machines, to access preconfigured tools for AI workloads quickly. This choice saves time and resources while providing the software necessary for efficient AI processing

- *Start with the Data Science Virtual Machines images.* The [Data Science Virtual Machine](/azure/machine-learning/data-science-virtual-machine/overview) image offers preconfigured access to data science tools. These tools include PyTorch, TensorFlow, scikit-learn, Jupyter, Visual Studio Code, Azure CLI, and PySpark. When used with GPUs, the image also includes Nvidia drivers, CUDA Toolkit, and cuDNN. These images serve as your baseline image. If you need more software, add it via a script at boot time or embed into a custom image. They maintain compatibility with your orchestration solutions.

- *Find alternative images as needed.* If the Data Science Virtual Machine image doesn't meet your needs, use the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps) or other search [methods](/azure/virtual-machines/overview#distributions) to find alternate images. For example, with GPUs, you might need [Linux images](/azure/virtual-machines/configure) that include InfiniBand drivers, NVIDIA drivers, communication libraries, MPI libraries, and monitoring tools.

## Pick a virtual machine size

Selecting an appropriate virtual machine size aligns with your AI model complexity, data size, and cost constraints. Matching hardware to training or inferencing needs maximizes efficiency and prevents underutilization or overload.

- *Narrow your virtual machine options.* Choose the latest virtual machine SKUs for optimal training and inference times. For training, select SKUs that support RDMA and GPU interconnects for high-speed data transfer between GPUs. For inference, avoid SKUs with InfiniBand, which is unnecessary. Examples include the [ND H200 v5](/azure/virtual-machines/sizes/gpu-accelerated/nd-h200-v5-series), [ND MI300X v5 series](/azure/virtual-machines/sizes/gpu-accelerated/nd-mi300x-v5-series), [ND H100 v5 series](/azure/virtual-machines/nd-h100-v5-series), [NDm A100 v4-series](/azure/virtual-machines/ndm-a100-v4-series), and [ND A100 v4-series](/azure/virtual-machines/nda100-v4-series).

- *Check virtual machine pricing.* Use the [Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) and [Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) VM pricing pages for a general cost overview. For a detailed estimate, use the [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).

- *Consider spot instances.* [Spot instances](/azure/virtual-machines/spot-vms) are cost-effective for inference scenarios with minimal data loss risk. Spot instances offer significant savings by utilizing unused datacenter capacity at a discount. However, this capacity can be reclaimed at any time, so spot instances are best for workloads that can handle interruptions. Regularly checkpoint data to minimize loss when evicted. For information, see [Using Spot VMs in Azure CycleCloud](/azure/cyclecloud/how-to/use-spot-instances).

## Choose a compute orchestration solution

Compute orchestration solutions facilitate the management of AI tasks across virtual machine clusters. Even for simple deployments, an orchestrator can help reduce costs and ensure an environment is reproducible. Orchestrators help ensure you only use the compute that you need for a specific amount of time. Select an orchestration tool based on your scheduling, containerization, and scaling needs to improve operations and scalability.

- *Use Azure CycleCloud for open-source schedulers.* Azure CycleCloud is ideal for open-source schedulers like Slurm, Grid Engine, or Torque/PBS. It provides flexible cluster management, customizable configurations, and advanced scheduling capabilities. Virtual machines within the cluster need configuration for AI workload execution. Virtual machines for CycleCloud and Batch are non-persistent. The orchestrator creates and removes VMs when needed to help with cost savings. For more information, see [Azure CycleCloud Workspace for Slum](./cycle-cloud.md).

- *Use Azure Batch for built-in scheduling.* Azure Batch offers built-in scheduling features with no need for extra software installation or management. It has a consumption pricing model and no licensing fees. It also supports containerized tasks natively. For deployment best practices, see [Azure Batch Accelerator](https://github.com/Azure/bacc).

- *Use Azure Kubernetes Service (AKS) for container scaling.* AKS is a managed service for deploying, scaling, and managing containers across a cluster. It's suitable for running AI workloads in containers at scale. For more information, see [Use Azure Kubernetes Service to host GPU-based workloads](/azure/architecture/reference-architectures/containers/aks-gpu/gpu-aks).

- *Manually orchestrate jobs for simpler tasks.* If orchestration needs are minimal, manage AI resources manually. Consider the following steps for small-scale workloads:
    - *Define your workflow.* Understand your workflow end-to-end, including dependencies and job sequence. Consider how to handle failures at any step.
    - *Log and monitor jobs.* Implement clear logging and monitoring frameworks for your jobs.
    - *Validate prerequisites.* Ensure your environment meets all workflow requirements, including necessary libraries and frameworks.
    - *Use version control.* Track and manage changes using version control.
    - *Automate tasks.* Use scripts to automate data preprocessing, training, and evaluation.

## Consider containers

Containers provide a consistent, reproducible environment that scales efficiently. Containers streamline transitions between environments, making them essential for scalable AI solutions.

- *Install drivers.* Ensure the necessary drivers are installed to enable container functionality in various scenarios. For cluster configurations, tools like Pyxis and Enroot are often required.

- *Use NVIDIA Container Toolkit.* This toolkit enables GPU resources within containers. Install all required drivers, such as CUDA and GPU drivers, and use your preferred container runtime and engine for AI workload execution.

## Next step

> [!div class="nextstepaction"]
> [Storage IaaS AI](./storage.md)



---
File: /infrastructure/cycle-cloud.md
---

---
title: Implementation option for AI on Azure infrastructure
description: Discover how to build AI workloads on Azure IaaS with detailed recommendations, architecture guides, and best practices.
author: stephen-sumner
ms.author: rajanaki
ms.date: 04/09/2025
ms.topic: conceptual
---

# Implementation option for AI on Azure infrastructure

This article provides implementation recommendations for organizations running AI workloads on Azure infrastructure (IaaS). After deploying an [Azure landing zone](../ready.md#use-an-azure-landing-zone), you can set up the application landing zone using the [CycleCloud Workspace for Slurm](/azure/cyclecloud/qs-deploy-ccws). Azure CycleCloud Workspace for Slurm offers several benefits for users who want to run AI workloads with the Slurm scheduler.

- *Easy and fast cluster creation.* Users can quickly create Slurm clusters on Azure through a simple GUI. They can choose from various Azure virtual machine (VM) sizes and types and customize cluster settings such as node count, network configuration, storage options (like Azure NetApp Files and Azure Managed Lustre Filesystem), and Slurm parameters.

- *Flexible and dynamic cluster management.* Azure CycleCloud scales Slurm clusters up or down automatically. Users can monitor cluster status, performance, and utilization, and view logs and metrics through the GUI. They can delete clusters when not needed and only pay for the resources they use.

- *Full control of the infrastructure.* Users have full control over the deployed infrastructure, allowing them to bring their own code, libraries, and packages, and to use resources on demand.

## Design guidelines

The following articles provide guidelines for AI workloads on Azure infrastructure (IaaS):

- [Compute](./compute.md)
- [Storage](./storage.md)
- [Networking](./networking.md)
- [Governance](./governance.md)
- [Management](./management.md)
- [Security](./security.md)

## Architecture

:::image type="content" source="../images/ai-infrastructure-landing-zone.svg" alt-text="Diagram showing AI application on Azure infrastructure in Azure landing zone." lightbox="../images/ai-infrastructure-landing-zone.svg" border="false":::
*Figure 1. AI application on Azure infrastructure in Azure landing zone.*

## Deploy CycleCloud Workspace for Slurm

The [CycleCloud Workspace for Slurm](/azure/cyclecloud/qs-deploy-ccws) can be used as the initial deployment in the enterprise environment. You can develop and customize the code to expand its functionality and/or adapt it to your Azure landing zone environment. Then, follow the guidance to [fine-tune a diffusion model from Hugging Face using Azure CycleCloud Workspace for Slurm](https://techcommunity.microsoft.com/t5/azure-compute-blog/fine-tuning-a-hugging-face-diffusion-model-on-cyclecloud/ba-p/4262431).

## Next step

> [!div class="nextstepaction"]
> [Compute IaaS AI](./compute.md)


---
File: /infrastructure/governance.md
---

---
title: Governance recommendations for AI workloads on Azure infrastructure (IaaS)
description: Learn how to govern AI workloads on Azure infrastructure (IaaS).
author: stephen-sumner
ms.author: rajanaki
ms.date: 04/30/2025
ms.topic: conceptual
---

# Governance recommendations for AI workloads on Azure infrastructure (IaaS)

This article provides governance recommendations for organizations running AI workloads on Azure infrastructure (IaaS). These recommendations help organizations establish a structured framework for resource management, cost control, security, and operational efficiency. By following these practices, you can scale your AI workloads responsibly and ensure they meet compliance, security, and financial goals.

## Resource governance

Resource governance establishes rules and standards for managing Azure resources. By enforcing governance policies, organizations can ensure compliance, standardize resource use, and control costs, which support the responsible scaling of AI operations.

- *Enforce tag usage.* Configure an [Azure Policy](/azure/governance/policy/tutorials/govern-tags) definition to enforce tagging on resources.

- *Apply governance policies to ensure compliance and standardization.* Use Azure Policy to enforce rules such as resource location, allowed SKUs, and mandatory tags. For example, create policies to restrict the deployment of certain high-cost VMs to control the budget.

- *Use resource groups for lifecycle management.* Deploy AI resources within resource groups that share a common lifecycle. Resource groups allow you to deploy, configure, and delete resources collectively. They also provide extra governance (policy), security (RBAC), and cost (budget) boundaries.

- *Standardize naming conventions.* Implement a standardized naming convention for AI resources. This practice improves tracking and management. Use the [naming rules and restrictions for each Azure resource](/azure/azure-resource-manager/management/resource-name-rules) and follow the [recommended abbreviations](/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations), as many resources often have name-length restrictions.

- *Govern infrastructure as code.* Use [Microsoft Defender for Cloud](/azure/defender-for-cloud/defender-for-devops-introduction) to monitor and enforce IaC security. This tool helps detect IaC misconfigurations and ensures secure deployments.

## Cost management

Cost management monitors and controls expenses related to AI workloads on Azure. Effective cost management enables organizations to set budgets, track spending, and maintain financial sustainability for AI projects.

- *Use tags to allocate costs.* Use tags to categorize resources by project, cost center, environment, and owner for better management and billing.

- *Use tag inheritance.* Use [tag inheritance](/azure/cost-management-billing/costs/enable-tag-inheritance) in Cost Management to apply billing, resource group, and subscription tags to child resource usage records.

- *Manage billing accounts.* Use [Microsoft Billing](/azure/cost-management-billing/cost-management-billing-overview) to oversee billing accounts and handle invoices. Assign a billing account to each AI project or team to facilitate accurate expense tracking.

- *Monitor costs.* Use [Microsoft Cost Management](/azure/cost-management-billing/costs/overview-cost-management#monitor-costs-with-alerts) to set budget alerts, cost anomaly alerts, and scheduled alerts. Monitoring costs in this way helps organizations maintain financial discipline.

- *View spending patterns.* Use the Azure [Cost analysis](/azure/cost-management-billing/costs/quick-acm-cost-analysis) to tool to regularly review spending patterns. This process identifies trends and reveals areas for potential savings, especially in VM usage.

- *Allow specific virtual machine SKUs.* Use Azure policy to allow only the virtual machines SKUs that align with your AI budget. The built-in policy definition [*Allowed virtual machine SKUs*](https://ms.portal.azure.com/#view/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fcccc23c7-8427-4f53-ad12-b6a63eb452b3) can enforce this control.

- *Consider autoscaling.* Use a [virtual machine scale set](/azure/virtual-machine-scale-sets/overview) to dynamically adjust VM counts based on demand, optimizing costs.

- *Configure VM autoshutdown.* Use the [autoshutdown feature](/azure/virtual-machines/auto-shutdown-vm) to schedule VMs to shut down during off-hours, reducing unnecessary costs.

### Security governance

Security governance addresses the need for robust protection measures across AI workloads. By implementing security policies and access controls, organizations can protect sensitive data and resources. It reduces risk and supports a secure AI environment on Azure.

- *Integrate with Microsoft Entra ID.* Use Microsoft Entra ID for centralized identity management and single sign-on (SSO) capabilities across AI workloads.

- *Implement distinct access controls for each environment.* Limit each deployment pipeline’s identity to its designated environment, reducing the risk of accidental deployments.

- *Enable Microsoft Defender for Cloud.* Activate Microsoft Defender for Cloud for advanced threat protection. It enhances security for workloads, including virtual machines, storage accounts, and databases, promoting a robust security posture for AI workloads.

### Operational governance

Operational governance ensures consistent monitoring and management of AI workloads. By using tools for monitoring, alerting, and automated deployments, organizations can maintain system health, detect issues early, and improve operational efficiency, contributing to reliable and stable AI operations.

- *Deploy monitoring agents.* Ensure that Azure Monitor Agents are deployed by default for virtual machines, Azure Virtual Machine Scale Sets, and Azure Arc connected servers. Connect them to a central Log Analytics workspace within the management subscription.

- *Configure alerts.* Enable [recommended alert rules](/azure/azure-monitor/best-practices-vm) to receive notifications of metric deviations.

- *Use a CI/CD pipeline.* Implement [continuous integration and continuous delivery (CI/CD)](/azure/cloud-adoption-framework/ready/considerations/devops-principles-and-practices#define-your-devops-framework) to automate code testing and deployment to different environments.

## Next step

> [!div class="nextstepaction"]
> [Management IaaS AI](./management.md)



---
File: /infrastructure/management.md
---

---
title: Management recommendations for AI workloads on Azure infrastructure (IaaS)
description: Learn how to manage AI workloads on Azure infrastructure (IaaS).
author: stephen-sumner
ms.author: rajanaki
ms.date: 04/30/2025
ms.topic: conceptual
---

# Management recommendations for AI workloads on Azure infrastructure (IaaS)

This article provides management recommendations for organizations running AI workloads on Azure infrastructure (IaaS). Effective management of AI workloads on Azure requires continuous monitoring, optimization practices, and a strong backup and recovery strategy. These efforts minimize downtime and ensure reliability in AI operations.

## Monitor AI infrastructure

Monitoring AI infrastructure involves tracking and evaluating the performance, health, and availability of all components in an AI deployment on Azure IaaS. Proactive monitoring allows organizations to detect and resolve potential issues before they affect operations.

- *Ensure monitoring by default.* Deploy the required Azure Monitor Agents for virtual machines and Azure Virtual Machine Scale Sets, including Azure Arc connected servers. Connect them to the central Log Analytics workspace in the management subscription. Consider using [Azure Monitor Baseline Alerts](https://azure.github.io/azure-monitor-baseline-alerts/welcome/) (AMBA).

- *Use Azure Update Manager.* You can monitor Windows and Linux update compliance across your machines in Azure and on-premises/on other cloud platforms (connected by [Azure Arc](/azure/azure-arc/)) from a single pane of management. You can also use Update Manager to make real-time updates or schedule them within a defined maintenance window.

- *Monitor virtual machines.* [Monitor](/azure/virtual-machines/monitor-vm) virtual machine (VM) host data (physical host) and VM guest data (operating system and application). Consider using [VM Insights](/azure/azure-monitor/vm/vminsights-enable-overview) to simplify the onboarding, access predefined performance charts, and utilize dependency mapping. Track Spot VM evictions and maintenance events to manage interruptions effectively. [Learn more about scheduled events](/azure/virtual-machines/linux/scheduled-events).

- *Monitor networks.* [Monitor and diagnose](/azure/network-watcher/network-watcher-overview) networking issues without logging into your VMs. Get real-time performance information at the packet level. Troubleshoot performance issues with the [Performance Diagnostics tool](/troubleshoot/azure/virtual-machines/windows/performance-diagnostics). [Track](/azure/network-watcher/network-insights-overview) topology, health, and metrics for all deployed network resources.

- *Monitor storage.* Monitor the performance of storage, such as local SSDs, [attached disks](/azure/virtual-machines/disks-metrics), file shares, and [Azure storage accounts](/azure/azure-monitor/insights/storage-insights-overview).

- *Use orchestrator monitoring capabilities (if applicable).* Consider using the built-in monitoring capabilities of orchestrators like Azure CycleCloud, Azure Batch, and Azure Kubernetes Service (AKS). Follow the guidance for the orchestrator you chose:

    - *Azure CycleCloud or Azure CycleCloud Workspace for Slurm:* Track CPU, disk, and network metrics. Store data from Azure CycleCloud clusters to Log Analytics and create custom metrics dashboards. For more information, see [Monitoring Azure CycleCloud](/azure/cyclecloud/concepts/monitoring). [Node Health Checks](https://github.com/Azure/azurehpc-health-checks#Configuration) are a set of automated tests to ensure that your HPC/AI hardware is healthy. You can run this check in Azure CycleCloud as part of cluster deployment or separately using the GitHub repo instructions. Ensure that you pay attention to the compatibility matrix in the documentation. Run where appropriate to ensure that you identify any unhealthy nodes before running your AI workloads.

    - *Azure Batch:* Collect job and task metrics such as active tasks, task duration, job start time, duration, task start time. Also collect pool metrics, such as idle nodes, running nodes, CPU usage, Disk I/O. For more information, see [Azure Batch monitoring](/azure/batch/monitor-batch).

    - [*Azure Kubernetes Service*](/azure/architecture/reference-architectures/containers/aks-gpu/gpu-aks). Use Azure Monitor for containers. Monitor pod performance, node health, and resource utilization. Set up alerts and custom dashboards.

## Manage business continuity and disaster recovery

Managing business continuity and disaster recovery for AI applications on Azure ensures that organizations can recover quickly from disruptions. By implementing strategies such as real-time replication, automated recovery, and regular backups, organizations safeguard their AI infrastructure against data loss and operational downtime.

- *Use Azure Site Recovery.* Site Recovery uses real-time replication and recovery automation to replicate workloads across regions. Built-in platform capabilities for VM workloads meet low RPO and RTO requirements. You can use Site Recovery to run recovery drills without affecting production workloads. You can also use Azure Policy to enable replication and to audit VM protection.

- *Use orchestrator capabilities (if applicable)*. Use your orchestrator to recover failed compute nodes. For example, configure Azure Batch to automatically [retry tasks](/azure/batch/best-practices#pool-allocation-failures) if there's failure.

- *Schedule backups.* Determine if you need to backup incremental changes to datasets and models daily or weekly. Backups could also include databases or entire datasets.

- *Ensure data compliance.* Make sure your backup strategy complies with data protection regulations. Comply with data residency requirements and store backups in appropriate geographic locations.

- *Create snapshots.* You can use the capabilities of your scheduler to take snapshots. For example, [CycleCloud](/azure/cyclecloud/how-to/backup-and-restore) can take point-in-time snapshots of the underlying application datastore as recovery points.

## Next step

> [!div class="nextstepaction"]
> [Secure IaaS AI](./security.md)



---
File: /infrastructure/networking.md
---

---
title: Networking recommendations for AI workloads on Azure infrastructure (IaaS)
description: Learn how to configure networking for AI workloads on Azure infrastructure (IaaS).
author: stephen-sumner
ms.author: rajanaki
ms.date: 03/18/2025
ms.topic: conceptual
---

# Networking recommendations for AI workloads on Azure infrastructure (IaaS)

This article provides networking recommendations for organizations running AI workloads on Azure infrastructure (IaaS). Designing a well-optimized network can enhance data processing speed, reduce latency, and ensure the network infrastructure scales alongside growing AI demands.

## Ensure sufficient bandwidth

Sufficient bandwidth refers to the capacity of a network to handle large volumes of data without delays or interruptions. High bandwidth ensures fast, uninterrupted data transfer between on-premises systems and Azure, supporting rapid AI model training and reducing downtime in the pipeline. For organizations transferring large datasets from on-premises to the cloud for AI model training, a high-bandwidth connection is essential. Use Azure ExpressRoute to establish a dedicated, secure, and reliable high-speed connection between your on-premises network and Azure.

## Minimize latency

Minimizing latency involves reducing delays in data transfer between networked resources. Lower latency provides quicker data processing, enabling real-time insights, and improving the performance of latency-sensitive workloads.

- *Optimize resource placement.* To minimize latency for AI workloads, such as data preprocessing, model training, and inference, deploy virtual machines (VMs) within the same Azure region or availability zone. Colocating resources reduces physical distance, thus improving network performance.
  
- *Use proximity placement groups (PPGs).* For latency-sensitive workloads requiring real-time processing or fast inter-process communication, utilize PPGs to physically colocate resources within an Azure datacenter. PPGs ensure that compute, storage, and networking resources remain close together, minimizing latency for demanding workloads. Orchestration solutions and InfiniBand handle node proximity automatically.
  
- *Use preconfigured Linux OS images.* Simplify cluster deployment by selecting Linux OS images from the Azure Marketplace prepackaged with InfiniBand drivers, NVIDIA drivers, communication libraries, and monitoring tools. These images are optimized for performance and can be deployed with Azure CycleCloud for fast, efficient cluster creation.

## Implement high-performance networking

High-performance networking utilizes advanced networking features to support large-scale, intensive AI computations, particularly for GPU-accelerated tasks. High-performance networks ensure rapid, efficient data exchanges between GPUs, which optimizes model training and accelerates AI development cycles.

- *Utilize InfiniBand for GPU workloads.* For workloads dependent on GPU acceleration and distributed training across multiple GPUs, use Azure's InfiniBand network. InfiniBand’s GPUDirect remote direct memory access (RDMA) capability supports direct GPU-to-GPU communication. It improves data transfer speed and model training efficiency. Orchestration solutions like Azure CycleCloud and Azure Batch handle InfiniBand network configuration when you use the appropriate VM SKUs.
  
- *Choose Azure’s GPU-optimized VMs.* Select VMs that use InfiniBand, such as ND-series VMs, which are designed for high-bandwidth, low-latency inter-GPU communication. This configuration is essential for scalable distributed training and inference, allowing faster data exchange between GPUs.

## Optimize for large-scale data processing

Optimizing for large-scale data processing involves strategies to manage extensive data transfers and high computational loads. By using data and model parallelism, you can scale your AI workloads and enhance processing speed. Use Azure’s GPU-optimized virtual machines to handle complex, data-intensive AI workloads.

- *Apply data or model parallelism techniques.* To manage extensive data transfers across multiple GPUs, implement data parallelism or model parallelism depending on your AI workload needs. Ensure the use of High Bandwidth Memory (HBM), which is ideal for high-performance workloads due to its high bandwidth, low power consumption, and compact design. HBM supports fast data processing, essential for AI workloads that require processing large datasets.

- *Use advanced GPU networking features.* For demanding AI scenarios, choose Azure VMs like NDH200v5, NDH100v5 and NDMI300Xv5. Azure configures these VMs with dedicated 400 Gb/s NVIDIA Quantum-2 CX7 InfiniBand connections within virtual machine scale sets. These connections support GPU Direct RDMA, enabling direct GPU-to-GPU data transfers that reduce latency and enhance overall system performance.

## Next step

> [!div class="nextstepaction"]
> [Security IaaS AI](./security.md)



---
File: /infrastructure/security.md
---

---
title: Security recommendations for AI workloads on Azure infrastructure (IaaS)
description: Learn how to secure AI workloads on Azure infrastructure (IaaS).
author: stephen-sumner
ms.author: rajanaki
ms.date: 04/30/2025
ms.topic: conceptual
---

# Security recommendations for AI workloads on Azure infrastructure (IaaS)

This article provides security recommendations for organizations running AI workloads on Azure infrastructure (IaaS). Security for AI on Azure infrastructure involves protecting data, compute, and networking resources that support AI workloads. Securing these components ensures that sensitive information remains safe, minimizes exposure to potential threats, and ensures a stable operational environment for AI models and applications.

## Secure Azure services

Azure service security requires configuring each Azure service used in an AI architecture to meet specific security standards and benchmarks.

- *Harden Azure services.* To apply secure configurations to Azure services, use the [Azure security baselines](/security/benchmark/azure/security-baselines-overview) for each service in your architecture. Common Azure services in AI workloads on Azure infrastructure include: [Windows virtual machines](/security/benchmark/azure/baselines/virtual-machines-windows-virtual-machines-security-baseline), [Linux virtual machines](/security/benchmark/azure/baselines/virtual-machines-linux-virtual-machines-security-baseline), [Azure CycleCloud](/azure/cyclecloud/concepts/security-best-practices), and [Key Vault](/security/benchmark/azure/baselines/key-vault-security-baseline).

- *Consider secure compute options.* Secure the boot process and integrity of your VMs using [trusted launch](/azure/virtual-machines/trusted-launch). Depending on your industry and use case, consider using confidential AI. [Confidential AI](/azure/confidential-computing/confidential-ai) is for cryptographically verifiable protection for AI data and models during training, fine-tuning, and inferencing.

## Secure networks

Securing networks involves setting up private endpoints, Network Security Groups (NSGs), and firewalls to manage and control data flow within Azure. This step limits exposure to external threats and protects sensitive data as it moves between services within the Azure infrastructure.

- *Use private endpoints.* Use private endpoints available in [Azure Private Link](/azure/networking/fundamentals/networking-overview#privatelink) for any PaaS solution in your architecture, such as your storage or filesystem.

- *Use encrypted virtual network connections for Azure to Azure connectivity.* Encrypted connections between virtual machines or virtual machine scale sets in the same or peered virtual networks prevent unauthorized access and eavesdropping. Establish these secure connections by configuring encryption options in Azure Virtual Network for virtual machine communication.

- *Implement Network Security Groups (NSGs).* NSGs can be complex. Ensure you have a clear understanding of the NSG rules and their implications when setting up your Azure infrastructure for AI workloads.

  - *Understand NSG prioritization rules*. [NSG](/azure/virtual-network/network-security-groups-overview) rules have a priority order. Understand this order to avoid conflicts and ensure the smooth running of your AI workloads.

- *Use Application Security Groups*. If you need to label traffic at a greater granularity than what virtual networks provide, consider using [Application Security Groups](/azure/virtual-network/application-security-groups).

- *Use a network firewall.* If you’re using a hub-spoke topology, deploy a [network firewall](/azure/networking/fundamentals/networking-overview#firewall) to inspect and filter network traffic between the spokes.

- *Close unused ports.* Limit internet exposure by exposing only services intended for external-facing use cases and using private connectivity for other services.

## Secure data

Securing data includes encrypting data at rest and in transit, along with protecting sensitive information such as keys and passwords. These measures ensure that data remains private and inaccessible to unauthorized users, reducing the risk of data breaches and unauthorized access to sensitive information.

- *Encrypt data*: Encrypt data at rest and in transit using strong encryption technologies between each service in the architecture.

- *Protect secrets*: Protect secrets by storing them in a key vault or a [hardware security module](/azure/key-vault/managed-hsm/overview) and routinely rotate them.

## Secure access

Securing access means configuring authentication and access control mechanisms to enforce strict access permissions and verify user identities. By restricting access based on roles, policies, and multifactor authentication, organizations can limit exposure to unauthorized access and protect critical AI resources.

- *Configure authentication*: Enable multifactor authentication (MFA) and prefer secondary administrative accounts or just-in-time access for sensitive accounts. Limit control plane access using services like Azure Bastion as secure entry points into private networks.

- *Use Conditional Access Policies.* Require MFA for accessing critical AI resources to enhance security. Restrict access to AI infrastructure based on geographic locations or trusted IP ranges. Ensure that only compliant devices (those meeting security requirements) can access AI resources. Implement risk-based Conditional Access policies that respond to unusual sign-in activity or suspicious behavior. Use signals like user location, device state, and sign-in behavior to trigger extra verification steps.

- *Configure least privilege access.* Configure least privilege access by implementing role-based access control (RBAC) to provide minimal access to data and services. Assign roles to users and groups based on their responsibilities. Use Azure RBAC to fine-tune access control for specific resources such as virtual machines and storage accounts. Ensure users have only the minimum level of access necessary to perform their tasks. Regularly review and adjust permissions to prevent privilege creep.

## Prepare for incident response

Preparing for incident response involves collecting logs and integrating them with a Security Information and Event Management (SIEM) system. This proactive approach enables organizations to detect and respond to security incidents quickly, reducing potential damage, and minimizing downtime for AI systems.

## Secure operating systems

Securing operating systems requires keeping virtual machines and container images up-to-date with the latest patches and running antimalware software. These practices protect AI infrastructure from vulnerabilities, malware, and other security threats. They help maintain a secure and reliable environment for AI operations.

- *Patch virtual machine guests.* Regularly apply patches to virtual machines and container images. Consider enabling [automatic guest patching](/azure/virtual-machines/automatic-vm-guest-patching) for your virtual machines and scale sets.

- *Use antimalware.* Use [Microsoft Antimalware for Azure](/azure/security/fundamentals/antimalware) on your virtual machines to protect them from malicious files, adware, and other threats.

## Next step

> [!div class="nextstepaction"]
> [Govern AI](../govern.md)



---
File: /infrastructure/storage.md
---

---
title: Storage recommendations for AI workloads on Azure infrastructure (IaaS)
description: Learn how to select storage for AI workloads on Azure infrastructure (IaaS).
author: stephen-sumner
ms.author: rajanaki
ms.date: 04/29/2025
ms.topic: conceptual
---

# Storage recommendations for AI workloads on Azure infrastructure (IaaS)

This article provides storage recommendations for organizations running AI workloads on Azure infrastructure (IaaS). A storage solution for AI workloads on Azure infrastructure must be capable of managing the demands of data storage, access, and transfer that are inherent to AI model training and inferencing.

AI workloads require high throughput and low latency for efficient data retrieval and processing. They also need mechanisms for data versioning and consistency to guarantee accurate and reproducible outcomes across distributed environments. When selecting the appropriate storage solution, consider factors such as data transfer times, latency, performance requirements, and compatibility with existing systems.

- *Use a file system for active data*. Implement a file system to store "job-specific/hot" data actively used or generated by AI jobs. This solution is ideal for real-time data processing due to its low latency and high throughput capabilities. These capabilities are critical for optimizing the performance of AI workflows. Azure has three principal file system solutions to support training and inferencing AI models on Azure infrastructure. To choose the right file system, follow these recommendations:

    - *Use Azure Managed Lustre for lowest data transfer times and minimized latency.* Azure Managed Lustre provides high performance with parallel file system capabilities and simplifies management with Azure integration. It's cost-effective, with usage-based storage costs, and allows selective data import from Blob Storage, optimizing data handling.
    
    - *Use Azure NetApp Files when you need enterprise-grade features and performance for AI workloads.* Azure NetApp Files offer high reliability and performance, ideal for mission-critical applications. Azure NetApp Files is beneficial if you have existing investments in NetApp infrastructure. It's beneficial for hybrid cloud capabilities and when you need to customize and fine-tune storage configurations.
    
    - *Use local NVMe/SSD file systems when performance is the top priority.* It aggregates the local NVMe of compute (worker nodes) using a job-dedicated parallel file system like BeeGFS On Demand (BeeOND). They operate directly on the compute nodes to create a temporary, high-performance file system during the job. These systems offer ultra-low latency and high throughput, making them ideal for I/O-intensive applications like deep learning training or real-time inferencing.

- *Transfer inactive data to Azure Blob Storage.* After completing a job, transfer inactive job data from Azure Managed Lustre to Azure Blob Storage for long-term, cost-effective storage. Blob storage provides scalable options with different access tiers, ensuring efficient storage of inactive or infrequently accessed data, while keeping it readily available when needed.

- *Implement checkpointing for model training.* Set up a checkpointing mechanism that saves the model’s state, including training weights and parameters, at regular intervals such as every 500 iterations. Store this checkpoint data in Azure Managed Lustre to allow restarting the model training from a previously saved state, improving the flexibility and resilience of your AI workflows.

- *Automate data migration to lower-cost storage tiers.* Configure Azure Blob Storage lifecycle management policies to automatically migrate older, infrequently accessed data to lower-cost storage tiers, such as the Cool or Archive tiers. This approach optimizes storage costs while ensuring that important data remains accessible when needed.

- *Ensure data consistency across distributed environments.* Ensure data consistency across distributed AI workloads by setting up synchronization between Azure Managed Lustre and Azure Blob Storage. This synchronization ensures that all nodes accessing the data are working with the same, consistent version, preventing errors and discrepancies in distributed environments.

- *Enable data versioning for reproducibility.* Activate versioning in Azure Blob Storage to track changes to datasets and models over time. This feature facilitates rollback, enhances reproducibility, and supports collaboration. It maintains a detailed history of modifications to data and models and allows you to compare and restore previous versions as needed.

## Next step

> [!div class="nextstepaction"]
> [Networking IaaS AI](./networking.md)



---
File: /infrastructure/well-architected.md
---

---
title: Well-architected considerations for AI workloads on Azure infrastructure (IaaS)
description: Learn how to design AI workloads on Azure infrastructure (IaaS).
author: stephen-sumner
ms.author: rajanaki
ms.date: 03/11/2025
ms.topic: conceptual
---
# Well-architected considerations for AI workloads on Azure infrastructure (IaaS)

Well-architected considerations for AI on Azure infrastructure involve best practices that optimize the reliability, security, operational efficiency, cost management, and performance of AI solutions. These principles ensure robust deployment, secure data handling, efficient model operation, and scalable infrastructure on Azure’s IaaS platform. Applying these principles allows organizations to build resilient, secure, and cost-effective AI models that meet business needs.

## Reliability

Reliability involves minimizing downtime and ensuring consistent performance for AI applications on Azure infrastructure. Ensuring reliable operations across distributed virtual machines (VMs) and maintaining performance during infrastructure changes prevents service interruptions. These practices are important because they guarantee continuous model availability and improve user experience.

- *Distribute VMs across Availability Zones.* Minimize downtime from hardware failures or maintenance events by using [Availability Zones](/azure/reliability/availability-zones-overview). They distribute VMs across fault and update domains to ensure continued application operation.

- *Set up health monitoring with Azure Monitor.* Track CPU, memory, and network performance on your VMs using Azure Monitor and configure alerts to notify you of performance degradation or failures in the infrastructure supporting your models. For more information, see [Azure Monitor VM Insights](/azure/azure-monitor/vm/vminsights-health-overview).

- *Automate patching and updates with rolling instances.* Use Azure Update Management to apply patches in a rolling manner, allowing one instance to be updated while others continue to serve traffic, preventing downtime during maintenance.

- *Design for graceful degradation during partial failures.* Ensure core functionality remains available by serving less complex AI models or limiting specific features when some VMs become unavailable, allowing users access to essential services even during outages.

- *Implement regular backups for key assets.* Regularly back up model data, training datasets, and configurations to enable quick restoration if there was a failure, safeguarding valuable progress and data.

## Security

Security covers protective measures to safeguard AI models, data, and infrastructure against unauthorized access and threats. Implement updates, monitor model integrity, and control access to prevent vulnerabilities that could compromise sensitive information. These steps are essential to maintain data privacy and trustworthiness of AI solutions in production environments.

- *Schedule updates for Azure resources.* Use maintenance configurations to set specific update schedules for VMs and extensions, reducing vulnerability windows.

- *Patch virtual machines and container images regularly.* Enable [automatic guest patching](/azure/virtual-machines/automatic-vm-guest-patching) for VMs and scale sets to maintain security against new threats. For more information, see [Guest updates and host maintenance overview](/azure/virtual-machines/updates-maintenance-overview).

- *Monitor for model drift and ensure integrity.* Ensure model integrity by implementing security mechanisms such as digital signatures or hash verifications for model files to prevent unauthorized modifications. Use Azure Monitor to track key performance metrics and identify model drift, which could indicate potential security vulnerabilities or data shifts. You can define custom metrics (accuracy, F1-score, and data distribution on your models) in your code by using the [Azure Monitor Metrics SDK](/azure/azure-monitor/essentials/metrics-custom-overview). Azure Monitor Metrics SDK allows you to send your model’s performance statistics and data drift measurements to Azure Monitor. Monitoring for performance changes over time can help detect when a model's behavior deviates, potentially signaling an attack or a need for retraining. This proactive approach helps safeguard model integrity and maintain security compliance.

- *Implement auditing and access logs.* Use Azure Monitor and Log Analytics to log access to models and VMs, helping to identify unauthorized access or unusual usage patterns. For more information, see [Activity logs in Azure Monitor](/azure/azure-monitor/essentials/activity-log).

- *Use version control for model files.* Store model files in Azure Storage (Blob, File, or Disk) with versioning to track changes, ensuring a clear audit trail for identifying and rolling back harmful modifications. Using Azure DevOps for version control enhances security by managing access to code changes and enforcing best practices in code reviews. This layered approach mitigates risks of unauthorized changes and provides accountability. For more information, see [Blob Versioning in Azure Storage](/azure/storage/blobs/versioning-overview).

- *Set up anomaly detection for model outputs.* Use Azure Monitor to track the output metrics of your models and set up alerts for unusual behavior. For example, monitoring API responses from your model can help detect abnormal output. You can set anomaly detection on a metric like prediction accuracy to automatically detect when it drops outside of an expected range. For more information, see [Create and Manage Metric Alerts with Dynamic Thresholds](/azure/azure-monitor/alerts/alerts-dynamic-thresholds).

- *Enforce model access policies.* Use [Azure role-based access control (RBAC)](/azure/role-based-access-control/overview) and Microsoft Entra ID to secure access to VMs and model files, limiting access to authorized users only.

- *Regularly revalidate models against updated data.* Implementing periodic revalidation of your model using automated scripts or workflows on your VMs ensures that the model remains accurate and effective against current datasets, mitigating risks from outdated or inaccurate predictions. By scheduling these tasks with Azure Automation or Azure Logic Apps, you can maintain compliance with data standards and enhance overall model security. This proactive approach helps identify vulnerabilities early, ensuring continuous improvement and safeguarding against potential threats. You can schedule your automation workflows to periodically trigger revalidation tasks. Start with an [Azure Automation runbook](/azure/automation/automation-runbook-execution), [run in the virtual machine](/azure/automation/automation-hybrid-runbook-worker), create an appropriate [schedule](/azure/automation/shared-resources/schedules) to get validation results.

- *Track data lineage and model file changes.* Enable versioning in Azure Blob Storage and track data used in training and inference, ensuring no unauthorized data affects model outcomes.

- *Apply resource quotas and rate limits.* Implement rate limits and quotas for your model APIs through Azure API Management to prevent overuse or abuse, which can lead to system vulnerabilities or service outages. This strategy ensures the system remains responsive during high traffic and mitigates risks associated with denial-of-service attacks. By controlling access, you can maintain performance and protect sensitive data from potential exploitation [API Management Quotas and Limits](/azure/api-management/api-management-policies#rate-limiting-and-quotas).

- *Conduct regular vulnerability scans.* Use Microsoft Defender Vulnerability Scanning to conduct vulnerability assessments of your VMs and related resources. Regularly check for any security issues or misconfigurations in your VM setup that could expose your models. [Microsoft Defender Vulnerability Scanning](/azure/defender-for-cloud/deploy-vulnerability-assessment-defender-vulnerability-management).

## Cost optimization

Cost optimization involves aligning resource usage with workload requirements to avoid unnecessary expenses. Right-sizing VMs, committing to reserved instances, and setting up autoscaling help manage costs without compromising performance. Controlling costs on Azure infrastructure is vital for long-term sustainability and scalability of AI deployments.

- *Commit to [Reserved Instances](https://azure.microsoft.com/pricing/reserved-vm-instances).* Save on virtual machine (VM) costs by committing to a one- or three-year term, which offers discounted rates.

- *Use Azure Virtual Machine Scale Sets for automatic scaling.* [Automatically scale](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview)  VM instances based on metrics like CPU usage, paying only for what you need and preventing over-provisioning.

- *Set automatic shutdowns for idle instances.* Avoid costs from unused resources by enabling automatic shutdown, especially for development and test environments.

- *Use [Azure Savings Plans](/azure/cost-management-billing/savings-plan/savings-plan-compute-overview) for predictable usage.* Reduce costs compared to pay-as-you-go pricing by committing to consistent usage across VM sizes and regions.

- *Use [Azure Spot instances](/azure/virtual-machines/spot-vms) for fault-tolerant workloads.* Get substantial discounts on spare capacity for workloads that can tolerate interruptions.

- *Select the right storage solution.* Balance cost and performance based on workload needs. Choose Azure Managed Lustre (AMLFS) for high-throughput, large-scale applications, and Azure NetApp Files (ANF) for advanced data management and reliability.

## Operational excellence

Operational excellence involves optimizing the configuration and management of Azure resources to improve the functionality of AI applications. Efficient resource allocation, performance tuning, and distributed training support smooth operation and adaptability to varying demands. This focus on operational efficiency ensures AI models perform as intended, without excessive resource use.

- *Optimize resource allocation.* Regularly review Azure VM sizes and configurations based on actual resource usage to match workload needs. Use Azure Advisor for recommendations on optimal sizing and scaling.

- *Configure autoscaling for efficiency.* Set up autoscaling for VMs or containers to handle workload demands without over-provisioning. Use Azure Virtual Machine Scale Sets to adjust resources dynamically based on demand. For more information, see [Azure Virtual Machine Scale Sets](/azure/virtual-machine-scale-sets/overview).

- *Conduct regular performance tuning.* Continuously profile the application to identify and resolve performance bottlenecks. Use [Application Insights Profiler](/azure/azure-monitor/profiler/profiler-overview) to analyze model code and resource usage.

- *Implement distributed training for efficiency.* Use distributed training techniques, if applicable, to reduce training time by using multiple VMs. Frameworks like Horovod and PyTorch support distributed training on Azure.

- *Save checkpoints in Azure Blob Storage.* Save model states, weights, and configurations periodically to Azure Blob Storage. You can use Azure SDKs or libraries available in the programming language you're using for the LLM. Store the checkpoints in a structured format, like TensorFlow SavedModel or PyTorch checkpoint files. Modify your training or inference code to include checkpoint logic. Start with setting intervals (after every epoch or some iterations) to save the model's state. Use a consistent naming convention for checkpoint files to track the most recent state easily.

- *Design for state recovery.* Ensure your application can recover from a saved checkpoint. Implement logic to load the model's state from Azure Blob Storage when the application starts. It includes, checking for existing checkpoints, and loading the most recent checkpoint if available, allowing the application to resume without losing progress.

## Performance efficiency

Performance efficiency refers to maximizing the processing power of Azure infrastructure to meet AI model demands. You should tune GPU settings, optimize input/output (I/O) processes, and run benchmarking tests to improve computational speed and responsiveness. Ensuring high performance supports the execution of complex AI models at scale, which enhances user satisfaction and reduces latency.

### GPU tuning

Increase the clock rate of a graphics processing unit (GPU) to improve performance, especially for tasks requiring high graphical processing or complex computations. Higher clock speeds allow the GPU to execute more operations in a given time period, enhancing overall efficiency. Use this [GPU-optimization script](https://github.com/Azure/azurehpc/tree/master/experimental/gpu_optimizations#gpu-optimization) to set the GPU clock frequencies to their maximum values.

- *Enable Accelerated Networking.* Accelerated Networking is a hardware acceleration technology that allows virtual machines to use single root I/O virtualization (SR-IOV) on supported virtual machines types. It provides lower latency, reduced jitter, and decreased CPU utilization. Enable accelerated Networking offers substantial enhancements in front-end network performance.

### I/O tuning

- *Optimize scratch storage.* Scratch needs to have high throughput and low latency. The training job requires reading data, processing it, and using this storage location as scratch space while the job runs. Ideally, you would use the local SSD directly on each VM. If you need a shared filesystem for scratch, combining all NVMe SSDs to create a Parallel File System (PFS) might be a great option in terms of cost and performance, assuming it has sufficient capacity. One method is to use [Azure Managed Lustre](/azure/azure-managed-lustre/amlfs-overview). If Azure Managed Lustre isn't suitable, you can explore storage options like [Azure NetApp Files](/azure/azure-netapp-files/azure-netapp-files-introduction) or [Azure Native Qumulo](/azure/partner-solutions/qumulo/qumulo-overview).

- *Implement checkpoint storage.* Large deep learning training jobs can run for weeks, depending on the number of VMs used. Just like any HPC cluster, you can encounter failures, such as InfiniBand issues, dual in-line memory module (DIMM) failures, error-correcting ode (ECC) errors in GPU memory. It's critical to have a checkpointing strategy. Know the checkpoint interval (when data is saved). Understand how much data is transferred each time. Have a storage solution that meets capacity and performance requirements. Use Blob Storage, if it meets the performance needs.

### Benchmarking tests

Benchmarking tests help evaluate and improve distributed deep learning training performance on GPUs, especially for large-scale models. These tests measure the efficiency of GPU communication across nodes, aiming to reduce data transfer bottlenecks during distributed training. The three tests discussed include:

- *Megatron framework*: Supports large-scale language models by improving distributed training efficiency.
- *The NVIDIA Collective Communications Library (NCCL) and ROCm Communication Collectives Library (RCCL) tests*: Evaluate performance and accuracy in multi-GPU communication using NCCL or RCCL libraries, testing patterns like all-reduce and scatter.

These tests ensure scalability and optimal performance for LLMs, with Megatron focusing on model training and NCCL/RCCL on GPU communication.

### NVIDIA Megatron-LM test

NVIDIA Megatron-LM is an open-source framework for training large language models. It allows developers to create massive neural networks for NLP tasks, with features including:

- *Parallelism*: Supports model, data, and pipeline parallelism for billion-parameter models.
- *Scalability*: Scales across multiple GPUs and nodes for efficient large model training.
- *Flexibility*: Allows configuration of model architecture, data loading, and training strategies.
- *Optimizations*: Uses NVIDIA GPU optimizations for performance gains.

Megatron-LM deploys on Azure HPC infrastructure, and it uses Azure’s scalability for large language models without requiring on-premises hardware.

#### Megatron-LM test set up

Deploying Megatron-LM requires specific software and hardware.

- *Pick the right deployment options.* Use the [CycleCloud Workspace for Slurm](./cycle-cloud.md) to simplify deployment. Choose NC-series or ND-series SKUs for the GPU partition. For multi-node training, ND-series SKUs are recommended for RDMA support. Azure’s HPC marketplace images generally include these drivers and libraries. If customization is needed, the azhpc-images repository can ensure compatibility.

- *Use the right image.* The software requirements for the project include a Linux-based operating system, typically Ubuntu. For multi-GPU and multi-node communication, it's essential to have communication libraries such as NCCL and MPI. Additionally, appropriate NVIDIA drivers must be installed to ensure GPU acceleration. [Azure's HPC marketplace images](/azure/virtual-machines/azure-hpc-vm-images) come with these drivers and libraries preinstalled. However, if customization is necessary, the [azhpc-images](https://github.com/Azure/azhpc-images?tab=readme-ov-file#azure-hpcai-vm-images) repository can be used to ensure compatibility.

#### Megatron-LM test use

You should run Megatron-LM using the latest release of [NGC's PyTorch container](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/pytorch). To run the container against a traditional Slurm-based HPC cluster, you need to install and configure these other components in your cluster:

- [enroot](https://github.com/NVIDIA/enroot): A tool that allows users to run containerized applications on HPC clusters without requiring root privileges or modifying the host system.
- [pyxis](https://github.com/NVIDIA/pyxis): A plugin for Slurm that enables seamless integration of enroot with Slurm, allowing users to submit containerized jobs to Slurm queues and run them on HPC nodes.

Both of these components are included in [CycleCloud Workspace for Slurm](./cycle-cloud.md) but are currently not included in Slurm clusters that are built via CycleCloud. You can introduce these extra components via [cluster-init with CycleCloud projects](/azure/cyclecloud/how-to/projects). With these requirements met, you can use Megatron-LM for LLM training by:

- *Verifying the performance of your cluster*: Identify any potential hardware issues before running your workload with [Node Health Checks](https://github.com/Azure/azurehpc-health-checks). Use NCCL tests to verify the distributed all-reduce performance of the cluster.
- *Selecting your training data*: Use the [codeParrot](https://huggingface.co/codeparrot/codeparrot-small) model as a starting point to validate your workflow.
- *Preprocessing your data*: Use the [preprocess\_data.py](https://github.com/NVIDIA/Megatron-LM/tree/main) script within the Megatron-LM repository to convert your data to a format that is compatible with Megatron-LM.
- *Training with Megatron-LM*: Use the [examples](https://github.com/NVIDIA/Megatron-LM/tree/main/examples) within Megatron-LM as a reference to configure Megatron for training.

This setup ensures efficient deployment and training of large language models on Azure’s infrastructure.

### NCCL bandwidth test

To verify and optimize GPU communication across nodes, run the NCCL bandwidth test. The NCCL bandwidth test is specialized tool within NCCL, a library that facilitates high-speed communication between GPUs. NCCL supports collective operations, including all-reduce, all-gather, reduce, broadcast, and reduce-scatter, across single or multi-GPU nodes, and achieves optimal performance on platforms with PCIe, NVLink, NVswitch, or networking setups like InfiniBand or TCP/IP. For more information, see [NVIDIA/NCCL tests](https://github.com/nvidia/nccl).

#### NCCL performance metrics

Use the NCCL bandwidth test to assess key metrics, including time and bandwidth. "Time" (in milliseconds) measures the overhead or latency in operations, making it useful for evaluating operations with small data sizes. "Bandwidth" (in GB/s) evaluates point-to-point operation efficiency, such as Send/Receive. "Bus bandwidth" reflects hardware usage efficiency by accounting for inter-GPU communication speed and bottlenecks in components like NVLink or PCI. Calculations for various collective operations are provided, such as AllReduce, ReduceScatter, AllGather, Broadcast, and Reduce.

#### NCCL test initiation

To initiate these tests within a CycleCloud deployment, connect to the scheduler node via SSH and access a GPU-equipped compute node. Clone the Git repository for NCCL tests, navigate to the `nccl-tests` directory, and create a host file listing the nodes for testing. Obtain the scheduler node’s IP address from CycleCloud’s web app.

### NCCL test arguments

Before running tests, specify different [arguments](https://github.com/nvidia/nccl-tests?tab=readme-ov-file#arguments) like the number of GPUs per thread (`-g`), data size range (`-b` for minimum bytes and `-e` for maximum bytes), step increment (`-i` or `-f`), reduction operation type (`-o`), datatype (`-d`), root device (`-r`), iteration count (`-n`), warmup count (`-w`), and CUDA graph settings (`-G`). Refer to the NCCL test documentation for a full list of adjustable parameters.

### RCCL tests

ROCm Communication Collectives Library (RCCL) is a specialized library designed for efficient communication between AMD GPUs. It provides collective operations such as all-reduce, all-gather, broadcast, and reduce, supporting both intra- and inter-node GPU communication. Optimized for platforms using PCIe and networking technologies like InfiniBand, RCCL ensures scalable data transfer in multi-GPU environments. It supports integration into both single- and multi-process workflows, such as those using MPI. For more information, see [ROCm Communication Collectives Library](https://github.com/rocm/rccl#rccl)

- *Set Up Environment.* Install ROCm and ensure RCCL is properly installed on all nodes.
- *Build RCCL Tests.* Clone the repository, navigate to the rccl-tests directory, and compile the tests.
- *Run Bandwidth Tests.* Use the provided test executables (rccl-tests), specifying communication operations like all-reduce.
- *Analyze Performance.* Compare bandwidth and latency results across nodes and GPUs.

## Next step

> [!div class="nextstepaction"]
> [Govern AI](../govern.md)



---
File: /platform/architectures.md
---

---
title: Get AI architecture guidance for Azure platform services (PaaS) for AI
description: Find AI architectures and guides to build AI workloads with Azure AI platform services like Azure AI Foundry, Azure OpenAI, Azure Machine Learning, and Azure AI Services.
author: stephen-sumner
ms.author: ssumner
ms.date: 07/01/2025
ms.topic: conceptual
---

# Get AI architecture guidance for Azure platform services (PaaS) for AI

This article helps organizations build AI workloads on Azure platform-as-a-service (PaaS) solutions. These services support both generative and nongenerative AI workloads with enterprise-grade security and scalability.

## Use generative AI architectures and guides

Generative AI architectures create new content and enable conversational experiences through large language models. The architectures provide different complexity levels to match your organization's needs and technical maturity. You must select the appropriate architecture based on your organization's size, compliance requirements, and existing Azure infrastructure. Here's how:

1. **Start with baseline architectures that provide proven design patterns for production workloads.** These architectures include security configurations, networking designs, and operational practices that enterprises need for reliable AI deployments. They address common challenges like model governance, cost management, and data protection.

   | Article | Article type | Target organization |
   |---------|--------------|---------------------|
   | [Baseline Azure AI Foundry chat reference architecture in an Azure landing zone](/azure/architecture/ai-ml/architecture/baseline-azure-ai-foundry-landing-zone) | Architecture | Enterprise |
   | [Baseline Azure AI Foundry chat reference architecture](/azure/architecture/ai-ml/architecture/baseline-azure-ai-foundry-chat) | Architecture | Any |
   | [Basic Azure AI Foundry chat reference architecture](/azure/architecture/ai-ml/architecture/basic-azure-ai-foundry-chat) | Architecture | Startup |

2. **Apply operational guidance that supports AI development lifecycle management.** These guides establish practices for model deployment, monitoring, and continuous improvement across development environments. They ensure consistent quality and reliability as AI applications evolve.

   | Article | Article type | Target organization |
   |---------|--------------|---------------------|
   | [GenAIOps](/azure/architecture/ai-ml/guide/genaiops-for-mlops) | Guide | Any |
   | [Developing RAG solutions](/azure/architecture/ai-ml/guide/rag/rag-solution-design-and-evaluation-guide) | Guide | Any |
   | [Proxy Azure OpenAI usage](/azure/architecture/ai-ml/guide/azure-openai-gateway-guide) | Guide | Any |

3. **Implement Well-Architected design areas that address specific technical concerns for AI workloads.** These design areas provide detailed recommendations for application design, data management, and operational excellence that complement the architectural patterns.

   | Article | Article type | Target organization |
   |---------|--------------|---------------------|
   | [Application design](/azure/well-architected/ai/application-design) | Design area | Any |
   | [Application platform](/azure/well-architected/ai/application-platform) | Design area | Any |
   | [Training data design](/azure/well-architected/ai/training-data-design) | Design area | Any |
   | [Grounding data design](/azure/well-architected/ai/grounding-data-design) | Design area | Any |
   | [Data platform](/azure/well-architected/ai/data-platform) | Design area | Any |
   | [MLOps and GenAIOps](/azure/well-architected/ai/mlops-genaiops) | Design area | Any |
   | [Operations](/azure/well-architected/ai/operations) | Design area | Any |
   | [Test and evaluate](/azure/well-architected/ai/test) | Design area | Any |
   | [Responsible AI](/azure/well-architected/ai/responsible-ai) | Design area | Any |

## Use nongenerative AI architectures and guides

Nongenerative AI architectures focus on classification, prediction, and analysis tasks without creating new content. These architectures process existing data to extract insights, automate decisions, and enhance business processes. You must choose architectures that align with your specific data processing and analysis requirements.

Here's how:

1. **Select specialized architectures that address specific use cases for data processing and analysis.** These architectures demonstrate proven patterns for common business scenarios like document processing, media analysis, and predictive analytics. They provide implementation guidance for integrating AI capabilities into existing business processes.

   | Article | Article type | Target organization |
   |---------|--------------|---------------------|
   | [Document processing architectures](/azure/architecture/ai-ml/architecture/automate-document-classification-durable-functions) | Architecture | Any |
   | [Video and image classification architecture](/azure/architecture/ai-ml/architecture/analyze-video-computer-vision-machine-learning) | Architecture | Any |
   | [Audio processing architecture](/azure/architecture/ai-ml/openai/architecture/call-center-openai-analytics) | Architecture | Any |
   | [Predictive analytics architecture](/azure/architecture/ai-ml/idea/personalized-offers) | Architecture | Any |

2. **Apply operational frameworks that support machine learning model lifecycle management.** These guides establish best practices for model training, deployment, and monitoring that ensure consistent performance and reliability in production environments.

   | Article | Article type | Target organization |
   |---------|--------------|---------------------|
   | [Azure Machine Learning](/azure/architecture/ai-ml/#azure-machine-learning) | Guide | Any |
   | [MLOps](/azure/architecture/ai-ml/guide/machine-learning-operations-v2) | Guide | Any |

## Adopt AI standards

The following articles provide best practices for adopting AI workloads using Azure PaaS solutions. These practices ensure your AI workloads meet requirements for security, governance, and operational excellence across key categories.

- **[Resource selection](./resource-selection.md)** - Use best practices to choose appropriate AI services and compute resources.
- **[Networking](./networking.md)** - Apply best practices to design secure and performant network connectivity.
- **[Governance](./governance.md)** - Follow best practices to establish policies and controls for AI resource management.
- **[Management](./management.md)** - Implement best practices for monitoring and operational practices.
- **[Security](./security.md)** - Enforce best practices for applying security controls and compliance requirements.

## Azure resources

| Category | Tool | Description |
|----------|------|-------------|
| Platform Services | [Azure AI Foundry](/azure/ai-foundry/what-is-azure-ai-foundry) | Unified platform for building and deploying generative and nongenerative AI applications |
| Platform Services | [Azure OpenAI](/azure/ai-services/openai/) | Access to OpenAI models with enterprise security and compliance |
| Platform Services | [Azure Machine Learning](/azure/machine-learning/overview-what-is-azure-machine-learning) | End-to-end machine learning lifecycle management platform |
| Platform Services | [Azure AI Services](/azure/ai-services/what-are-ai-services) | Prebuilt AI capabilities for vision, speech, language, and decision making |
| Architecture Guidance | [Azure Architecture Center AI/ML](/azure/architecture/ai-ml/) | Comprehensive collection of AI and machine learning architecture patterns |
| Best Practices | [Well-Architected Framework AI Workloads](/azure/well-architected/ai/get-started) | Design principles and recommendations for AI workloads on Azure |

## Next steps

> [!div class="nextstepaction"]
> [Resource selection](./resource-selection.md)


---
File: /platform/governance.md
---

---
title: Govern Azure platform services (PaaS) for AI
description: Learn how to govern AI workloads using Azure AI platform services (PaaS) with recommendations and best practices.
author: stephen-sumner
ms.author: ssumner
ms.date: 04/29/2025
ms.topic: conceptual
---

# Govern Azure platform services (PaaS) for AI

This article provides governance recommendations for organizations that use Azure AI platform-as-a-service (PaaS) solutions. These recommendations help you establish responsible AI practices that reduce security, cost, and compliance risks while ensuring your AI investments align with business objectives.

## Govern AI platforms

AI platform governance applies policy controls across Azure AI services to ensure consistent operations. Platform-level governance enforces security, compliance, and operational standards across your AI ecosystem. You must implement comprehensive policies to maintain oversight and strengthen AI management practices. Here's how:

1. **Apply built-in governance policies for each AI platform.** Azure Policy provides predefined policy definitions that address common governance requirements for AI services. These policies help enforce security configurations, cost controls, and compliance requirements without custom development. Use Azure Policy to implement built-in policy definitions for [Azure AI Foundry](/azure/ai-foundry/how-to/azure-policy), [Azure AI services](/azure/ai-services/policy-reference), and [Azure AI Search](/azure/search/policy-reference).

2. **Enable Azure landing zone AI policies for comprehensive coverage.** Azure landing zones include curated policy sets that address workload-specific governance requirements. These policies provide tested configurations that align with Microsoft recommendations for AI workloads. Select the appropriate policy initiative under the *Workload Specific Compliance* category during Azure landing zone deployment, including [Azure OpenAI](https://www.azadvertizer.net/azpolicyinitiativesadvertizer/Enforce-Guardrails-OpenAI.html), [Azure Machine Learning](https://www.azadvertizer.net/azpolicyinitiativesadvertizer/Enforce-Guardrails-MachineLearning.html), [Azure AI Search](https://www.azadvertizer.net/azpolicyinitiativesadvertizer/Enforce-Guardrails-CognitiveServices.html), and [Azure Bot services](https://www.azadvertizer.net/azpolicyinitiativesadvertizer/Enforce-Guardrails-BotService.html).

## Govern AI models

Model governance controls ensure AI models produce safe, reliable, and ethical outputs. Clear policies for model inputs and outputs protect against harmful content generation and misuse while maintaining compliance standards. You must implement systematic model oversight to protect users and support responsible AI deployment practices. Here's how:

1. **Create and maintain an AI agent inventory.** Microsoft Entra Agent ID provides a centralized view of all AI agents created through Azure AI Foundry and Copilot Studio. A complete inventory enables access control enforcement and policy compliance monitoring across your organization. Use [Microsoft Entra Agent ID](/entra/identity/monitoring-health/concept-sign-ins#microsoft-entra-agent-id) to track and manage your AI agents.

2. **Enforce model restrictions.** Azure Policy allows you to control which AI models your organization can use. Apply [model-specific policies](/azure/ai-foundry/how-to/built-in-policy-model-deployment) in Azure AI Foundry to ensure compliance with organizational standards and requirements.

3. **Implement AI risk detection processes.** Use Defender for Cloud to [identify AI workloads](/azure/defender-for-cloud/identify-ai-workload-model) and [assess risks](/azure/defender-for-cloud/explore-ai-risk) before deployment. Conduct regular [red team assessments](/azure/ai-services/openai/concepts/red-teaming) of generative AI models. Document all findings and update governance policies to address new risks.

    | Step                          | Action                                                                                     | Description                                                                                       |
    |-------------------------------|--------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
    | Enable Defender for Cloud AI workload discovery | Use Defender for Cloud to identify AI workloads and assess risks before deployment. | This step ensures visibility into AI workloads and helps detect potential vulnerabilities early. |
    | Schedule regular red team assessments | Conduct red team assessments of generative AI models periodically.                   | Regular assessments help identify weaknesses and improve the security posture of AI models.      |
    | Document and track identified risks | Maintain a record of risks discovered during assessments.                             | Tracking risks ensures accountability and supports continuous improvement in governance policies.|
    | Update policies based on findings | Revise governance policies to address newly identified risks.                          | Policy updates ensure that governance measures remain effective and aligned with current risks. |

4. **Apply content safety controls across all models.** [Azure AI Content Safety](/azure/ai-services/content-safety/overview) provides filters that prevent harmful content generation. Consistent application maintains safety standards and reduces legal liability from inappropriate AI outputs.

5. **Apply model grounding techniques.** Control AI model outputs through [system messages](/azure/ai-services/openai/concepts/system-message) and [retrieval augmented generation](/azure/ai-studio/concepts/retrieval-augmented-generation) (RAG). Test grounding effectiveness with tools like [PyRIT](https://github.com/Azure/PyRIT) to ensure consistent and appropriate responses.

## Govern AI costs

Cost management controls prevent unnecessary AI spending while maximizing operational efficiency. Effective controls ensure AI investments align with business objectives and prevent budget overruns from resource misuse. You must implement financial oversight and resource optimization practices to maintain cost-effective AI operations. Here's how:

1. **Select the appropriate billing model for your workload patterns.** Commitment tiers and provisioned throughput provide predictable costs for stable workloads. Azure OpenAI models offer [provisioned throughput units](/azure/ai-services/openai/concepts/provisioned-throughput) (PTUs) that cost less than pay-as-you-go pricing for consistent usage patterns. Combine PTU endpoints with consumption-based endpoints to handle traffic spikes cost-effectively. Use PTUs for primary endpoints and consumption-based endpoints for overflow traffic. For more guidance, see [Introduce a gateway for multiple Azure OpenAI instances](/azure/architecture/ai-ml/guide/azure-openai-gateway-multi-backend#multiple-azure-openai-instances-in-a-single-region-and-single-subscription).

2. **Choose models that match requirements without overspending.** Model selection directly impacts costs while affecting capability requirements. Less expensive models often provide sufficient performance for many use cases without sacrificing necessary functionality. For Azure AI Foundry, see [Azure AI Foundry pricing](https://azure.microsoft.com/pricing/details/ai-foundry/?cdn=disable) and [model billing information](/azure/ai-studio/how-to/model-catalog-overview#billing). Use Azure Policy definitions to [allow specific models](/azure/ai-foundry/how-to/built-in-policy-model-deployment) that meet cost requirements.

3. **Set quotas and limits to prevent cost overruns.** Provisioning quotas control resource allocation and prevent unexpected charges. Allocate quotas for each model based on expected workloads. Monitor dynamic quotas continuously to ensure they match actual demand and adjust them to maintain optimal throughput without overspending.

4. **Select cost-effective deployment options.** Azure AI Foundry models provide different [deployment options](/azure/ai-foundry/concepts/deployments-overview). Choose the most cost-effective and compliant option for your use case.

5. **Control client usage patterns.** Client behavior directly affects consumption costs in pay-per-use services. Limit client access through security protocols like network controls, keys, and role-based access control (RBAC). Enforce API constraints like max tokens and max completions. Batch requests when possible to optimize efficiency and keep prompts concise while providing necessary context to reduce token consumption.

6. **Automate resource shutdown for non-production workloads.** Automatic shutdown prevents unnecessary compute costs during idle periods. Define and enforce policies requiring AI resources to use automatic shutdown features on virtual machines and compute instances in Azure AI Foundry and Azure Machine Learning. Apply automatic shutdown to non-production environments and production workloads that can go offline during specific periods.

7. **Implement gateway controls for cost management.** A [generative AI gateway](/azure/api-management/genai-gateway-capabilities) provides centralized cost controls across AI endpoints. The gateway tracks token usage, throttles consumption, applies circuit breakers, and routes traffic to different endpoints to optimize costs.

For additional cost management guidance, see [Manage AI costs](../manage.md#manage-ai-costs) and [cost optimization](/azure/architecture/ai-ml/architecture/baseline-azure-ai-foundry-chat#cost-optimization) in the baseline Azure AI Foundry chat reference architecture.

## Govern AI security

AI security governance protects AI workloads from threats that compromise data, models, or infrastructure. Security controls safeguard systems against unauthorized access and data breaches. You must implement comprehensive security measures to maintain AI solution integrity and reliability. Here's how:

1. **Enable comprehensive threat detection across all AI resources.** Microsoft Defender for Cloud provides security monitoring and threat detection for AI workloads. This service identifies misconfigurations and security risks before they become vulnerabilities. Enable [Defender for Cloud](/azure/defender-for-cloud/get-started) on every subscription and activate [AI threat protection](/azure/defender-for-cloud/ai-threat-protection) to monitor AI-specific security risks.

2. **Implement least privilege access controls.** Role-based access control (RBAC) limits user permissions to necessary functions only. This approach reduces attack surface and prevents unauthorized access to sensitive AI resources. Start with the Reader role for all users and elevate to Contributor role only when development work requires additional permissions. Use [custom roles](/azure/role-based-access-control/custom-roles) when built-in roles provide excessive permissions.

3. **Use managed identities for service authentication.** Managed identities eliminate the need to store credentials in code or configuration files. This approach reduces credential theft risks and simplifies authentication management. Implement [managed identity](/entra/identity/managed-identities-azure-resources/overview) on all supported Azure services that access AI model endpoints and grant least privilege access to application resources.

4. **Apply just-in-time access for administrative operations.** Privileged Identity Management (PIM) provides temporary elevated access when needed. This approach minimizes exposure time for high-privilege accounts and reduces security risks. Use [Privileged Identity Management](/entra/id-governance/privileged-identity-management/pim-configure) for administrative access to AI resources and require approval workflows for sensitive operations.

5. **Secure network access to AI endpoints.** Network controls prevent unauthorized access to AI services from untrusted networks. Private endpoints and virtual network integration protect AI resources from internet-based attacks. Configure [private endpoints](/azure/ai-services/cognitive-services-virtual-networks) for Azure AI services and use [virtual network service endpoints](/azure/virtual-network/virtual-network-service-endpoints-overview) to restrict access to approved networks only.

## Govern AI operations

AI operations governance establishes controls over AI service management and maintenance to ensure stable performance. Operations governance provides long-term reliability and consistent business value from AI investments. You must implement centralized oversight and continuity plans to prevent downtime and maintain operational effectiveness. Here's how:

1. **Establish model lifecycle management policies.** Model versioning policies ensure compatibility and smooth transitions between updates. Version control prevents disruptions when models are upgraded or retired and maintains system stability across deployments. Create policies that define model versioning standards, compatibility testing requirements, and rollback procedures for all AI platforms in your organization.

2. **Implement business continuity and disaster recovery plans.** Disaster recovery plans protect AI operations against service interruptions and data loss while ensuring business operations continue during outages. These plans maintain service availability for critical AI workloads. Configure baseline disaster recovery for resources that host AI model endpoints, including [Azure AI Foundry](/azure/ai-studio/how-to/disaster-recovery), [Azure OpenAI](/azure/ai-services/openai/how-to/business-continuity-disaster-recovery), and Azure AI services.

3. **Configure monitoring and alerting for AI workloads.** Baseline metrics provide early warning of performance degradation and operational issues before they affect users. Alert rules enable proactive responses to prevent service disruptions. Enable recommended alert rules for [Azure AI Search](/azure/search/monitor-azure-cognitive-search#azure-ai-search-alert-rules), [Azure AI Foundry Agent Service deployments](/azure/ai-foundry/agents/how-to/metrics), and individual Azure AI services.

## Govern AI regulatory compliance

AI regulatory compliance establishes controls to meet industry standards and legal requirements for AI deployments. Compliance controls reduce liability risks and build stakeholder trust while avoiding regulatory penalties. You must implement systematic compliance processes to maintain regulatory alignment and demonstrate responsible AI practices. Here's how:

1. **Automate compliance assessment and management processes.** Microsoft Purview Compliance Manager provides centralized compliance tracking across cloud environments. Automated assessment reduces manual oversight burden and ensures consistent compliance monitoring. Use [Microsoft Purview Compliance Manager](/microsoft-365/compliance/compliance-manager-overview) to assess compliance status and apply [regulatory compliance initiatives](/azure/governance/policy/samples/#regulatory-compliance) in Azure Policy for your industry requirements.

1. **Develop industry-specific compliance frameworks.** Regulatory requirements vary across industries and geographic locations. Custom compliance frameworks address specific obligations for your business context. Create compliance checklists that reflect regulatory demands relevant to your industry and use standards like ISO/IEC 23053:2022 (Framework for Artificial Intelligence Systems Using Machine Learning) to audit policies applied to your AI workloads.

## Govern AI data

AI data governance protects sensitive information and intellectual property while ensuring high-quality AI outputs. Data controls prevent unauthorized access and maintain regulatory compliance across AI workloads. You must implement comprehensive data protection measures to safeguard privacy and maintain AI solution integrity. Here's how:

1. **Implement centralized data discovery and classification.** Microsoft Purview provides unified data governance across organizational systems. Centralized classification ensures consistent data handling standards and regulatory compliance. Use [Microsoft Purview](/purview/data-governance-overview) to scan, catalog, and classify data from systems across your organization and implement [Microsoft Purview SDKs](/purview/developer/microsoft-purview-sdk-documentation-overview) to enforce compliance policies programmatically.

2. **Maintain data security boundaries across AI systems.** Data security boundaries prevent sensitive information from reaching unauthorized AI endpoints. Indexing processes can remove existing security controls around data sources. Ensure that data ingested into AI models meets classification standards and undergoes security review before use in AI applications.

3. **Prevent copyright infringement in AI outputs.** Content filtering systems protect against intellectual property violations in AI-generated content. Copyright protection reduces legal risks and maintains ethical AI practices. Use [Protected material detection in Azure AI Content Safety](/azure/ai-services/content-safety/concepts/protected-material) to filter copyrighted material and ensure that training or fine-tuning data uses legally obtained and properly licensed sources.

4. **Establish version control for AI training data.** Version control for grounding data ensures consistency and enables rollback capabilities. Data versioning maintains deployment stability and supports change management across AI systems. Implement version control processes for grounding data in retrieval augmented generation (RAG) implementations to track changes and maintain consistency across deployments.

## Next step

> [!div class="nextstepaction"]
> [Management PaaS AI](../platform/management.md)



---
File: /platform/management.md
---

---
title: Manage Azure platform services (PaaS) for AI
description: Learn how to manage AI workloads using Azure AI platform services (PaaS) with recommendations and best practices.
author: stephen-sumner
ms.author: ssumner
ms.date: 07/01/2025
ms.topic: conceptual
---

# Manage Azure platform services (PaaS) for AI

This article offers management recommendations for organizations running AI workloads on Azure. It focuses on Azure platform-as-a-service (PaaS) solutions for AI.

## Manage AI deployments

Consistent deployment configurations enhance security, compliance, and operational efficiency across all AI environments. Organizations that standardize their deployment approach reduce configuration drift and ensure reliable performance. You must implement systematic deployment practices that align with your business requirements. Here's how:

1. **Select the appropriate operating model for your organization.** Deployment models create logical boundaries such as data domains or business functions to ensure autonomy, governance, and cost tracking. Deploy an instance of Azure AI Foundry for each business unit because sharing a single instance across multiple business units limits cost tracking and creates resource constraints. Define a project per use case and use hub-based projects only when teams require shared resources. For more information, see [What type of Azure AI Foundry project do I need?](/azure/ai-foundry/what-is-azure-ai-foundry#project-types) and [AI Foundry resource types](/azure/ai-foundry/concepts/resource-types).

2. **Deploy to regions that meet your requirements.** Model placement depends on specific latency, throughput, and compliance requirements that determine optimal performance. Check the Azure region [product availability](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/table) table to confirm support for required hardware, features, and data-residency rules before deployment to ensure performance and regulatory alignment.

3. **Monitor AI deployment resources continuously.** Resource monitoring captures performance data and identifies issues before they affect users. Diagnostic settings capture logs and metrics for all key services including [Azure AI Foundry and Azure AI services](/azure/ai-services/diagnostic-logging). This monitoring provides visibility into system health and enables proactive issue resolution. See also [Azure Monitor Baseline Alerts](https://azure.github.io/azure-monitor-baseline-alerts/patterns/artificial-intelligence/).

4. **Manage deployment resources centrally.** Centralized resource management provides consistent oversight and control across all AI deployments. Use the [Management center](/azure/ai-foundry/concepts/management-center) in Azure AI Foundry to configure Foundry projects, track resource utilization, and govern access. This approach ensures standardized resource allocation and cost control. Also [monitor costs in Azure AI Foundry](/azure/ai-foundry/concepts/management-center).

5. **Use Azure API Management as a unified gateway for multiple deployments.** API Management provides consistent security, scalability, rate limiting, token quotas, and centralized monitoring when onboarding multiple applications or teams. This approach standardizes access patterns and reduces management overhead across your AI services. For more information, see [Access Azure OpenAI and other language models through a gateway](/azure/architecture/ai-ml/guide/azure-openai-gateway-guide).

## Manage AI models

Model monitoring ensures outputs align with Responsible AI principles and maintain accuracy over time. AI models experience drift due to changing data, user behaviors, or external factors that can lead to inaccurate results or ethical concerns. You must implement continuous monitoring to detect and address these changes proactively. Here's how:

1. **Monitor model outputs for quality and alignment.** Monitoring processes ensure workloads remain aligned with responsible AI targets and deliver expected results. Use Azure AI Foundry's [observability features](/azure/ai-foundry/concepts/observability) and [monitor applications](/azure/ai-foundry/how-to/monitor-applications). For Azure AI Foundry Agent Service, [monitor agent deployments](/azure/ai-foundry/agents/how-to/metrics).

2. **Track model performance metrics continuously.** Performance monitoring helps pinpoint issues when accuracy or response quality drops below acceptable thresholds. Monitor latency in response times and accuracy of vector search results through [tracing](/azure/ai-studio/how-to/develop/trace-local-sdk) in Azure AI Foundry.

3. **Consider implementing a generative AI gateway for enhanced monitoring.** Azure API Management enables logging and monitoring capabilities that platforms don't provide natively, including source IP collection, input text tracking, and output text analysis. This approach provides comprehensive audit trails and monitoring data. For more information, see [Implement logging and monitoring for Azure OpenAI Service language models](/azure/architecture/ai-ml/openai/architecture/log-monitor-azure-openai).

4. **Choose compute.** In Azure AI Foundry, compute resources support essential [model deployments](/azure/ai-foundry/concepts/foundry-models-overview#model-deployment-managed-compute-and-serverless-api-deployments) and [fine-tuning](/azure/ai-foundry/concepts/fine-tuning-overview#serverless-or-managed-compute). Standardize compute types, runtimes, and shutdown periods across compute instances, clusters, and serverless options.

## Manage AI data

Data quality determines the accuracy and reliability of AI model outputs. Organizations that maintain high-quality data standards achieve better model performance and reduce the risk of biased or inaccurate results. You must implement systematic data management practices to ensure consistent model quality. Here's how:

1. **Monitor data drift continuously.** Data drift detection identifies when input data patterns change from training baselines, which can degrade model performance over time. Track accuracy and data drift in both generative and nongenerative AI workloads to ensure models remain relevant and responsive to current conditions. Use [evaluations in Azure AI Foundry](/azure/ai-studio/concepts/evaluation-approach-gen-ai) to establish monitoring baselines and detection thresholds.

2. **Set up automated alerts for performance degradation.** Alert systems provide early warning when model performance drops below acceptable thresholds, enabling proactive intervention before issues affect users. Configure custom alerts to detect performance deviations and trigger remediation workflows when models require retraining or adjustment.

3. **Ensure quality data processing standards.** Data preparation requirements differ between AI workload types but must maintain consistent quality standards across all implementations. For generative AI, structure grounding data in the correct format with appropriate chunking, enrichment, and embedding for optimal AI model consumption. For more information, see [Guide to designing and developing a RAG solution](/azure/architecture/ai-ml/guide/rag/rag-solution-design-and-evaluation-guide).

## Implement business continuity

Business continuity ensures AI services remain available during regional outages or service disruptions. Service interruptions can affect critical business operations that depend on AI capabilities, making continuity planning essential for organizational resilience. You must implement multi-region deployment strategies to maintain service availability. Here's how:

1. **Deploy AI services across multiple regions.** Multi-region deployments provide redundancy that maintains service availability when individual regions experience outages or capacity constraints. Implement multi-region deployment strategies for [Azure AI Foundry](/azure/ai-studio/how-to/disaster-recovery#plan-for-multi-regional-deployment) and [Azure OpenAI](/azure/ai-services/openai/how-to/business-continuity-disaster-recovery) to ensure consistent service delivery.

2. **Configure automated failover mechanisms.** Automated failover reduces recovery time and ensures continuous service delivery when primary regions become unavailable. Set up traffic routing and load balancing between regions to enable seamless transitions during service disruptions.

## Next step

> [!div class="nextstepaction"]
> [Govern AI](../govern.md)


---
File: /platform/networking.md
---

---
title: Configure secure networking for Azure AI platform services
description: Learn how to implement secure networking for AI workloads using Azure platform services with actionable recommendations and best practices.
author: stephen-sumner
ms.author: ssumner
ms.date: 07/01/2025
ms.topic: conceptual
---

# Configure secure networking for Azure AI platform services

This article helps you implement secure networking for AI workloads on Azure platform services. You need secure networking to protect sensitive AI models, ensure data privacy, and maintain compliance requirements. Proper network configuration controls access to Azure AI Foundry and Azure AI Services while optimizing performance for model training and deployment.

## Use virtual networks

Virtual networks establish secure communication boundaries for AI services and prevent unauthorized access from public networks. Private endpoints eliminate public internet exposure while maintaining full service functionality and performance. You should use virtual networks with private endpoints to protect AI models, data, and services from external threats. Here's how:

1. **Create private endpoints for all AI platform services**. Private endpoints provide dedicated network interfaces within your virtual network that connect directly to Azure services. This configuration removes public internet exposure while maintaining full functionality and performance for your AI workloads. Use [private link for Azure AI Foundry](/azure/ai-foundry/how-to/configure-private-link?tabs=azure-portal&pivots=fdp-project) and apply the same restrictions to [Azure AI services](/azure/ai-services/cognitive-services-virtual-networks).

2. **Deploy supporting services within the network boundary**. Supporting services like Azure Storage, Azure Key Vault, and Azure Container Registry must operate within the same secure network boundary as your AI services. This configuration ensures consistent security posture across all components while maintaining proper access controls for your AI workload dependencies. Use private endpoints to connect these supporting services to your managed virtual networks as shown in the [Baseline Azure AI Foundry chat reference architecture](/azure/architecture/ai-ml/architecture/baseline-azure-ai-foundry-chat#architecture).

## Control network traffic

Network traffic control defines how data flows between AI services and external systems. Proper traffic restrictions protect sensitive AI data and ensure secure operations. You must implement traffic controls to safeguard AI workloads and maintain operational security. Here's how:

1. **Deploy secure access using jumpbox infrastructure**. Jumpbox access provides a centralized entry point into your AI network environment while maintaining strict security boundaries. This configuration prevents direct exposure of AI resources to external networks while enabling secure access. Use a jumpbox within your AI workload virtual network or a connectivity hub virtual network, and configure [Azure Bastion](/azure/bastion/bastion-overview) for secure RDP/SSH connectivity without exposing virtual machines to the public internet.

2. **Restrict outbound traffic to approved destinations**. Outbound traffic restrictions prevent unauthorized data exfiltration while allowing necessary communication for AI model training and inference. This approach protects AI models and training data while maintaining connectivity for legitimate operations. Limit outbound traffic to approved services and fully qualified domain names (FQDNs) as documented for [Azure AI services](/azure/ai-services/cognitive-services-data-loss-prevention) and [Azure AI Foundry](/azure/ai-studio/how-to/configure-managed-network).

3. **Prepare domain name resolution services**. Deploy Azure DNS infrastructure as part of your [Azure landing zone](/azure/cloud-adoption-framework/ready/azure-best-practices/dns-for-on-premises-and-azure-resources) and configure [conditional forwarders](/azure/private-link/private-endpoint-dns) for appropriate zones. This setup ensures reliable name resolution for secure communication between AI workloads and external systems.

4. **Configure network access controls**. Use [network security groups](/azure/virtual-network/network-security-groups-overview) (NSGs) to define and enforce access policies for inbound and outbound traffic. These controls implement the principle of least privilege, ensuring only essential communication is permitted.

5. **Use network monitoring services**. Monitor network performance and health using tools like Azure Monitor Network Insights and Azure Network Watcher. For advanced threat detection and response, integrate [Microsoft Sentinel](/azure/sentinel/overview) into your Azure network monitoring strategy.

6. **Deploy Azure Firewall to secure outbound traffic**. [Azure Firewall](/azure/firewall/overview) enforces security policies for outgoing traffic before it reaches the internet. Use it to control and monitor outbound traffic, enable SNAT for private IP translation, and ensure secure and identifiable outbound communication.

7. **Use Azure Web Application Firewall (WAF) for internet-facing workloads**. [Azure WAF](/azure/web-application-firewall/overview) protects AI workloads from common web vulnerabilities like SQL injections and cross-site scripting attacks. Configure Azure WAF on [Application Gateway](/azure/web-application-firewall/ag/ag-overview) to enhance security for workloads exposed to malicious web traffic.

## Azure resources

| Category | Tool | Description |
|----------|------|-------------|
| Network isolation | [Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) | Creates secure network boundaries and enables private communication between Azure resources |
| Private connectivity | [Azure Private Link](/azure/private-link/private-link-overview) | Provides private access to Azure services over the Microsoft backbone network |
| Secure access | [Azure Bastion](/azure/bastion/bastion-overview) | Delivers secure RDP/SSH connectivity without public IP exposure |
| DNS management | [Azure Private DNS](/azure/dns/private-dns-overview) | Manages private DNS zones for secure name resolution within virtual networks |
| API gateway | [Azure API Management](/azure/api-management/api-management-key-concepts) | Centralizes API management and security for AI service endpoints |
| Web security | [Azure Application Gateway](/azure/application-gateway/overview) | Provides secure HTTPS termination and web application firewall capabilities |
| Global delivery | [Azure Front Door](/azure/frontdoor/front-door-overview) | Offers global load balancing and secure edge connectivity for AI applications |

## Next step

> [!div class="nextstepaction"]
> [Governance](../platform/governance.md)



---
File: /platform/resource-selection.md
---

---
title: Select Azure Platform as a Service (PaaS) Solutions for AI
description: Learn how to select the right Azure AI services, compute, and tools to build effective generative and nongenerative AI workloads.
author: stephen-sumner
ms.author: ssumner
ms.date: 03/27/2025
ms.topic: conceptual
---

# Select Azure PaaS solutions for AI

This article describes how to choose appropriate resources for Azure AI platform as a service (PaaS) solutions. The following table provides an overview of the primary Azure AI PaaS solutions and important decision criteria.

| AI services | AI type | Description | Skills required |
|---------|------------|---------| --- |
| [Azure AI Foundry](/azure/ai-foundry/what-is-azure-ai-foundry) | Generative AI and nongenerative AI | A platform for building and deploying generative and nongenerative AI applications | Developer and data science skills |
| [Azure AI services](/azure/ai-services/what-are-ai-services) | Generative AI and nongenerative AI | Various services that provide prebuilt generative and nongenerative AI models | Developer skills |
| [Azure OpenAI](/azure/ai-foundry/openai/concepts/models) | Generative AI | A service for accessing OpenAI models | Developer and data science skills |
| [Azure Machine Learning](/azure/machine-learning/overview-what-is-azure-machine-learning) | Machine learning | A service for training and deploying machine learning models | Developer skills and advanced data science skills |

## Select resources for generative AI workloads

Generative AI combines various resources to process input data and generate meaningful outputs. Select the right resources to ensure that applications, such as applications that use [retrieval-augmented generation (RAG)](/azure/architecture/ai-ml/guide/rag/rag-solution-design-and-evaluation-guide), deliver accurate results by grounding AI models effectively.

:::image type="content" source="../images/generative-ai-app.svg" alt-text="Diagram that shows the basic components of a generative AI workload." lightbox="../images/generative-ai-app.svg" border="false":::

### Generative AI workflow

The following workflow corresponds to the preceding diagram:

1. The AI app receives a query from the user. 

1. An orchestrator, such as Azure AI Foundry Agent Service, Semantic Kernel, or LangChain, manages the data flow.

1. A search and retrieval mechanism identifies the appropriate grounding data.

1. The mechanism sends the grounding data to a generative AI platform.

1. The generative AI platform generates a response based on the user query and grounding data.

### Generative AI resource selection

Use the following recommendations to build generative RAG workloads:

1. **Choose a generative AI platform.** Use Azure AI Foundry or Azure OpenAI to deploy and manage generative AI models. Azure AI Foundry provides a code-first platform that includes built-in tools to develop, deploy, and orchestrate applications. Use Azure OpenAI if you only need access to [OpenAI models](/azure/ai-services/openai/concepts/models).

1. **Choose the appropriate AI compute type.** Azure AI Foundry requires [compute instances](/azure/ai-studio/how-to/create-manage-compute) for specific capabilities. Select a compute type that meets your performance and budget needs.

1. **Pick an orchestrator.** Use popular orchestrators like [Azure AI Foundry Agent Service](/azure/ai-foundry/agents/overview), [Semantic Kernel](/semantic-kernel/overview/), or [LangChain](https://python.langchain.com/v0.2/docs/integrations/platforms/microsoft/) to manage data flow and interactions. For workloads that have multiple collaborating agents, your orchestrator must support the [AI agent orchestration patterns](/azure/architecture/ai-ml/guide/ai-agent-design-patterns) that you use.

1. **Pick a search and knowledge retrieval mechanism.** To ground generative AI models, create an index or vector database for relevant data retrieval. Use Azure AI Search to build traditional and vector indexes from various [data sources](/azure/search/search-indexer-overview#supported-data-sources), apply [data chunking](/azure/search/vector-search-integrated-vectorization), and use [multiple query types](/azure/search/search-query-overview#types-of-queries). For structured databases, consider [Azure Cosmos DB](/azure/cosmos-db/vector-database), [Azure Database for PostgreSQL](/azure/postgresql/flexible-server/how-to-use-pgvector), or [Azure Cache for Redis](/azure/azure-cache-for-redis/cache-overview-vector-similarity).

1. **Choose a data source for grounding data.** Store grounding data in Azure Blob Storage for images, audio, video, or large datasets. Alternatively, use databases that [AI Search](/azure/search/search-indexer-overview#supported-data-sources) or [vector databases](/dotnet/ai/conceptual/vector-databases#available-vector-database-solutions) support.

1. **Pick a compute platform.** Use the Azure [compute decision tree](/azure/architecture/guide/technology-choices/compute-decision-tree) to select the right platform for your workload.

## Select resources for nongenerative AI workloads

Nongenerative AI workloads use platforms, compute resources, data sources, and data processing tools to support machine learning tasks. Select the right resources to ensure that you can build AI workloads by using prebuilt or custom solutions effectively.

:::image type="content" source="../images/non-generative-ai-app.svg" alt-text="Diagram that shows the basic components of a nongenerative AI workload." lightbox="../images/non-generative-ai-app.svg" border="false":::

### Nongenerative AI workflow

The following workflow corresponds to the preceding diagram:

1. The AI app ingests incoming data.

1. An optional data processing mechanism extracts or manipulates the data.

1. An AI model endpoint analyzes the data.

1. Data can be used for training or fine-tuning of AI models.

### Nongenerative AI resource selection

Use the following recommendations to build nongenerative AI workloads:

1. **Choose a nongenerative AI platform.** Use AI services or Machine Learning based on your requirements. AI services provides prebuilt AI models that simplify deployment and reduce the need for deep data science expertise. Machine Learning provides a platform to develop custom machine learning models by using your data. It also integrates those models into your workloads.

1. **Choose the appropriate AI compute type.** Machine Learning requires [compute resources](/azure/machine-learning/concept-azure-machine-learning-v2) to run jobs or host endpoints. Select a compute type that meets your performance and budget needs. AI services don't require compute resources.

1. **Pick a data source.** Use supported [data sources](/azure/machine-learning/how-to-datastore) to host training data for Machine Learning. Many AI services don't require fine-tuning data. And some AI services, like Azure AI Custom Vision, allow you to upload local files to a managed data storage solution.

1. **Pick a compute platform.** Use the Azure [compute decision tree](/azure/architecture/guide/technology-choices/compute-decision-tree) to select the right platform for your workload.

1. **Pick a data processing service (optional).** Use Azure Functions to process serverless data or Azure Event Grid to trigger data processing pipelines.

## Next step

> [!div class="nextstepaction"]
> [Networking](../platform/networking.md)



---
File: /platform/security.md
---

---
title: Secure Azure platform services (PaaS) for AI
description: Learn how to secure AI workloads using Azure AI platform services (PaaS) with recommendations and best practices.
author: stephen-sumner
ms.author: ssumner
ms.date: 04/30/2025
ms.topic: conceptual
---

# Secure Azure platform services (PaaS) for AI

This article provides security recommendations for organizations that run AI workloads on Azure. These recommendations focus on Azure AI platform-as-a-service (PaaS) solutions. Organizations must protect AI resources from potential threats to maintain data integrity and compliance. Security baselines and well-architected frameworks help organizations safeguard their AI infrastructure against vulnerabilities.

## Secure AI resources

AI resource security requires security baselines and best practices to protect the infrastructure that supports AI workloads on Azure. This protection reduces risks from external threats and ensures consistent security across the organization. You must apply standardized security controls to maintain robust protection. Here's how:

1. **Apply Azure security baselines to all AI resources.** Azure security baselines provide standardized security controls that address common vulnerabilities across AI platforms. These baselines ensure consistent protection and reduce configuration errors that could expose your infrastructure. Use the [Azure security baselines](/security/benchmark/azure/security-baselines-overview) for each AI platform you deploy.

2. **Follow Azure Well-Architected Framework security guidance.** The Azure Well-Architected Framework provides service-specific security recommendations that complement baseline controls. These guidelines address unique security considerations for each AI service and help optimize your security posture. Review and implement the security recommendations in [Azure Service Guides](/azure/well-architected/service-guides/?product=popular) for your AI platforms.

## Secure AI models

AI model security protects against threats like prompt injection attacks and model manipulation that can compromise system integrity. Model security ensures AI systems provide reliable outputs and maintain organizational trust. You must implement comprehensive model protection to prevent malicious exploitation and maintain service reliability. Here's how:

1. **Enable threat protection for all AI models.** Microsoft Defender for Cloud provides continuous monitoring and detection capabilities that identify emerging threats before they compromise your AI infrastructure. This protection ensures consistent security coverage across all AI workloads and reduces response time to potential attacks. Deploy [Microsoft Defender for Cloud AI threat protection](/azure/defender-for-cloud/ai-threat-protection) to monitor for prompt injection attacks, model manipulation, and other AI-specific threats.

2. **Monitor outputs and apply prompt shielding.** Output monitoring detects malicious or unpredictable responses that could indicate successful attacks against your AI models. Prompt shielding prevents harmful user inputs from reaching your models and generating inappropriate responses. Implement [Prompt Shields](/azure/ai-services/content-safety/concepts/jailbreak-detection) to scan user inputs for attack patterns and regularly review model outputs for signs of compromise or manipulation.

3. **Verify model authenticity and integrity.** Model verification ensures only legitimate and secure AI models operate in your environment. This verification prevents unauthorized or tampered models from compromising your infrastructure and maintains trust in AI outputs. Establish verification processes that check model signatures, validate source authenticity, and confirm model integrity before deployment, especially for open-source models.

4. **Deploy an AI gateway for centralized security.** An AI gateway provides centralized traffic control and consistent security policy enforcement across all AI workloads. This approach simplifies security management and ensures uniform protection standards throughout your organization. Use [Azure API Management as an AI gateway](/azure/architecture/ai-ml/guide/azure-openai-gateway-guide) to enforce authentication policies, control traffic flow, and monitor API usage patterns. Configure the gateway's [managed identity with least privilege access](/azure/api-management/api-management-howto-use-managed-service-identity) and integrate with Microsoft Entra ID for [centralized authentication](/azure/architecture/ai-ml/guide/azure-openai-gateway-custom-authentication#general-recommendations).

## Secure AI access

AI access controls restrict resource usage to authorized users through authentication and authorization mechanisms. Access management prevents unauthorized interactions with AI models and protects sensitive data. You must implement comprehensive access controls to maintain security compliance and reduce breach risks. Here's how:

1. **Use Microsoft Entra ID for authentication instead of API keys.** Microsoft Entra ID provides centralized identity management with advanced security features that static API keys cannot offer. This approach eliminates credential management overhead and reduces security vulnerabilities from compromised keys. Replace API keys with Microsoft Entra ID authentication for [Azure AI Foundry](/azure/ai-services/authentication#authenticate-with-microsoft-entra-id), [Azure OpenAI](/azure/ai-services/openai/how-to/managed-identity), and [Azure AI Services](/azure/ai-services/authentication#authenticate-with-microsoft-entra-id). If you must use keys, [rotate keys](/azure/ai-services/rotate-keys) regularly and audit access.

2. **Maintain an inventory of AI agents.** An accurate inventory of AI agent identities provides the foundation for access management and policy enforcement. This inventory prevents shadow AI deployments and ensures all agents follow security standards. Use [Microsoft Entra Agent ID](/entra/identity/monitoring-health/concept-sign-ins#microsoft-entra-agent-id) to view all AI agents created through Azure AI Foundry and Copilot Studio.

3. **Configure multifactor authentication and privileged access.** Multifactor authentication adds an essential security layer that protects against credential compromise. Privileged access controls limit administrative exposure and reduce attack surfaces. Enable [multifactor authentication](/entra/identity/authentication/tutorial-enable-azure-mfa) for all users and implement [Privileged Identity Management](/entra/id-governance/privileged-identity-management/pim-configure) for administrative accounts to provide just-in-time access.

4. **Implement Conditional Access policies.** Conditional Access policies provide adaptive security that responds to risk indicators and context. These policies prevent unauthorized access while maintaining user productivity through intelligent access decisions. Configure [risk-based Conditional Access policies](/entra/id-protection/howto-identity-protection-configure-risk-policies) that require additional verification for unusual sign-in activity, restrict access by geographic location, and ensure only compliant devices access AI resources.

5. **Apply least privilege access principles.** Least privilege access minimizes security exposure by granting only necessary permissions for specific roles. This approach reduces the impact of potential breaches and prevents unauthorized resource access. Use [Azure role-based access control](/azure/ai-studio/concepts/rbac-ai-studio) to assign appropriate permissions based on job responsibilities and review access regularly to prevent privilege escalation.

6. **Secure service-to-service communication.** Service-to-service authentication eliminates credential management complexity while providing secure communication channels. This approach reduces security risks from stored credentials and simplifies access management. Use [managed identity](/entra/identity/managed-identities-azure-resources/overview) to authenticate Azure services without managing credentials.

7. **Control external access to AI endpoints.** External access controls ensure only authorized clients interact with AI models and provide comprehensive monitoring capabilities. This protection prevents unauthorized model usage and maintains service availability. Require Microsoft Entra ID authentication for AI model endpoints and consider Azure API Management as an AI gateway to enforce access policies and monitor usage patterns.

8. **Use Azure AI Foundry Management Center for governance.** Centralized management provides consistent access controls and resource governance across your AI infrastructure. This centralization ensures compliance with organizational standards and simplifies administrative overhead. Use the management center to control access to AI resources, manage quotas, and enforce governance policies.

## Secure AI data

Securing AI data means implementing data boundaries and access controls to prevent compliance violations and privacy breaches. You must implement strict data governance to ensure each AI application processes only appropriate datasets. Here's how:

1. **Define data boundaries based on user access levels.** Data boundaries establish clear separation between different information types based on user permissions and application scope. This separation prevents AI applications from exposing sensitive data to unauthorized users. Create distinct datasets for employee-facing applications (internal data), customer-facing applications (customer data), and public-facing applications (public data only).

2. **Implement dataset isolation for different AI applications.** Dataset isolation ensures each AI workload operates within its designated data environment without cross-contamination. This isolation reduces data leakage risks between applications with different security requirements. Use separate Azure storage accounts, databases, or data lakes for different AI applications, and configure access controls to prevent unauthorized cross-dataset access.

3. **Configure role-based data access controls.** Role-based controls ensure users and applications access only data appropriate for their function and clearance level. This approach reduces privilege escalation risks and unauthorized data exposure. Implement Azure RBAC policies that align data access permissions with user roles and application requirements.

4. **Use Microsoft Purview for data governance.** Microsoft Purview provides centralized data discovery, classification, and compliance management across your AI ecosystem. This tool maintains visibility into data usage and ensures compliance with organizational policies. Deploy [Microsoft Purview for Azure AI services](/purview/ai-azure-services) and [AI agents](/purview/ai-agents) to monitor data lineage, classify sensitive information, and enforce data governance policies.

## Secure AI execution

AI execution security protects against malicious code execution when AI agents run user-requested operations or autonomous processes. Execution security prevents system compromise and maintains infrastructure stability. You must implement comprehensive execution controls to protect against code injection attacks and resource exhaustion. Here's how:

1. **Isolate AI execution environments.** Environment isolation ensures each code execution operates in a controlled space that cannot affect other system components. This isolation prevents malicious code from compromising host systems or accessing unauthorized resources. Use [Dynamic Sessions in Azure Container Apps](/azure/container-apps/sessions?tabs=azure-cli) to create fresh, isolated environments for each execution that are automatically destroyed after completion.

2. **Review and approve execution code.** Code review processes identify security vulnerabilities and malicious patterns before deployment to production environments. This review prevents compromised scripts from executing and maintains code quality standards. Conduct thorough security reviews of all scripts before deployment, use version control systems to track changes, and ensure only approved code versions execute in your AI agents.

3. **Configure resource limits and timeouts.** Resource limits prevent individual executions from consuming excessive system resources that could disrupt other services. These controls maintain system stability and prevent denial-of-service conditions. Set CPU, memory, and disk usage limits for execution environments and configure automatic timeouts to terminate long-running or stuck processes.

4. **Monitor execution activity.** Execution monitoring provides visibility into AI agent behavior and helps detect malicious or unusual activity patterns. This monitoring enables rapid response to security incidents and maintains operational awareness. Log all execution activities, monitor resource usage patterns, and configure alerts for suspicious behavior or resource consumption anomalies.

For more information, see [Azure AI Foundry Agent Service](/azure/ai-foundry/agents/overview), [How to create Assistants with Azure OpenAI Service](/azure/ai-services/openai/how-to/assistant), [How to use Azure OpenAI Assistants function calling](/azure/ai-services/openai/how-to/assistant-functions), and [Agent implementation](/azure/cosmos-db/ai-agents#implementation-of-ai-agents).

## Azure resources

| Category | Tool | Description |
|----------|------|-------------|
| Security baselines | [Azure Machine Learning security baseline](/security/benchmark/azure/baselines/machine-learning-service-security-baseline) | Provides standardized security controls for Azure Machine Learning deployments |
| Security baselines | [Azure AI Foundry security baseline](/security/benchmark/azure/baselines/azure-ai-studio-security-baseline) | Offers security controls specific to Azure AI Foundry environments |
| Security baselines | [Azure OpenAI security baseline](/security/benchmark/azure/baselines/azure-openai-security-baseline) | Delivers security controls tailored for Azure OpenAI services |
| Architecture guidance | [Azure Machine Learning service guide](/azure/well-architected/service-guides/azure-machine-learning) | Provides comprehensive security recommendations for Azure Machine Learning |
| Architecture guidance | [Azure OpenAI service guide](/azure/well-architected/service-guides/azure-openai) | Offers security best practices specific to Azure OpenAI implementations |

## Next step

> [!div class="nextstepaction"]
> [Management](./management.md)


---
File: /center-of-excellence.md
---

---
title: Establish an AI Center of Excellence
description: Learn how to establish an AI Center of Excellence (AI CoE), an internal team of experts who drive AI adoption on Azure in your organization.
author: stephen-sumner
ms.author: pnp
ms.date: 06/09/2025
ms.update-cycle: 180-days
ms.topic: conceptual
ms.collection: ce-skilling-ai-copilot
---

# Establish an AI Center of Excellence

This article describes how to build an AI Center of Excellence (AI CoE) in your organization. An AI CoE consists of an internal team of experts who drive successful and valuable AI outcomes. The AI CoE prevents fragmented or ungoverned AI adoption. It establishes a strong foundation for AI initiatives and provides business and technical consultation that supports successful AI integration.

## Build the AI CoE team

An AI CoE team helps ensure consistent AI adoption across your organization. To be effective, the AI CoE needs the right leadership, expertise, and organizational alignment. To build your team, follow these steps:

1. **Secure executive sponsorship.** Executive sponsorship provides the budget, authority, and organizational credibility that the AI CoE needs to succeed. Without executive backing, the AI CoE can't enforce standards or drive organizational change. Form a steering committee with business and IT leaders, establish monthly progress reviews with sponsors, and ensure that the CoE has direct access to C-level decision makers.

1. **Appoint an AI CoE leader.** Assign a dedicated leader who drives AI initiatives and acts as the single point of contact for AI strategy implementation. A clear leader ensures accountability, strategic alignment, and effective communication. Select someone who has strong AI expertise, proven leadership skills, and the ability to influence stakeholders across all levels.

1. **Assemble the AI CoE team.** Build a multidisciplinary team that has advanced skills to support enterprise AI adoption. A diverse team addresses both technical and business requirements while maintaining security and governance standards. Business leaders identify relevant use cases, identify available data, and evaluate the model's effectiveness. AI technical experts handle data management, model design, training, adaptation, and selection. Include senior data scientists, machine learning engineers, AI governance experts, AI security specialists, and AI operations professionals in the team.

1. **Determine the placement within your organization.** Proper organizational alignment ensures effective collaboration with existing teams and access to resources. AI emerges alongside or after other existing technologies and relies on cloud infrastructure, data, and governance. It commonly builds on existing teams rather than being a standalone team. If you already operate a Cloud Center of Excellence (CCoE), integrate AI practices and expertise into that team. Only create a standalone AI team if current teams can't support AI adoption or if critical risks exist. The key is to avoid unnecessary complexity and to build AI adoption on strong foundations rather than operating in isolation.

1. **Define your operating model.** Companies at an early stage of their AI journey benefit from a centralized CoE to consolidate expertise and foundational practices. Centralization at the onset accelerates AI adoption. As your AI adoption matures, you should move toward an [advisory approach](#evolve-ai-coe-operations) where the AI CoE supports AI use. A centralized model ensures control and consistency, while an advisory approach provides flexibility.

## Define the responsibilities of the AI CoE

Clear responsibility creates accountability, closes governance gaps, and supports consistent implementation of AI initiatives. Your AI CoE should fulfill core responsibilities to define its operations, especially at the beginning of your AI adoption journey. Use the following table to assign AI CoE responsibilities.

| Area of focus | Responsibilities |
|---------------|------------------|
| **Define AI strategy** | Establish a clear AI strategy that aligns with business goals. The identification of use cases and organizational fit drives value in AI adoption. Work with business leaders to identify AI opportunities. Use the [AI decision tree](./strategy.md#define-an-ai-technology-strategy) to select the right AI solutions. Develop a [responsible AI strategy](./strategy.md#develop-a-responsible-ai-strategy) that guides ethical implementation. |
| **Develop AI skills** | Build organizational AI capabilities through skills assessments and development programs. [Assess current AI skills](./plan.md#assess-ai-skills). Implement [learning pathways](./plan.md#acquire-ai-skills) that employees can use to develop their skills. Provide hands-on experimentation opportunities to keep teams current. |
| **Lead pilot projects** | Run strategic pilot projects to validate AI approaches and demonstrate business value. Prioritize projects based on business impact and technical feasibility by [creating an AI proof of concept](./plan.md#validate-concepts-through-proof-of-concepts). Use the results to refine operational processes and improve CoE performance. |
| **Define and enforce AI standards** | Develop [governance policies](./govern.md) and [security standards](./secure.md) for data quality and model life cycle management. Document AI standards, integrate them into daily workflows, and monitor ethical AI use. Review models for bias and transparency. Conduct regular data security and compliance audits. |
| **Create intake and prioritization workflows** | Implement processes to evaluate and prioritize AI project requests. Create a structured intake process to collect and assess project requests. Apply consistent criteria for business value, technical feasibility, and resource requirements. Maintain a prioritized AI initiative backlog. |
| **Develop reusable assets** | Create compliance checklists and publish assets on an internal platform for reuse and knowledge sharing. |
| **Measure and report outcomes** | Implement frameworks to track AI adoption progress and business impact. Define key performance indicators such as adoption rates, compliance levels, and project cycle times. Regularly report insights to leadership. Use performance data to drive continuous improvement. |
| **Manage AI services** (optional) | Provide operational management and governance for deployed AI services and models. [Deploy and govern AI services](./manage.md#manage-ai-deployment). Monitor AI model performance and accuracy. Implement proper life cycle management for AI deployments. Build and maintain a library of templates, code repositories, and compliance tools. Develop templates for common AI use cases. Maintain code repositories that use proven patterns. |

## Evolve AI CoE operations

As AI adoption matures, the AI CoE should evolve from a centralized control to an advisory team. This transition is only possible when you can embed AI governance into your platform operations. To recognize when the AI CoE should transition to an advisory role, follow these steps:

1. **Recognize organizational inflection points.** Monitor key indicators that signal when centralized control is hindering rather than helping AI adoption. Early recognition prevents organizational friction and ensures continuous delivery momentum. Watch for approval delays and knowledge bottlenecks where AI experts in the CoE can't support all teams. You might see growing friction where product teams and the CoE frequently debate priorities instead of focusing on value delivery.

1. **Embed AI delivery into platform operations.** Transfer AI delivery to the [platform teams](../../strategy/prepare-organizational-alignment.md#understand-your-operating-models-readiness-for-cloud). Platform teams enforce consistent governance, manage reliable deployments, and help ensure secure delivery across all workloads. Embedding these functions scales standards to every team and maintains agility.

1. **Transition to an advisory model.** Replace the CoE gatekeeper model that blocks work with an advisory group that sets guardrails. Distribute AI expertise into product teams, platform teams, and enabling teams. Let frontline teams own delivery and implementation while forums provide policy and oversight. The CoE focuses on guidance and policy rather than direct control.

Shifting the CoE to an advisory role helps teams innovate rapidly while maintaining standards and security.

## Next step

Use the AI adoption checklists to determine your next step.

> [!div class="nextstepaction"]
> [AI checklists](index.md#ai-checklists)



---
File: /govern.md
---

---
title: Govern AI
description: Learn the process to govern AI with best practices and recommendations.
author: stephen-sumner
ms.author: ssumner
ms.date: 07/01/2025
ms.topic: conceptual
---

# Govern AI

This article helps you establish an organizational process for governing AI. You use this guidance to integrate AI risk management into your broader risk management strategies, creating a unified approach to AI, cybersecurity, and privacy governance. The process follows the [NIST Artificial Intelligence Risk Management Framework (AI RMF)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf) and [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook). The guidance aligns with the framework in [CAF Govern](/azure/cloud-adoption-framework/govern/).

## Assess AI organizational risks

AI risk assessment identifies potential risks that AI technologies introduce into your organization. This assessment builds trust in AI systems and reduces unintended consequences. You must conduct thorough risk assessments to ensure AI deployments align with your organization's values, risk tolerance, and operational goals. Here's how:

1. **Understand your AI workloads.** Each AI workload presents unique risks based on its purpose, scope, and implementation. You must clarify the specific function, data sources, and intended outcomes for each AI workload to map associated risks effectively. Document any assumptions and limitations related to each AI workload to establish clear boundaries for risk assessment.

1. **Use Responsible AI principles to identify risks.** Responsible AI principles provide a structured framework for comprehensive risk assessment. You must evaluate each AI workload against these principles to identify potential vulnerabilities and ethical concerns. Use the following table to guide your risk identification process:

    | Responsible AI principle    | Definition  | Risk assessment question    |
    |-----------------------------|-------------|----------------|
    | AI Privacy and Security      | AI workloads should respect privacy and be secure.  | How might AI workloads handle sensitive data or become vulnerable to security breaches?            |
    | Reliability and Safety       | AI workloads should perform safely and reliably.    | In what situations could AI workloads fail to operate safely or produce unreliable outcomes?   |
    | Fairness                     | AI workloads should treat people equitably.         | How could AI workloads lead to unequal treatment or unintended bias in decision-making? |
    | Inclusiveness                | AI workloads should be inclusive and empowering.     | How might certain groups be excluded or disadvantaged in the design or deployment of AI workloads?|
    | Transparency                 | AI workloads should be understandable.               | What aspects of AI decision-making could be difficult for users to understand or explain?|
    | Accountability               | People should be accountable for AI workloads.       | Where could accountability be unclear or difficult to establish in the development or use of AI?|

1. **Identify specific AI risks.** Risk identification requires systematic evaluation of security, operational, and ethical vulnerabilities. You must assess potential data breaches, unauthorized access, model manipulation, and misuse scenarios for each AI workload. Consult stakeholders from different departments to uncover risks that technical teams might overlook, and evaluate both quantitative impacts (financial losses, performance degradation) and qualitative impacts (reputational damage, user trust) to determine your organization's risk tolerance.

1. **Identify risks from external dependencies.** External dependencies introduce additional risk vectors that require careful evaluation. You must assess risks from third-party data sources, AI models, software libraries, and API integrations that your AI workloads depend on. Address potential issues such as security vulnerabilities, data quality problems, bias in external datasets, intellectual property conflicts, and vendor reliability by establishing clear policies that ensure external dependencies align with your organizational privacy, security, and compliance standards.

1. **Assess integration risks.** AI workloads rarely operate in isolation and create new risks when integrated with existing systems. You must evaluate how AI workloads connect with current applications, databases, and business processes to identify potential failure points. Document specific risks such as dependency cascades where AI failure affects multiple systems, increased system complexity that makes troubleshooting difficult, data format incompatibilities, performance bottlenecks, and security gaps at integration points that could compromise overall system functionality.

## Document AI governance policies

AI governance policies provide a structured framework for responsible AI use within your organization. These policies align AI activities with ethical standards, regulatory requirements, and business objectives. You must document policies that address identified AI risks based on your organization's risk tolerance. Here are AI governance policy examples:

| AI governance policy area | AI governance policy recommendations |
|-----------|----------------------|
| Define policies for selecting and onboarding models | ▪ *Establish policies for selecting AI models.* Policies should outline criteria for choosing models that meet organizational values, capabilities, and cost constraints. Review potential models for alignment with risk tolerance and intended task requirements.<br><br> ▪ *Onboard new models with structured policies.* A formal process for model onboarding maintains consistency in model justification, validation, and approval. Use sandbox environments for initial experiments, then validate and review models in the production catalog to avoid duplication. |
| Define policies for using third-party tools and data | ▪ *Set controls for third-party tools.* A vetting process for third-party tools safeguards against security, compliance, and alignment risks. Policies should include guidelines for data privacy, security, and ethical standards when using external datasets.<br><br> ▪ *Define data sensitivity standards.* Keeping sensitive and public data separate is essential for mitigating AI risks. Create policies around data handling and separation.<br><br> ▪ *Define data quality standards.* A "golden dataset" provides a reliable benchmark for AI model testing and evaluation. Establish clear policies for data consistency and quality to ensure high performance and trustworthy outputs. |
| Define policies for maintaining and monitoring models | ▪ *Specify retraining frequency by use case.* Frequent retraining supports accuracy for high-risk AI workloads. Define guidelines that consider the use case and risk level of each model, especially for sectors like healthcare and finance.<br><br> ▪ *Monitor for performance degradation.* Monitoring model performance over time helps detect issues before they affect outcomes. Document benchmarks, and if a model’s performance declines, initiate a retraining or review process. |
| Define policies for regulatory compliance     | ▪ *Comply with regional legal requirements.* Understanding regional laws ensures AI operations remain compliant across locations. Research applicable regulations for each deployment area, such as data privacy laws, ethical standards, and industry regulations.<br><br> ▪ *Develop region-specific policies.* Tailoring AI policies to regional considerations supports compliance with local standards. Policies might include language support, data storage protocols, and cultural adaptations.<br><br> ▪ *Adapt AI for regional variability.* Flexibility in AI workloads allows for location-specific functionality adjustments. For global operations, document region-specific adaptations like localized training data and feature restrictions. |
| Define policies for user conduct              | ▪ *Define risk mitigation strategies for misuse.* Misuse prevention policies help protect against intentional or unintentional harms. Outline possible misuse scenarios and incorporate controls, such as restricted functionalities or misuse detection features.<br><br> ▪ *Set user conduct guidelines.* User agreements clarify acceptable behaviors when interacting with the AI workload, reducing the risk of misuse. Draft clear terms of use to communicate standards and support responsible AI interaction. |
| Define policies for AI integration and replacement | ▪ *Outline integration policies.* Integration guidelines ensure AI workloads maintain data integrity and security during workload interfacing. Specify technical requirements, data-sharing protocols, and security measures.<br><br> ▪ *Plan for transition and replacement.* Transition policies provide structure when replacing old processes with AI workloads. Outline steps for phasing out legacy processes, training staff, and monitoring performance throughout the change. |

## Enforce AI governance policies

The enforcement of your AI governance policies maintains consistent and ethical AI practices across your organization. You should use automated tools and manual interventions ensure policy adherence across all AI deployments. Here's how:

1. **Automate policy enforcement where possible.** Automated enforcement reduces human error and ensures consistent policy application across all AI deployments. Automation provides real-time monitoring and immediate response to policy violations, which manual processes cannot match effectively. Use platforms like Azure Policy and Microsoft Purview to enforce policies automatically across AI deployments, and regularly assess areas where automation can improve policy adherence.

2. **Manually enforce AI policies where automation is insufficient.** Manual enforcement addresses complex scenarios that require human judgment and provides essential training for policy awareness. Human oversight ensures policies adapt to unique situations and maintains organizational understanding of AI governance principles. Provide AI risk and compliance training for employees to ensure they understand their role in AI governance, conduct regular workshops to keep staff updated on AI policies, and perform periodic audits to monitor adherence and identify areas for improvement.

3. **Use workload-specific governance guidance for targeted enforcement.** Workload-specific guidance addresses unique security and compliance requirements for different AI deployment patterns. This approach ensures policies align with the technical architecture and risk profile of each AI workload type. Use detailed security guidance available for AI workloads on Azure platform services (PaaS) and Azure infrastructure (IaaS) to govern AI models, resources, and data within these workload types.

    - [Govern PaaS AI](./platform/governance.md)
    - [Govern IaaS AI](./infrastructure/governance.md)

## Monitor AI organizational risks

Risk monitoring identifies emerging threats and ensures AI workloads operate as intended. Continuous evaluation maintains system reliability and prevents negative impacts. You must establish systematic monitoring to adapt to evolving conditions and address risks before they affect operations. Here's how:

1. **Establish procedures for ongoing risk evaluation.** Regular risk evaluations provide early detection of emerging threats and system degradation. You must create structured review processes that engage stakeholders from across your organization to assess broader AI impacts and maintain comprehensive risk awareness. Schedule quarterly risk assessments for high-risk AI workloads and annual assessments for lower-risk systems, and develop response plans that outline specific actions for different risk scenarios to enable rapid mitigation when issues arise.

2. **Develop a comprehensive measurement plan.** A structured measurement plan ensures consistent data collection and analysis across all AI workloads. You must define clear data collection methods that combine automated logging for operational metrics with surveys and interviews for qualitative feedback from users and stakeholders. Establish measurement frequency based on workload risk levels, focusing monitoring efforts on high-risk areas, and create feedback loops that use measurement results to refine risk assessments and improve monitoring processes.

3. **Quantify and qualify AI risks systematically.** Balanced risk measurement requires both quantitative metrics and qualitative indicators that align with each workload's specific purpose and risk profile. You must select appropriate quantitative metrics such as error rates, accuracy scores, and performance benchmarks alongside qualitative indicators including user feedback, ethical concerns, and stakeholder satisfaction. Benchmark performance against industry standards and regulatory requirements to track AI trustworthiness, effectiveness, and compliance over time.

4. **Document and report measurement outcomes consistently.** Systematic documentation and reporting enhance transparency and support informed decision-making across your organization. You must create standardized reports that summarize key metrics, significant findings, and any anomalies detected during monitoring activities. Share these insights with relevant stakeholders through regular briefings and use findings to refine risk mitigation strategies, update governance policies, and improve future AI deployments.

5. **Establish independent review processes.** Independent reviews provide objective assessments that internal teams might miss due to familiarity or bias. You must implement regular independent reviews using external auditors or uninvolved internal reviewers who can assess AI risks and compliance objectively. Use review findings to identify blind spots in your risk assessments, strengthen governance policies, and validate the effectiveness of your current monitoring approaches.

## Next step

> [!div class="nextstepaction"]
> [Manage AI](manage.md)

## Example AI risk mitigations

The following table lists some common AI risks and provides a mitigation strategy and a sample policy for each one. The table doesn't list a complete set of risks.

| Risk ID | AI risk| Mitigation | Policy|
|---|---|---|---|
| R001| Noncompliance with data protection laws| Use Microsoft Purview Compliance Manager to evaluate data compliance.|The Security Development Lifecycle must be implemented to ensure that all AI development and deployment complies with data protection laws.|
| R005| Lack of transparency in AI decision making | Apply a standardized framework and language to improve transparency in AI processes and decision making. | The NIST AI Risk Management Framework must be adopted and all AI models must be thoroughly documented to maintain transparency of all AI models.|
| R006| Inaccurate predictions | Use Azure API Management to track AI model metrics to ensure accuracy and reliability.|Continuous performance monitoring and human feedback must be used to ensure that AI model predictions are accurate. |
| R007| Adversarial attack | Use PyRIT to test AI workloads for vulnerabilities and strengthen defenses.|The Security Development Lifecycle and AI red team testing must be used to secure AI workloads against adversarial attacks. |
| R008| Insider threats| Use Microsoft Entra ID to enforce strict access controls that are based on roles and group memberships to limit insider access to sensitive data.| Strict identity and access management and continuous monitoring must be used to mitigate insider threats. |
| R009| Unexpected costs| Use Microsoft Cost Management to track CPU, GPU, memory, and storage usage to ensure efficient resource utilization and prevent cost spikes. |Monitoring and optimization of resource usage and automated detection of cost overruns must be used to manage unexpected costs.|
| R010| Underutilization of AI resources| Monitor AI service metrics, like request rates and response times, to optimize usage.| Performance metrics and automated scalability must be used to optimize AI resource utilization. |



---
File: /index.md
---

---
title: AI adoption
description: Discover how startups and enterprises can effectively adopt generative and nongenerative AI.
author: stephen-sumner
ms.author: ssumner
ms.date: 07/01/2025
ms.topic: conceptual
---

# AI adoption

The Cloud Adoption Framework (CAF) provides a structured process for adopting AI solutions in Azure. This framework outlines clear steps, many of which apply to Microsoft Copilot adoption.

The CAF AI adoption process supports organizations ranging from large enterprises to [startups](https://www.microsoft.com/startups). You learn how to identify AI use cases, select appropriate AI solutions, and build effective AI workloads. The guidance also covers operational processes required for governance, management, and security of AI implementations.

:::image type="content" source="./images/ai-adoption-process.svg" alt-text="Diagram showing the AI adoption process: AI Strategy, AI Plan, AI Ready, Govern AI, Manage AI, and Secure AI." lightbox="./images/ai-adoption-process.svg" border="false":::
*Figure 1. How to use the AI adoption guidance.*

## AI checklists

Use these AI checklists as a practical roadmap for adopting and managing AI. The enterprise checklist equips your organization to scale AI effectively. The startup checklist helps you quickly move toward production while adopting governance, management, and security best practices.

| AI adoption step | Applicable AI technology | Startup checklist | Enterprise checklist |
|---|---|---|---|
| [AI Strategy](./strategy.md) | Copilots<br>Azure | &#9744; [Define an AI technology strategy](./strategy.md#define-an-ai-technology-strategy) | &#9744; [Identify AI use cases](./strategy.md#identify-ai-use-cases) <br> &#9744; [Define an AI technology strategy](./strategy.md#define-an-ai-technology-strategy) <br> &#9744; [Develop an AI data strategy](./strategy.md#develop-an-ai-data-strategy) <br> &#9744; [Develop a responsible AI strategy](./strategy.md#develop-a-responsible-ai-strategy) |
| [AI Plan](./plan.md) | Copilots<br>Azure | &#9744; [Access AI resources](./plan.md#access-ai-resources) <br> &#9744; [Establish responsible AI](./plan.md#establish-responsible-ai-practices) | &#9744; [Assess AI skills](./plan.md#assess-ai-skills) <br> &#9744; [Acquire AI skills](./plan.md#acquire-ai-skills) <br> &#9744; [Access AI resources](./plan.md#access-ai-resources) <br> &#9744; [Prioritize AI use cases](./plan.md#prioritize-ai-use-cases) <br> &#9744; [Create an AI proof of concept](./plan.md#validate-concepts-through-proof-of-concepts) <br> &#9744; [Establish responsible AI](./plan.md#establish-responsible-ai-practices) <br> &#9744; [Estimate delivery timelines](./plan.md#estimate-delivery-timelines) |
| [AI Ready](./ready.md) | Azure | &#9744; [Build an AI environment](./ready.md#build-an-ai-environment) <br> &#9744; [Choose an architecture](./platform/architectures.md) | &#9744; [Establish AI governance](./ready.md#establish-governance-boundaries-for-ai-workloads) <br> &#9744; [Establish AI connectivity](./ready.md#establish-secure-connectivity-for-ai-workloads) <br> &#9744; [Establish AI reliability](./ready.md#establish-ai-reliability-across-regions) <br> &#9744; [Establish an AI foundation](./ready.md#use-an-azure-landing-zone) <br> &#9744; [Choose an architecture](./platform/architectures.md) <br> &#9744; [Use AI design areas](./platform/resource-selection.md) |
| [Govern AI](./govern.md) | Copilots<br>Azure | &#9744; [Enforce AI governance policies](./govern.md#enforce-ai-governance-policies) | &#9744; [Assess AI organizational risks](./govern.md#assess-ai-organizational-risks) <br> &#9744; [Document AI governance policies](./govern.md#document-ai-governance-policies) <br> &#9744; [Enforce AI policies](./govern.md#enforce-ai-governance-policies) <br> &#9744; [Monitor AI organizational risks](./govern.md#monitor-ai-organizational-risks) |
| [Manage AI](./manage.md) | Copilots<br>Azure | &#9744; [Manage AI models](./manage.md#manage-ai-models) <br> &#9744; [Manage AI costs](./manage.md#manage-ai-costs) | &#9744; [Manage AI operations](./manage.md#manage-ai-operations) <br> &#9744; [Manage AI deployment](./manage.md#manage-ai-deployment) <br> &#9744; [Manage AI models](./manage.md#manage-ai-models) <br> &#9744; [Manage AI costs](./manage.md#manage-ai-costs) <br> &#9744; [Manage AI data](./manage.md#manage-ai-data) <br> &#9744; [Manage AI business continuity](./manage.md#manage-ai-business-continuity) |
| [Secure AI](./secure.md) | Copilots<br>Azure | &#9744; [Protect AI resources and data](./secure.md#protect-ai-resources-and-data) | &#9744; [Discover AI security risks](./secure.md#discover-ai-security-risks) <br> &#9744; [Protect AI resources and data](./secure.md#protect-ai-resources-and-data) <br> &#9744; [Detect AI security threats](./secure.md#detect-ai-security-threats) |

## Next step

> [!div class="nextstepaction"]
> [AI Strategy](strategy.md)



---
File: /manage.md
---

---
title: Manage AI
description: Learn the process to manage AI with best practices and recommendations.
author: stephen-sumner
ms.author: ssumner
ms.date: 07/01/2025
ms.topic: conceptual
---

# Manage AI

This article provides guidance to manage AI workloads throughout their lifecycle. Organizations achieve consistent AI performance when they establish structured operational processes, implement proper deployment governance, and maintain comprehensive monitoring practices.

## Manage AI operations

Operational frameworks provide structure for managing complex AI projects. These frameworks ensure consistency across development teams and reduce errors that slow delivery cycles. You must establish clear operational processes to achieve reliable AI workload management. Here's how:

1. **Establish an AI center of excellence for strategic guidance.** An AI center of excellence provides strategic oversight and technical guidance for AI deployments across the organization. This group ensures that AI approaches align with business objectives and technical requirements. Use your [AI center of excellence](./center-of-excellence.md) to evaluate which management approach fits your organization's needs and create deployment standards that support governance and innovation.

1. **Select the right operational framework for your workload type.** Different AI workloads require different operational approaches that affect team processes and tooling decisions. This choice determines your development methodology and technology stack integration. Use [MLOps](/azure/architecture/ai-ml/guide/machine-learning-operations-v2) frameworks for traditional machine learning workflows and [GenAIOps](/azure/architecture/ai-ml/guide/genaiops-for-mlops) for generative AI workloads.

1. **Standardize development tools across all teams.** Consistent tooling eliminates compatibility problems between team environments and reduces learning curves for developers. This approach prevents integration issues and accelerates development cycles. Define and standardize the use of SDKs and APIs for consistency across development teams. For more information, see [Choose the right SDK to support your use case](/microsoft-365/agents-sdk/choose-agent-solution)

1. **Create dedicated sandbox environments for experimentation.** Sandbox environments allow safe testing without affecting production systems and provide teams freedom to test new approaches. These environments prevent experimental code from affecting stable workloads. Use a sandbox environment that remains distinct from dev, test, and production environments in the AI development lifecycle. Maintain consistency across dev, test, and prod environments to prevent breaking changes during promotion between environments.

1. **Simplify operations when possible.** New capabilities make it easier to customize and deploy agents and fine-tuned models without specialized expertise. Traditional fine-tuning requires expert data scientists to curate datasets and build task-specific pipelines, which creates operational complexity. Use [Copilot Tuning (preview)](/microsoft-copilot-studio/microsoft-copilot-fine-tune-model) in Microsoft 365 to fine-tune models for internal tasks without requiring specialized expertise.

## Manage AI deployment

AI deployment management defines who can deploy AI resources and governs these endpoints. A structured approach ensures organizations balance development speed with governance requirements. You must establish clear deployment authority to achieve consistent AI resource management. Here's how:

1. **Grant workload teams deployment authority within defined governance boundaries.** Workload teams accelerate development when they control AI resource deployment without waiting for central approval processes. This autonomy reduces bottlenecks and enables rapid response to business requirements while maintaining organizational standards. Use [Azure Policy](/azure/governance/policy/overview) to enforce governance consistently across workload environments and create AI policies that address governance gaps. For Azure AI Foundry, deploy an instance per business unit and use Azure AI Foundry projects for each use case within the business unit rather than creating a centralized shared resource across business units.

1. **Define clear AI deployment policies for both management approaches.** AI policies provide guardrails that prevent configuration drift and security gaps while ensuring compliance with organizational standards. These policies reduce the risk of unauthorized AI resource usage. Create AI policies to enforce content filter settings and prevent the use of disallowed models, then communicate these policies clearly to all teams. Conduct regular audits to ensure compliance.

1. **Create continuous integration and delivery pipelines for deployment.** Automated pipelines reduce manual errors and ensure consistent deployments across environments while providing repeatable processes that catch issues early. These pipelines maintain quality standards throughout development. Create data pipelines that cover code quality checks, unit and integration tests, and experimentation flows. Include production deployment steps with manual approval processes for promoting releases. Maintain separation between models and client interfaces to ensure independent component updates.

## Manage AI models

AI model management involves governance structures, continuous monitoring, and performance maintenance over time. This process helps organizations align models with ethical standards, track model performance, and ensure AI systems remain effective and aligned with business objectives. You must establish comprehensive model management processes to achieve reliable AI performance. Here's how:

1. **Define an AI measurement baseline for performance tracking.** Measurement baselines ensure AI models align with business goals and ethical standards. These baselines provide objective criteria for evaluating model performance and responsible AI compliance across your organization. Establish KPIs related to responsible AI principles like fairness, transparency, and accuracy, then map these KPIs to specific AI workloads.

1. **Identify root causes of performance issues quickly.** Visibility into each stage of AI interactions helps isolate problems and implement corrective actions efficiently, preventing cascading failures across systems. For example, determine whether chatbot errors originate from prompt crafting or model context understanding. Use built-in tools like Azure Monitor and Application Insights to identify performance bottlenecks and anomalies proactively.

1. **Retrain AI models based on performance criteria.** Models degrade over time due to data changes and require retraining to maintain relevance. Regular retraining ensures AI systems stay current with business needs and data patterns. Schedule retraining based on model performance metrics or business requirements to keep AI systems relevant. Assess initial training costs to evaluate optimal retraining frequency since retraining can be expensive. Maintain version control for models and ensure rollback mechanisms for underperforming versions.

1. **Establish model promotion processes with quality gates.** Quality gates ensure only validated models reach production environments. These processes prevent poorly performing models from affecting business operations and maintain consistent quality standards. Use performance criteria to promote trained, fine-tuned, and retrained models to higher environments. Define performance criteria that are unique to each application and establish clear promotion workflows that include testing and validation steps.

1. **Track model retirement schedules to prevent service disruptions.** Model retirement tracking prevents performance issues when vendor support ends. Organizations that miss retirement dates face unexpected service degradation or compatibility problems. Monitor retirement dates for pretrained models to maintain functionality when vendors deprecate services. For instance, update generative AI models before deprecation to maintain system functionality. Use [Azure AI Foundry portal](https://ai.azure.com?cid=learnDocs) to view model retirement dates for all deployments.

## Manage AI costs

AI cost management ensures organizations control expenses while maintaining performance across compute, storage, and token usage. Organizations need structured cost oversight and optimization strategies to prevent budget overruns and maximize resource efficiency. You must establish comprehensive cost management processes to achieve predictable AI spending. Here's how:

1. **Implement cost management best practices for each Azure AI service.** Different Azure AI services have unique pricing models and optimization features that affect total cost of ownership. Understanding service-specific cost structures helps organizations select the most cost-effective options for their workloads. For example, follow cost management guidance for [Azure AI Foundry](/azure/ai-studio/how-to/costs-plan-manage) to optimize expenses for each service type.

1. **Monitor usage patterns to maximize billing efficiency.** Understanding cost breakpoints prevents unnecessary charges and helps organizations optimize resource allocation. Tracking usage patterns reveals opportunities to adjust models and architecture for better cost performance. Monitor tokens per minute (TPM) and requests per minute (RPM) to understand usage patterns, then adjust models and architecture based on these patterns. Use fixed-price thresholds for services like image generation or hourly fine-tuning to avoid unexpected charges. Consider commitment-based billing models for consistent usage patterns to reduce overall costs.

1. **Establish automated cost monitoring and alerts.** Automated alerts prevent budget overruns by notifying teams of unexpected charges before they impact project budgets. These alerts enable proactive cost management and help organizations maintain financial control over AI initiatives. Set up budget alerts in Azure Cost Management to track spending against predefined thresholds and establish budgeting strategies that align with business objectives. Create alerts at multiple thresholds to provide early warning of cost increases.

## Manage AI data

AI data management ensures accuracy, integrity, and compliance throughout the AI lifecycle. Organizations need structured data governance and quality control processes to maintain reliable AI performance. You must establish comprehensive data management practices to achieve consistent AI outcomes. Here's how:

1. **Create and maintain golden datasets for consistent validation.** Golden datasets provide standardized benchmarks for testing AI models across different environments and versions. These authoritative datasets ensure consistent evaluation criteria and help detect performance degradation over time. Develop golden datasets that represent your production data patterns and use these datasets for regular testing and validation across all AI workloads. Update golden datasets regularly to reflect current business requirements and data patterns.

1. **Implement secure data pipelines with integrity controls.** Data pipeline integrity prevents corruption and ensures reliable AI model performance. Secure pipelines protect sensitive information and maintain data quality from collection through preprocessing and storage. Build custom data pipelines that include validation checks at each stage and implement security controls to protect data throughout the pipeline process. Use automated testing to verify data quality and consistency before feeding data into AI models.

1. **Monitor data sensitivity classifications and respond to changes.** Data sensitivity classifications change due to business requirements and regulatory updates. Organizations must track these changes and update AI systems accordingly to maintain compliance and security. Develop processes to identify when data sensitivity changes and implement procedures to remove or replace sensitive data in downstream AI systems. Use [Microsoft Defender for Cloud](/azure/defender-for-cloud/data-security-posture-enable) and [Microsoft Purview](/purview/purview-security) to label and manage sensitive data throughout your organization. When sensitivity changes occur, identify all AI models that use the affected data and retrain models with datasets that exclude the reclassified sensitive information.

## Manage AI business continuity

Business continuity management protects AI systems from disruptions and ensures rapid recovery when incidents occur. Organizations need multi-region strategies and tested recovery procedures to maintain AI service availability. Effective continuity planning prevents extended outages that affect business operations. You must establish comprehensive business continuity processes to achieve reliable AI system resilience. Here's how:

1. **Implement continuous monitoring across all AI components.** AI workloads change over time due to data evolution, model updates, or shifts in user behavior. Continuous monitoring detects these changes early and prevents performance degradation that affects business outcomes. Monitor [AI deployments](./platform/management.md#manage-ai-deployments), [AI models](./platform/management.md#manage-ai-models), and [AI data](./platform/management.md#manage-ai-data) to ensure workloads remain aligned with established KPIs. Conduct regular audits to assess AI systems against defined responsible AI principles and metrics.

1. **Deploy AI systems across multiple regions for high availability.** Multi-region deployments prevent single points of failure and ensure AI services remain accessible during regional outages. This approach provides geographic redundancy that protects against infrastructure failures and natural disasters. Deploy both generative and traditional AI systems across multiple Azure regions and implement necessary redundancy for trained and fine-tuned models to avoid retraining during outages. Use [Azure Front Door](/azure/frontdoor/front-door-overview) or [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview) to route traffic between regions automatically.

1. **Test disaster recovery plans regularly to validate effectiveness.** Regular testing identifies gaps in recovery procedures and ensures teams can restore AI systems effectively during real incidents. These tests validate that all components work together properly after recovery and help organizations refine their response procedures. Perform quarterly tests of disaster recovery plans that include data restoration processes and validation procedures for all AI components. Document test results and update recovery procedures based on lessons learned from each test cycle.

1. **Implement version control for all AI system components.** Version control systems track changes and enable quick restoration of previous configurations during recovery scenarios. This approach provides audit trails for modifications and ensures teams can identify and revert problematic changes efficiently. Use Git to manage changes to models, data pipelines, and system configurations across all AI workloads. Implement automated auditing that tracks model and system changes so teams can quickly identify and revert unplanned alterations that affect performance.

1. **Create automated backup strategies for AI assets.** Automated backups ensure critical AI components remain protected without manual intervention. These strategies prevent data loss and reduce recovery time when systems need restoration after incidents. Establish automated backup schedules for trained models, datasets, and configuration files using [Azure Backup](/azure/backup/backup-overview) or [Azure Storage](/azure/storage/common/storage-redundancy) with geo-redundant options. Store backups in separate regions from primary deployments to ensure availability during regional outages.

1. **Document recovery procedures with clear responsibilities.** Clear documentation ensures teams can execute recovery procedures consistently during high-stress situations. Documented procedures reduce recovery time and prevent errors that occur when teams operate without established guidelines. Create runbooks that define step-by-step recovery procedures for different failure scenarios and assign specific roles and responsibilities to team members for each recovery task. Update documentation regularly to reflect changes in AI architecture and recovery processes.

## Next step

> [!div class="nextstepaction"]
> [Secure AI](./secure.md)



---
File: /plan.md
---

---
title: Plan for AI adoption
description: Learn the process to plan for AI adoption with best practices and recommendations.
author: stephen-sumner
ms.author: ssumner
ms.date: 07/01/2025
ms.topic: conceptual
---

# Plan for AI adoption

This article helps you create an AI adoption plan that transforms your organization's AI strategy into actionable steps. An AI adoption plan bridges the gap between AI vision and execution. The plan ensures alignment between AI initiatives and business goals while addressing skill gaps, resource requirements, and implementation timelines.

## Assess AI skills

Current capability assessment prevents resource misallocation and ensures realistic project planning aligned with organizational readiness. AI projects fail when organizations attempt implementations beyond their technical maturity or data availability. You must evaluate your skills, data assets, and infrastructure to establish a foundation for successful AI adoption. Here's how:

1. **Measure your AI maturity level using the skills and data readiness framework.** The framework provides objective criteria to assess your organization's current AI capabilities. This measurement prevents overcommitting to projects beyond your current capabilities. Use the following table to assess your maturity:

   | AI maturity level | Skills required | Data readiness | Feasible AI use cases |
   |-------------------|-----------------|----------------|----------------------|
   | Level 1 | ▪ Basic understanding of AI concepts <br> ▪ Ability to integrate data sources and map out prompts | ▪ Minimal to zero data available <br> ▪ Enterprise data available | ▪ Azure quickstart projects <br> ▪ Any Copilot solution |
   | Level 2 | ▪ Experience with AI model selection <br> ▪ Familiarity with AI deployment and endpoint management <br> ▪ Experience with data cleaning and processing | ▪ Minimal to zero data available <br> ▪ Small, structured dataset <br> ▪ Small amount of domain-specific data available | ▪ Any Level 1 projects <br> ▪ Custom analytical AI workload using Azure AI services <br> ▪ Custom generative AI chat app without Retrieval Augmented Generation (RAG) in Azure AI Foundry <br> ▪ Custom machine learning app with automated model training <br> ▪ Fine-tuning a generative AI model |
   | Level 3 | ▪ Proficiency in prompt engineering <br> ▪ Proficiency in AI model selection, data chunking, and query processing <br> ▪ Proficiency in data preprocessing, cleaning, splitting, and validating <br> ▪ Grounding data for indexing | ▪ Large amounts of historical business data available for machine learning <br> ▪ Small amount of domain-specific data available | ▪ Any Level 1-2 projects <br> ▪ Generative AI app with RAG in Azure AI Foundry <br> ▪ Training and deploying a machine learning model <br> ▪ Training and running a small AI model on Azure Virtual Machines |
   | Level 4 | ▪ Advanced AI/machine learning expertise, including infrastructure management <br> ▪ Proficiency in handling complex AI model training workflows <br> ▪ Experience with orchestration, model benchmarking, and performance optimization <br> ▪ Strong skills in securing and managing AI endpoints | ▪ Large amounts of data available for training | ▪ Any Level 1-3 projects <br> ▪ Training and running large generative or non-generative AI apps on Virtual Machines, Azure Kubernetes Service, or Azure Container Apps |

2. **Inventory your data assets and evaluate their quality for AI use cases.** Data quality directly impacts AI model performance and determines which use cases you can implement successfully. This inventory reveals data preparation requirements and helps prioritize use cases based on available data. Document data sources, formats, quality, and accessibility across your organization.

3. **Review your technology infrastructure and determine AI readiness requirements.** Infrastructure capacity constrains AI project scope and influences deployment strategies. This review helps you plan infrastructure investments and select appropriate Azure services. Assess compute resources, storage capacity, network bandwidth, and security controls needed for your target AI use cases.

## Acquire AI skills

A comprehensive capability-building strategy ensures your organization has the skills needed to implement and maintain AI systems successfully. Skills gaps create project delays and increase the risk of implementation failures. You must develop a multi-faceted approach that combines training, hiring, and partnerships to build sustainable AI capabilities. Here's how:

1. **Develop internal AI skills through structured learning programs.** Internal skill development provides long-term capability building and ensures knowledge retention within your organization. This approach builds organizational confidence and reduces dependency on external resources. Use the [AI learning hub](/ai/) platform for free AI training, certifications, and product guidance. Set certification goals such as [Azure AI Fundamentals](/credentials/certifications/azure-ai-fundamentals/), [Azure AI Engineer Associate](/credentials/certifications/azure-ai-engineer/), and [Azure Data Scientist Associate](/credentials/certifications/azure-data-scientist/) certifications.

2. **Recruit AI professionals to fill critical skill gaps beyond internal capacity.** External recruitment provides immediate access to specialized expertise and accelerates project timelines. This strategy helps fill gaps that would take too long to develop internally. Hire experts in model development, generative AI, or AI ethics. Update job descriptions to reflect current skill needs and build an employer brand that emphasizes innovation and technical leadership.

3. **Partner with Microsoft experts to supplement your AI capabilities.** Microsoft partnerships provide access to proven expertise and industry best practices while reducing implementation risk. This approach accelerates learning and ensures alignment with Microsoft AI technologies. Use the [Microsoft partners marketplace](https://partner.microsoft.com/partnership/find-a-partner) to access AI, data, and Azure expertise across industries.

## Access AI resources

Clear access requirements and licensing strategies prevent deployment delays and ensure compliance with organizational policies. Different AI solutions have distinct access patterns that affect cost, security, and governance. You must understand the specific access requirements for each AI solution in your portfolio to plan budgets and security controls effectively. Here's how:

| Microsoft AI solution         | How to gain access                                                                                       |
|-------------------------------|----------------------------------------------------------------------------------------------------------|
| Microsoft 365 Copilot         | Requires a Microsoft 365 business or enterprise license with an additional Copilot license. See [Microsoft 365 Copilot](https://www.microsoft.com//microsoft-365/microsoft-copilot#plans). |
| Microsoft Copilot Studio      | Requires a standalone license or an add-on license. See [Microsoft Copilot Studio](/microsoft-copilot-studio/requirements-licensing-subscriptions). |
| In-product Copilots           | Requires access to the primary product. See [GitHub](https://azure.microsoft.com//products/github/copilot), [Power Apps](https://www.microsoft.com//power-platform/products/power-apps), [Power BI](https://www.microsoft.com//power-platform/products/power-bi), [Dynamics 365](https://www.microsoft.com//dynamics-365/solutions/ai), [Power Automate](https://www.microsoft.com//power-platform/products/power-automate), [Microsoft Fabric](/fabric/fundamentals/copilot-enable-fabric), and [Azure](https://azure.microsoft.com//products/copilot/). |
| Role-based Copilots           | Requires specific access requirements. See [Role-based agents for Microsoft 365 Copilot](https://www.microsoft.com/microsoft-365/copilot/copilot-for-work#role-based-agents) and [Microsoft Copilot for Security](https://www.microsoft.com/security/business/ai-machine-learning/microsoft-copilot-security). |
| Azure services                | Requires an [Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account/search). Includes Azure AI Foundry and Azure OpenAI. |

## Prioritize AI use cases

Strategic prioritization ensures you focus resources on projects that deliver maximum value while matching your organizational capabilities. Use case prioritization reduces implementation risk and accelerates time to value. You must evaluate each use case against feasibility, strategic value, and resource requirements to create an achievable implementation roadmap. Here's how:

1. **Evaluate use cases against your current AI maturity and available resources.** Realistic evaluation prevents overcommitting to projects beyond your current capabilities and ensures successful implementation. This assessment helps you focus on achievable goals that build momentum for future projects. Review your AI maturity level, data availability, technical infrastructure, and staffing capacity for each use case defined in your [AI Strategy](./strategy.md#identify-ai-use-cases).

2. **Rank use cases by strategic value and implementation feasibility.** Strategic ranking helps you allocate limited resources to projects with the highest potential impact and success probability. This approach maximizes return on AI investments while building organizational confidence. Score each use case on business impact, technical complexity, resource requirements, and alignment with organizational goals.

3. **Create a prioritized implementation roadmap with clear success criteria.** A structured roadmap provides clear direction for implementation teams and enables progress tracking against defined milestones. This roadmap helps manage stakeholder expectations and resource allocation. Select top-priority use cases and define specific success metrics, timelines, and resource requirements for each project.

## Validate concepts through proof of concepts

Proof of concepts reduce implementation risk by validating technical feasibility and business value before full-scale development. PoCs help identify potential challenges and refine requirements in a controlled environment. You must create focused validation projects that test core assumptions and gather data for informed decision-making. Here's how:

1. **Select an appropriate use case for proof of concept validation.** The right PoC selection balances learning opportunities with manageable risk and complexity. This selection ensures you gather meaningful insights without overwhelming your team or organization. Choose a high-value project from your prioritized list that matches your AI maturity level. Start with internal, non-customer-facing projects to limit risk and test your approach.

2. **Implement a focused proof of concept using Microsoft guidance and tools.** Structured implementation reduces development time and ensures you follow proven practices for your chosen AI approach. This approach maximizes learning while minimizing resource investment. Use the following implementation guides based on your AI type:

   | AI type | Implementation guide |
   |---------|---------------------|
   | Generative AI | Azure PaaS: [Azure AI Foundry](/azure/ai-studio/quickstarts/get-started-playground) and [Azure OpenAI](/azure/ai-services/openai/assistants-quickstart)<br><br>Microsoft Copilots: [Copilot Studio](/microsoft-copilot-studio/fundamentals-get-started) and [Microsoft 365 Copilot extensibility](/microsoft-365-copilot/extensibility/decision-guide) |
   | Machine learning | [Azure Machine Learning](/azure/machine-learning/tutorial-azure-ml-in-a-day) |
   | Analytical AI | Azure AI services with specific guides for [Content Safety](/azure/ai-services/content-safety/quickstart-jailbreak), [Custom Vision](/azure/ai-services/custom-vision-service/getting-started-build-a-classifier), [Document Intelligence](/azure/ai-services/document-intelligence/quickstarts/try-document-intelligence-studio), and other services |

3. **Use PoC results to refine your use case prioritization and implementation approach.** PoC insights reveal practical challenges and opportunities that inform future project planning and resource allocation. This feedback loop ensures your AI roadmap remains realistic and achievable. Document lessons learned, technical challenges, and business value demonstrated. Adjust your use case priorities based on proven feasibility and measured impact.

## Establish responsible AI practices

Responsible AI practices protect your organization from ethical, legal, and reputational risks while ensuring AI systems align with organizational values. Early integration of responsible AI principles prevents costly redesigns and builds stakeholder trust. You must embed ethical considerations, governance frameworks, and security measures into your implementation plan from the beginning. Here's how:

1. **Use responsible AI planning tools to evaluate potential impacts and design ethical systems.** Systematic evaluation tools help identify potential risks and ensure AI systems meet ethical standards and regulatory requirements. These tools provide structured approaches to complex ethical considerations. Use the [AI impact assessment template](https://www.microsoft.com/ai/tools-practices), [Human-AI eXperience Toolkit](https://www.microsoft.com/research/project/hax-toolkit/), and [Responsible AI Maturity Model](https://www.microsoft.com/research/publication/responsible-ai-maturity-model/) to guide your planning process.

2. **Implement AI governance frameworks to guide project decisions and monitor system behavior.** Governance frameworks provide consistent decision-making criteria and ensure accountability across AI projects. These frameworks help organizations maintain control over AI development and deployment. Establish policies covering roles, responsibilities, compliance requirements, and ethical standards. See [Govern AI](./govern.md) for detailed guidance on governance implementation.

3. **Apply AI security and operations best practices throughout the implementation lifecycle.** Security and operational excellence ensure AI systems remain reliable, secure, and cost-effective throughout their lifecycle. These practices prevent security incidents and operational failures. Implement AI operations frameworks like GenAIOps or MLOps for deployment tracking and performance monitoring. See [Manage AI](./manage.md) and [Secure AI](./secure.md) for detailed implementation guidance.

## Estimate delivery timelines

Realistic timeline estimation enables effective resource planning and stakeholder management while ensuring project success. Timeline accuracy depends on project complexity, organizational maturity, and resource availability. You must base timeline estimates on empirical data from your proof of concepts and organizational capabilities. Here's how:

1. **Use proof of concept results to estimate implementation timelines for each use case.** PoC data provides realistic baseline estimates that account for your organization's specific capabilities and constraints. This approach produces more accurate timelines than theoretical estimates. Document development time, testing cycles, and deployment complexity observed during PoC implementation.

2. **Account for organizational maturity and complexity factors in timeline planning.** Different AI solutions have characteristic implementation timelines that vary based on organizational readiness and project scope. This understanding helps set appropriate expectations with stakeholders. Microsoft Copilots typically provide the shortest timelines for return on investment (days to weeks), while custom Azure AI workloads require several weeks to months to reach production readiness.

3. **Build in buffer time for learning, iteration, and unexpected challenges.** AI projects often encounter unforeseen technical challenges and require multiple iterations to achieve desired outcomes. Buffer time prevents schedule pressure that could compromise quality or ethical considerations. Add 20-30% contingency time to initial estimates and plan for multiple development cycles.

## Azure resources

| Category | Tool | Description |
|----------|------|-------------|
| Learning & Certification | [AI learning hub](/ai/) | Provides free AI training, certifications, and product guidance for skill development |
| Assessment & Planning | [AI impact assessment template](https://www.microsoft.com/ai/tools-practices) | Evaluates social, economic, and ethical effects of AI initiatives |
| Development Platform | [Azure AI Foundry](/azure/ai-foundry/quickstarts/get-started-playground) | Development platform for building AI applications and agents with access to generative AI models and nongenerative models for vision, speech, language, and decision-making |
| Model Training | [Azure Machine Learning](/azure/machine-learning/tutorial-azure-ml-in-a-day) | End-to-end machine learning lifecycle management and model deployment |
| Conversational AI | [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-get-started) | Platform for building custom conversational AI agents and chatbots |
| Partner Network | [Microsoft partners marketplace](https://partner.microsoft.com/partnership/find-a-partner) | Access to certified partners with AI, data, and Azure expertise |

## Next step

Complete your AI adoption planning by establishing the technical foundation for implementation. For custom AI workloads with Azure, proceed to AI Ready to configure your technical environment. For Microsoft Copilot adoption, advance to AI Governance to establish organizational oversight.

> [!div class="nextstepaction"]
> [AI Ready (Azure only)](ready.md)

> [!div class="nextstepaction"]
> [Govern AI (Copilots and Azure)](ready.md)



---
File: /ready.md
---

---
title: AI Ready
description: Learn the process to build AI workloads in Azure with best practices and recommendations.
author: stephen-sumner
ms.author: ssumner
ms.date: 07/01/2025
ms.topic: conceptual
---

# AI Ready

This article outlines the organizational process for building AI workloads in Azure. The article provides recommendations for making key design and process decisions for adopting AI workloads at scale. It focuses on AI-specific guidance for resource organization and connectivity.

## Establish governance boundaries for AI workloads

AI governance requires proper resource organization and policy management to ensure secure, compliant, and cost-effective operations. You must create clear governance boundaries to protect sensitive data and control AI resource access effectively. Here's how:

1. **Create separate management groups for internet-facing and internal AI workloads.** Management group separation establishes critical data governance boundaries between external ("online") and internal-only ("corporate") AI applications. This separation prevents external users from accessing sensitive internal business data while you maintain appropriate access controls. The approach aligns with [Azure landing zone management group](/azure/cloud-adoption-framework/ready/landing-zone/design-area/resource-org-management-groups) architecture principles and supports policy inheritance across workload types.

2. **Apply AI-specific policies to each management group.** Start with baseline policies from [Azure landing zones](https://github.com/Azure/Enterprise-Scale/wiki/ALZ-Policies) and add Azure Policy definitions for [Azure AI Foundry](/azure/ai-foundry/how-to/built-in-policy-model-deployment), [Azure AI services](/azure/ai-services/policy-reference), [Azure AI Search](/azure/governance/policy/samples/built-in-policies#search), and [Azure Virtual Machines](/azure/virtual-machines/policy-reference). Policy enforcement ensures uniform AI governance across your platform and reduces manual compliance oversight.

3. **Deploy AI resources within workload-specific subscriptions.** AI resources must inherit governance policies from their workload management group rather than platform subscriptions. This separation prevents development bottlenecks that platform team controls create and enables workload teams to operate with appropriate autonomy. Deploy AI workloads to application landing zone subscriptions in Azure landing zone environments.

## Establish secure connectivity for AI workloads

AI networking encompasses network infrastructure design, security measures, and efficient data transfer patterns for AI workloads. You must implement proper security controls and connectivity options to prevent network-based disruptions and maintain consistent performance. Here's how:

1. **Activate Azure DDoS Protection for internet-facing AI workloads.** [Azure DDoS Protection](/azure/ddos-protection/ddos-protection-overview) safeguards your AI services from potential disruptions and downtime that distributed denial of service attacks cause. DDoS protection at the virtual network level defends against traffic floods that target internet-facing applications and maintains service availability during attacks.

2. **Secure operational access to AI workloads with Azure Bastion.** Use a jumpbox and Azure Bastion to secure operational access to AI workloads and prevent direct internet exposure of management interfaces. This approach creates a secure gateway for administrative tasks while maintaining network isolation for AI resources.

3. **Choose appropriate connectivity for on-premises data sources.** Organizations that transfer large amounts of data from on-premises sources to cloud environments need high-bandwidth connections to support AI workload performance requirements.

   - **Use Azure ExpressRoute for high-volume data transfer.** [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) provides dedicated connectivity for high data volumes, real-time processing, or workloads that require consistent performance. ExpressRoute includes a [FastPath](/azure/expressroute/about-fastpath) feature that improves data path performance by bypassing the ExpressRoute gateway for specific traffic flows.

   - **Use Azure VPN Gateway for moderate data transfer.** [Azure VPN Gateway](/azure/vpn-gateway/vpn-gateway-about-vpngateways) works well for moderate data volumes, infrequent data transfer, or when public internet access is required. VPN Gateway offers simpler setup and cost-effective operation for smaller datasets compared to ExpressRoute. Use the appropriate [topology and design](/azure/vpn-gateway/design) for your AI workloads, including site-to-site VPN for cross-premises connectivity and point-to-site VPN for secure device access.

## Establish AI reliability across regions

AI reliability requires strategic region placement and redundancy planning to ensure consistent performance and high availability. Organizations must address model hosting, data locality, and disaster recovery to maintain reliable AI services. You need to plan your regional deployment strategy to avoid service interruptions and optimize performance. Here's how:

1. **Deploy AI endpoints across multiple regions for production workloads.** Production AI workloads require hosting in at least two regions to provide redundancy and ensure high availability. Multi-region deployments enable faster failover and recovery during regional failures. For Azure OpenAI in Azure AI Foundry, use [global deployments](/azure/ai-services/openai/how-to/deployment-types#deployment-types) that automatically route requests to regions with available capacity. For regional deployments, implement [Azure API Management](/azure/api-management/genai-gateway-capabilities#backend-load-balancer-and-circuit-breaker) to load balance API requests across AI endpoints.

2. **Verify AI service availability in target regions before deployment.** Different regions provide varying levels of AI service availability and feature support. Check [Azure service availability by region](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/#products-by-region_tab5) to confirm your required AI services are available. Azure OpenAI deployment models include global standard, global provisioned, regional standard, and regional provisioned options with different regional availability patterns.

3. **Evaluate regional quota limits and capacity requirements.** Azure AI services have regional subscription limits that affect large-scale model deployments and inference workloads. Contact Azure support proactively when you anticipate capacity needs that exceed standard quotas to prevent service disruptions during scaling.

4. **Optimize data placement for retrieval-augmented generation applications.** Data storage location significantly affects application performance in RAG scenarios. Co-locating data with AI models in the same region reduces latency and improves data retrieval efficiency, though cross-region configurations remain viable for specific business requirements.

5. **Replicate critical AI assets to secondary regions for business continuity.** Business continuity requires replicating fine-tuned models, RAG datasets, trained models, and training data to secondary regions. Asset replication enables faster recovery during outages and maintains service availability across different failure scenarios.

## Establish an AI foundation

An AI foundation provides the core infrastructure and resource hierarchy that support AI workloads in Azure. It includes setting up scalable, secure environments that align with governance and operational needs. A strong AI foundation enables efficient deployment and management of AI workloads. It also ensures security and flexibility for future growth.

### Use an Azure landing zone

An [Azure landing zone](/azure/cloud-adoption-framework/ready/landing-zone/) is the recommended starting point that prepares your Azure environment. It provides a predefined setup for platform and application resources. Once the platform is in place, you can deploy AI workloads to dedicated application landing zones.

If your organization uses Azure landing zones for workloads, then continue to use them for workloads that use AI. You deploy your AI workloads to dedicated application landing zones. Figure 2 below illustrates how AI workloads integrate within an Azure landing zone.

:::image type="content" source="./images/azure-landing-zone-ai.svg" alt-text="Diagram showing AI workloads within an Azure landing zone." lightbox="./images/azure-landing-zone-ai.svg" border="false":::
*Figure 2. AI workload in an Azure landing zone.*

### Build an AI environment

If you don't use an Azure landing zone, follow the recommendations in this article to build your AI environment. The following diagram shows a baseline resource hierarchy. It segments internal AI workloads and internet-facing AI workloads. Internal workloads use policy to deny online access from customers. This separation safeguards internal data from exposure to external users. AI development should use a jumpbox to manage AI resources and data.

:::image type="content" source="./images/baseline-resource-hierarchy.svg" alt-text="Diagram showing the resource organization for internal and internet-facing AI workloads." lightbox="./images/baseline-resource-hierarchy.svg" border="false":::
*Figure 3. Baseline resource hierarchy for AI workloads.*

## Next steps

The next step is to build and deploy AI workloads to your AI environment. Use the following links to find the architecture guidance that meets your needs. Start with platform-as-a-service (PaaS) architectures. PaaS is Microsoft's recommended approach to adopting AI.

> [!div class="nextstepaction"]
> [PaaS AI architecture guidance](./platform/architectures.md)

> [!div class="nextstepaction"]
> [IaaS AI architecture guidance](./infrastructure/cycle-cloud.md)



---
File: /secure.md
---

---
title: Secure AI
description: Learn the process to secure AI with best practices and recommendations.
ms.author: ssumner
author: stephen-sumner
ms.date: 07/01/2025
ms.topic: conceptual
---

# Secure AI

This article helps you establish a security process for AI workloads in Azure. A secure AI environment supports business objectives and builds stakeholder confidence in AI solutions.

## Discover AI security risks

AI workloads create new attack surfaces that traditional security measures can't address. You must systematically evaluate AI-specific vulnerabilities to build effective defenses. Here's how:

1. **Identify AI system risks across your environment.** AI systems face evolving threats that require specialized evaluation frameworks to detect. These frameworks help you understand attack vectors specific to machine learning and AI workloads. Use frameworks like [MITRE ATLAS](https://atlas.mitre.org/) and [OWASP Generative AI risk](https://genai.owasp.org/) to identify risks across all AI workloads in your organization.

2. **Assess AI data risks throughout your workflows.** Sensitive data in AI workflows increases the risk of insider threats and data leaks that can compromise business operations. Data risk assessment helps you prioritize security investments based on actual exposure levels. Use tools like [Microsoft Purview Insider Risk Management](/purview/insider-risk-management) to assess enterprise-wide data risks and prioritize them based on data sensitivity levels.

3. **Test AI models for security vulnerabilities.** AI models contain unique vulnerabilities like data leakage, prompt injection, and model inversion that attackers can exploit. Real-world testing uncovers risks that static reviews can't detect. Test models for vulnerabilities using data-loss-prevention techniques and adversarial simulations, and red team both [generative AI](/azure/ai-services/openai/concepts/red-teaming) and nongenerative AI models to simulate real attacks.

4. **Conduct periodic risk assessments.** New threats emerge as AI models, usage patterns, and threat actors evolve over time. Regular assessments ensure your security posture adapts to changing risk landscapes. Run recurring assessments to identify vulnerabilities in models, data pipelines, and deployment environments, and use assessment findings to guide your risk mitigation priorities.

## Protect AI resources and data

AI systems contain valuable assets that require strong protection against unauthorized access and attacks. You must implement specific security controls to safeguard these critical resources.

### Secure AI resources

Comprehensive security measures protect your AI investments and maintain stakeholder trust in your AI solutions. You must apply targeted controls to secure all components of your AI infrastructure. Here's how:

1. **Create a complete AI asset inventory.** Unknown AI assets create security unguarded sides that attackers exploit to gain unauthorized access. A comprehensive inventory enables effective monitoring and rapid incident response for all AI components. Use [Azure Resource Graph Explorer](/azure/governance/resource-graph/) to discover AI resources across subscriptions, implement [Microsoft Defender for Cloud](/azure/defender-for-cloud/identify-ai-workload-model) to identify generative AI workloads, and maintain this inventory through automated scanning and regular validation.

2. **Secure all AI communication channels.** Exposed communication paths between AI components allow data interception and system compromise. Properly secured channels prevent unauthorized access and protect sensitive information in transit. Implement [managed identities](/entra/identity/managed-identities-azure-resources/overview) for secure authentication without stored credentials, use [virtual networks](/azure/ai-foundry/agents/how-to/virtual-networks) to isolate AI communications, and deploy [Azure API Management](/azure/api-management/export-rest-mcp-server) to secure Model Context Protocol server endpoints.

3. **Apply platform-specific security controls.** Different AI deployment models face distinct security threats based on their architecture and exposure points. Platform-tailored controls address the specific vulnerabilities present in each deployment type. Follow dedicated security guidance based on your deployment model:

    - [Azure PaaS security](./platform/security.md)
    - [Azure IaaS security](./infrastructure/security.md)

### Secure AI data

AI workloads rely on data and artifacts that require robust protection to prevent unauthorized access, data leaks, and compliance violations. You must implement comprehensive data security measures to protect AI data and artifacts. Here's how:

1. **Define and maintain data boundaries.** Clear data boundaries ensure AI workloads access only data appropriate for their intended audience and use case. Use [Microsoft Purview](/purview/purview-security) to classify data sensitivity and define access policies. Implement [Azure role-based access control (RBAC)](/azure/role-based-access-control/) to restrict data access by workload and user group. Use [Azure Private Link](/azure/private-link/) to create network-level data isolation between AI applications.

2. **Implement comprehensive data loss prevention.** Unauthorized data exposure through AI responses can compromise sensitive information and violate regulatory requirements. Data loss prevention controls prevent AI models from inadvertently revealing protected data in their outputs. Use [Microsoft Purview Data Loss Prevention](/purview/dlp-learn-about-dlp) to scan and block sensitive data in AI workflows. Configure [content filtering](/azure/ai-foundry/concepts/content-filtering) to prevent sensitive information leakage, and implement custom filters to detect and redact organization-specific sensitive data patterns. For Microsoft Copilot Studio, [Configure data loss prevention policies for agents](/microsoft-copilot-studio/admin-data-loss-prevention).

3. **Protect AI artifacts from compromise.** Unsecured AI models and datasets become targets for theft, poisoning, or reverse engineering attacks. Protected artifacts maintain intellectual property value and prevent malicious manipulation of AI systems. Store models and datasets in [Azure Blob Storage](/azure/storage/blobs/) with private endpoints, apply encryption at rest and in transit, and implement strict access policies with monitoring to detect unauthorized access attempts.

## Detect AI security threats

AI systems face evolving threats that require continuous monitoring to prevent security breaches and service disruptions. Rapid threat detection protects AI investments and maintains business continuity. You must implement automated monitoring and response capabilities to address AI-specific security incidents effectively. Here's how:

1. **Deploy automated AI risk detection across your environment.** AI workloads introduce dynamic threats that manual monitoring can't detect quickly enough to prevent damage. Automated systems provide real-time visibility into emerging risks and enable rapid response to security incidents. Use [AI security posture management](/azure/defender-for-cloud/ai-security-posture) in Microsoft Defender for Cloud to automate detection and remediation of generative AI risks across your Azure environment.

2. **Establish AI-focused incident response procedures.** Undetected security incidents can lead to data loss, model compromise, or service disruption that damages business operations. Specialized incident response procedures address the unique characteristics of AI security events. Build and test incident response plans that address AI-specific threats and continuously monitor for indicators of compromise in AI systems. Establish clear escalation procedures for different types of AI security incidents.

3. **Implement platform-specific monitoring strategies.** AI workloads deployed on different platforms face distinct security challenges that require tailored monitoring approaches. Platform-specific monitoring ensures comprehensive coverage of all potential attack vectors. Apply monitoring guidance based on your deployment architecture:

    - [AI monitoring on Azure platforms (PaaS)](./platform/management.md)
    - [AI monitoring on Azure infrastructure (IaaS)](./infrastructure/management.md)

## Azure resources

| Category | Tool | Description |
|----------|------|-------------|
| Asset Discovery | [Azure Resource Graph Explorer](/azure/governance/resource-graph/) | Discovers and inventories AI resources across Azure subscriptions |
| Security Monitoring | [Microsoft Defender for Cloud](/azure/defender-for-cloud/identify-ai-workload-model) | Identifies generative AI workloads and security risks |
| Identity Management | [Managed Identities](/azure/active-directory/managed-identities-azure-resources/) | Secures AI service authentication without storing credentials |
| Network Security | [Virtual Networks](/azure/ai-foundry/agents/how-to/virtual-networks) | Isolates AI communications and restricts network access |
| API Security | [Azure API Management](/azure/api-management/export-rest-mcp-server) | Secures Model Context Protocol server endpoints |
| Data Protection | [Azure Blob Storage](/azure/storage/blobs/) | Provides encrypted storage for AI artifacts with access controls |
| Data Governance | [Microsoft Purview](/purview/purview-security) | Catalogs and classifies AI data with sensitivity labels |

## Next steps

Govern AI, Manage AI, and Secure AI are continuous processes you must iterate through regularly. Revisit each AI Strategy, AI Plan, and AI Ready as needed. Use the AI adoption checklists to determine what your next step should be.

> [!div class="nextstepaction"]
> [AI checklists](index.md#ai-checklists)



---
File: /strategy.md
---

---
title: Create your strategy for AI adoption
description: Create your strategy for AI adoption
author: stephen-sumner
ms.author: ssumner
ms.date: 07/01/2025
ms.topic: conceptual
---

# Create your strategy for AI adoption

This article explains the process to prepare your organization for AI adoption. It describes how to select the right AI solutions, prepare your data, and ground your approach in responsible AI principles. A well-planned AI strategy aligns with your business objectives and ensures that AI projects contribute to overall success.

:::image type="complex" source="./images/ai-decision-tree.svg" alt-text="Diagram showing Microsoft and Azure services with decision points for each service." lightbox="./images/ai-decision-tree.svg" border="false":::
    Start by identifying your AI use case. If the goal is to enhance individual productivity, use Microsoft 365 Copilot when focusing on Microsoft 365 apps. Use in-product Copilots for products like Azure, GitHub, Fabric, Dynamics 365, or Power Platform. Use role-aligned Copilots for domain-specific roles such as security, sales, service, or finance. If the use case is more general, use Microsoft Copilot or Copilot Pro. If you already use Microsoft 365 Copilot and need to create custom agents with domain-specific skills, use Extensibility Tools for Microsoft 365 Copilot. If the goal is to automate business functionality, use Copilot Studio for a SaaS tool that enables agent creation and deployment through natural language with integrated pricing. Use Azure AI Foundry for a full development platform with API access to both Azure OpenAI and Azure AI services. If you only need access to OpenAI models, use Azure OpenAI. If you need prebuilt non-generative models or Azure AI Search for agent support, use Azure AI services. If you need to train and deploy machine learning models with your own data, use Microsoft Fabric if you already work in that environment; otherwise, use Azure Machine Learning. Use Azure Container Apps for lightweight AI inferencing without managing GPU infrastructure. If you need to bring your own models and orchestrate them with Azure CycleCloud, Azure Batch, or Kubernetes, use Azure Virtual Machines.
:::image-end:::

## Identify AI use cases

AI improves individual efficiency and enhances business processes. Generative AI increases productivity and improves customer experiences. Nongenerative AI, such as machine learning, analyzes structured data and automates repetitive tasks. Use this understanding to identify areas across your business where AI adds value.

1. **Identify automation opportunities.** Focus on processes suitable for automation to improve efficiency and reduce operational costs. Target repetitive tasks, data-heavy operations, or areas with high error rates where AI can have a significant impact.

2. **Gather customer feedback.** Use customer feedback to uncover use cases that improve customer satisfaction when automated with AI. This feedback helps prioritize impactful AI initiatives.

3. **Conduct an internal assessment.** Collect input from various departments to identify challenges and inefficiencies that AI can address. Document workflows and gather stakeholder input to uncover opportunities for automation, insight generation, or improved decision-making.

4. **Research industry use cases.** Investigate how similar organizations or industries use AI to solve problems or enhance operations. Use tools like the [AI architectures](/azure/architecture/ai-ml/) in the Azure Architecture Center for inspiration and to evaluate suitable approaches.

5. **Define AI targets.** For each identified use case, define the goal (general purpose), objective (desired outcome), and success metric (quantifiable measure). These benchmarks guide your AI adoption and measure success. For more information, see [example AI strategy](#example-ai-strategy).

## Define an AI technology strategy

Technology strategy determines the right approach for your organization's capabilities, data assets, and budget requirements. This strategy prepares your organization for agent-based architectures that enable multiple AI systems to collaborate on complex tasks. You must evaluate technology options across three service models to select the most suitable approach for your needs.

1. **Understand AI agents.** AI agents are autonomous systems that use AI models to complete tasks without constant human oversight. These systems represent a shift from traditional automation to intelligent decision-making that adapts to changing conditions. You must plan for agent integration to support [complex workflows](/azure/architecture/ai-ml/guide/ai-agent-design-patterns) and multi-system collaboration. Review [What are agents?](/azure/ai-foundry/agents/overview#what-is-an-ai-agent) to understand agent capabilities and prepare your organization for agent-based solutions.

2. **Adopt standard mechanisms for AI interoperability.** Standard protocols enable AI systems to communicate across different platforms and reduce custom implementations. These protocols support data sharing and system integration while maintaining flexibility for future technology changes. You should understand protocols like Model Context Protocol for cross-system data ingestion to ensure your AI systems support interoperability requirements. Evaluate tools like [NLWeb](https://github.com/microsoft/NLWeb?tab=readme-ov-file#what-is-nlweb) to prepare your content for the AI web. For example, see [Model Context Protocol in Microsoft Copilot Studio](/microsoft-copilot-studio/agent-extend-action-mcp#create-an-mcp-server) and [Exposing REST APIs as MCP servers](/azure/api-management/export-rest-mcp-server).

3. **Select the appropriate AI service model.** Microsoft offers three service models with varying levels of customization and [shared responsibility](/azure/security/fundamentals/shared-responsibility-ai): Software as a Service (SaaS), Platform as a Service (PaaS), and Infrastructure as a Service (IaaS). Each model requires different technical skills and provides different degrees of control over AI implementation. You must match your team's capabilities, data requirements, and customization needs with the appropriate service model. Use the AI decision tree to guide your selection process.

### Buy AI with software services (SaaS)

Microsoft provides SaaS generative AI solutions, known as Copilots, to enhance productivity with minimal technical expertise. Refer to the following table for details.

| Microsoft Copilots | Description | User | Data needed | Skills required | Main cost factors |
|---------------------|-------------|------|-------------|-----------------|-------------------|
| Microsoft 365 Copilot | [Microsoft 365 Copilot](/copilot/microsoft-365/microsoft-365-copilot-overview) provides web-based (internet) and work-based (Microsoft Graph) chat and in-app AI for Microsoft 365 apps. | Business | Yes. [Categorize your data](/security/zero-trust/copilots/zero-trust-microsoft-365-copilot#step-1-deploy-or-validate-your-data-protection) with sensitivity labels and securely interact with your data in Microsoft Graph. | General IT and data management | [License](https://www.microsoft.com/microsoft-365/microsoft-copilot#plans) |
| Role-based Copilots | Agents that enhance efficiency for specific roles in [Security](/copilot/security/microsoft-security-copilot), [Sales](https://www.microsoft.com/microsoft-365/copilot/copilot-for-sales), [Service](https://www.microsoft.com/microsoft-copilot/microsoft-copilot-for-service), and [Finance](https://www.microsoft.com/microsoft-copilot/microsoft-copilot-for-finance). | Business | Yes. Data-connection and plug-in options are available. | General IT and data management | Licenses or [Security Compute Units (Copilot for Security)](https://azure.microsoft.com/pricing/details/microsoft-security-copilot) |
| In-product Copilots | AI within products like [GitHub](https://azure.microsoft.com/products/github/copilot), [Power Apps](https://www.microsoft.com/power-platform/products/power-apps), [Power BI](https://www.microsoft.com/power-platform/products/power-bi?culture=en-us&country=us), [Dynamics 365](https://www.microsoft.com/dynamics-365/solutions/ai), [Power Automate](https://www.microsoft.com/power-platform/products/power-automate), [Microsoft Fabric](/fabric/fundamentals/copilot-fabric-overview), and [Azure](https://azure.microsoft.com/products/copilot/). | Business and individual | Yes. Most require minimal data preparation. | None | Free or subscription |
| Microsoft Copilot or Microsoft Copilot Pro | [Microsoft Copilot](https://copilot.microsoft.com/) is a free web-grounded chat application. [Copilot Pro](https://www.microsoft.com/store/b/copilotpro) provides better performance, capacity, and access to Copilot in certain Microsoft 365 apps. | Individual | No | None | [Microsoft Copilot](https://copilot.microsoft.com/) is free. Microsoft Copilot Pro requires a [subscription](https://www.microsoft.com/store/b/copilotpro?msockid=1e787d5f5c8d61da16f469995d146045) |

### Build AI agents with software services (SaaS)

Microsoft provides SaaS and low-code platforms to build AI agents. Refer to the following table for details.

| Microsoft Copilots | Description | User | Data needed | Skills required | Main cost factors |
|---------------------|-------------|------|-------------|-----------------|-------------------|
| Extensibility tools for Microsoft 365 Copilot | [Customize](/microsoft-365-copilot/extensibility/) Microsoft 365 Copilot with more data or capabilities via declarative agents. Use tools like [Copilot Studio](/microsoft-copilot-studio/microsoft-copilot-extend-copilot-extensions?context=%2Fmicrosoft-365-copilot%2Fextensibility%2Fcontext), [agent builder](/microsoft-365-copilot/extensibility/copilot-studio-agent-builder), [Teams toolkit](/microsoft-365-copilot/extensibility/build-declarative-agents), and [SharePoint](/microsoft-365-copilot/extensibility/build-declarative-agents). | Business and individual | Use [Microsoft Graph connectors](/microsoft-365-copilot/extensibility/overview-graph-connector) to add data. | Data management, general IT, or developer skills | [Microsoft 365 Copilot license](/microsoft-365-copilot/extensibility/faq#license-questions) |
| Copilot Studio | Use [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio) to build agents with low-code tools. | IT | Automates much of the data work to create custom copilots. | Platform to connect data sources, map prompts, and deploy copilots | [License](https://www.microsoft.com/microsoft-copilot/microsoft-copilot-studio#Pricing) |

### Build AI workloads with Azure platforms (PaaS)

Azure provides multiple PaaS options tailored to your AI goals, skill set, and data needs. These platforms cater to various levels of technical expertise. Review the [pricing pages](https://azure.microsoft.com/products/) for each Azure service, and use the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator) to develop cost estimates.

| AI goal | Microsoft solution | Data needed | Skills required | Main cost factors |
| --------------|----|-------------| ---------| ---- |
| Build agents | Azure AI Foundry [Agent Service](/azure/ai-services/agents/overview) | Yes | [Environment setup](/azure/ai-services/agents/environment-setup), model selection, [tooling](/azure/ai-services/agents/how-to/tools/overview), grounding data storage, data isolation, [agent triggering](/azure/ai-services/agents/how-to/triggers), [connect agents](/azure/ai-services/agents/how-to/connected-agents?pivots=portal), [content filtering](/azure/ai-services/openai/how-to/content-filters?context=%2Fazure%2Fai-services%2Fagents%2Fcontext%2Fcontext), [private networking](/azure/ai-services/agents/how-to/virtual-networks), [agent monitoring](/azure/ai-services/agents/concepts/tracing), [service monitoring](/azure/ai-services/agents/how-to/metrics) | Consuming model tokens, storage, features, compute, grounding connections |
| Build RAG applications | [Azure AI Foundry](/azure/ai-foundry/concepts/retrieval-augmented-generation) | Yes | [Select models](/azure/ai-foundry/concepts/foundry-models-overview), orchestrating dataflow, chunking data, enriching chunks, choosing indexing, understanding query types (full-text, vector, hybrid), understanding filters and facets, performing reranking, prompt engineering, deploying endpoints, and consuming endpoints in apps | Compute, number of tokens in and out, AI services consumed, storage, and data transfer |
| Fine-tune GenAI models | [Azure AI Foundry](/azure/ai-foundry/concepts/fine-tuning-overview) | Yes | Preprocessing data, splitting data into training and validation data, validating models, configuring other parameters, improving models, deploying models, and consuming endpoints in apps | Compute, number of tokens in and out, AI services consumed, storage, and data transfer |
| Train and inference models | [Azure Machine Learning](/azure/machine-learning/overview-what-is-azure-machine-learning) <br>or<br> [Microsoft Fabric](/fabric/get-started/microsoft-fabric-overview) | Yes | Preprocessing data, training models by using code or automation, improving models, deploying machine learning models, and consuming endpoints in apps | Compute, storage, and data transfer |
| Consume prebuilt AI models and services | [Azure AI services](/azure/ai-services/what-are-ai-services?context=%2Fazure%2Fai-foundry%2Fcontext%2Fcontext) and/or<br>[Azure OpenAI](/azure/ai-services/openai/overview)| Yes | Select AI models, securing endpoints, consuming endpoints in apps, and fine-tuning as needed | Use of model endpoints consumed, storage, data transfer, compute (if you train custom models) |
| Isolate AI apps | [Azure Container Apps](/azure/container-apps/gpu-serverless-overview) | Yes | Select AI models, orchestrating dataflow, chunking data, enriching chunks, choosing indexing, understanding query types (full-text, vector, hybrid), understanding filters and facets, performing reranking, prompt engineering, deploying endpoints, and consuming endpoints in apps | Compute, number of tokens in and out, AI services consumed, storage, and data transfer |

### Bring AI models with infrastructure services (IaaS)

For greater customization and control, use Azure's IaaS solutions such as [Azure Virtual Machines through CycleCloud](./infrastructure/cycle-cloud.md) and [Azure Kubernetes Service](/azure/aks/gpu-cluster). These solutions enable training and deployment of custom AI models. Refer to the relevant [pricing pages](https://azure.microsoft.com/products/) and the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator).

| AI goal | Microsoft solution | Data needed | Skills required | Main cost factors |
| --------------|----|-------------| ---------| ---- |
| Train and inference your own AI models. Bring your own models to Azure. | [Azure Virtual Machines](./infrastructure/cycle-cloud.md) <br>or<br>[Azure Kubernetes Service](/azure/aks/gpu-cluster) | Yes | Infrastructure management, IT, program installation, model training, model benchmarking, orchestration, deploying endpoints, securing endpoints, and consuming endpoints in apps | Compute, compute node orchestrator, managed disks (optional), storage services, Azure Bastion, and other Azure services used |

## Develop an AI data strategy

Data strategy defines how you collect, manage, and use data for AI initiatives. This strategy ensures data assets support your AI use cases while maintaining security and compliance. You must establish governance frameworks, assess scalability needs, design lifecycle management, and implement responsible data practices.

1. **Establish data governance frameworks for AI workloads.** Data governance provides secure and compliant AI data usage through access controls and responsible use policies. Governance frameworks define requirements for different AI use cases and establish ongoing data management processes. You must define data classification schemes based on sensitivity and exposure levels. Use data security and compliance protections for generative AI apps in [Microsoft Purview](/purview/ai-microsoft-purview).

2. **Assess scalability requirements for AI data needs.** Scalability assessment ensures your data infrastructure handles current and future AI workload demands without performance issues or cost overruns. This assessment identifies volume, velocity, and variety requirements that guide technology selection. You must document current data volumes, processing frequencies, and data types for each AI use case.

3. **Design data lifecycle management for AI assets.** Lifecycle management keeps data accessible, secure, and cost-effective from collection to disposal while supporting AI requirements. This approach addresses collection strategies, storage optimization, and quality assurance processes. You must plan systematic data collection from databases, APIs, IoT devices, and third-party providers. Design storage strategies with appropriate tiers based on access patterns and retention needs. Establish ETL/ELT pipelines for data quality and use the [Responsible AI Dashboard](https://github.com/microsoft/responsible-ai-toolbox#introducing-responsible-ai-dashboard) to identify and mitigate dataset bias.

4. **Implement responsible data practices for AI development.** Responsible practices ensure AI systems use data ethically and maintain regulatory compliance. These practices guide data collection, usage, and retention decisions throughout the AI lifecycle. You must implement data lineage tracking using [Microsoft Fabric](/fabric/governance/lineage) or [Microsoft Purview](/purview/concept-data-lineage) for transparency. Establish data quality standards, bias detection, and fairness considerations in training datasets. Define retention and disposal policies that balance AI performance with privacy and compliance requirements.

## Develop a responsible AI strategy

Responsible AI strategy ensures AI solutions remain trustworthy and ethical. This strategy establishes frameworks for ethical AI development that align with business objectives. You must establish accountability, define principles, select tools, and assess compliance to create a responsible AI strategy.

1. **Assign AI accountability to designated teams.** Accountability structures provide ownership for AI governance decisions and ensure responsive management of regulatory requirements. These structures define roles and decision-making authority for AI initiatives. You must assign individuals or teams to monitor AI technology changes and regulatory requirements. [Create an AI cloud center of excellence](./center-of-excellence.md) to centralize responsibilities and establish escalation procedures.

2. **Adopt responsible AI principles as business objectives.** Responsible AI principles provide the framework for ethical AI development that guides decision-making and aligns with industry standards. These principles become business objectives that shape AI project selection and development. You must adopt Microsoft's six [responsible AI principles](https://www.microsoft.com/ai/responsible-ai#advancing-aI-policy), which align with the [NIST AI Risk Management Framework (RMF)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf). Integrate these principles into project planning, development processes, and success metrics.

3. **Select responsible AI tools for your AI portfolio.** Tool selection ensures appropriate mechanisms for ethical AI principles and maintains consistent application of responsible AI standards. Tool selection addresses integration approaches and operational processes. You must assess and select appropriate Responsible AI [tools and processes](https://www.microsoft.com/ai/tools-practices#tabs-pill-bar-oc8dad_tab1) that align with your AI use cases and risk profiles. Integrate these tools within development workflows to ensure consistent application.

4. **Identify compliance requirements for AI regulations.** Compliance assessment protects the organization from legal risks and ensures AI initiatives align with applicable laws and industry standards. Compliance requirements vary by industry, geography, and AI application. You must identify relevant local and international AI regulations that apply to your operations and AI use cases. Monitor regulatory changes and update compliance strategies to ensure ongoing alignment throughout your AI adoption journey.

## Example AI strategy

This example AI strategy is based on a fictional company, Contoso. Contoso operates a customer-facing e-commerce platform and employs sales representatives who need tools to forecast business data. The company also manages product development and inventory for production. Its sales channels include both private companies and highly regulated public sector agencies.

| AI use case | Goals | Objectives | Success metrics | AI approach | Microsoft solution | Data needs | Skill needs | Cost factors | AI data strategy | Responsible AI strategy |
|---|---|---|---|---|---|---|---|---|---|---|
| **E-commerce web application chat feature** | Automate business process | Improve customer satisfaction | Increased customer retention rate | PaaS, generative AI, RAG | Azure AI Foundry | Item descriptions and pairings | RAG and cloud app development | Usage | Establish data governance for customer data and implement AI fairness controls. | Assign AI accountability to AI CoE and align with Responsible AI principles. |
| **Internal app document-processing workflow** | Automate business process | Reduce costs | Increased completion rate | Analytical AI, fine-tuning | Azure AI services - Document Intelligence | Standard documents | App development | Estimated usage | Define data governance for internal documents and plan data lifecycle policies. | Assign AI accountability and ensure compliance with data handling policies. |
| **Inventory management and product purchasing** | Automate business process | Reduce costs | Shorter shelf life of inventory | Machine learning, training models | Azure Machine Learning | Historical inventory and sales data | Machine learning and app development | Estimated usage | Establish governance for sales data and detect and address biases in data. | Assign AI accountability and comply with financial regulations. |
| **Daily work across company** | Enhance individual productivity | Improve employee experience | Increased employee satisfaction | SaaS generative AI | Microsoft 365 Copilot | OneDrive data | General IT | Subscription costs | Implement data governance for employee data and ensure data privacy. | Assign AI accountability and utilize built-in responsible AI features. |
| **E-commerce app for regulated industry chat feature** | Automate business process | Increase sales | Increased sales | IaaS generative AI model training | Azure Virtual Machines | Domain-specific training data | Cloud infrastructure and app development | Infrastructure and software | Define governance for regulated data and plan lifecycle with compliance measures. | Assign AI accountability and adhere to industry regulations. |

## Next step

> [!div class="nextstepaction"]
> [AI Plan](plan.md)



---
File: /toc.yml
---

items:
  - name: Overview AI adoption
    href: index.md
  - name: AI Strategy
    href: strategy.md
  - name: AI Plan
    href: plan.md
  - name: AI Ready
    items:
    - name: Prepare AI environment
      href: ready.md
    - name: AI on Azure platforms (PaaS)
      items:
      - name: AI architectures
        href: platform/architectures.md
      - name: Resource selection
        href: platform/resource-selection.md
      - name: Networking
        href: platform/networking.md
      - name: Governance
        href: platform/governance.md
      - name: Security
        href: platform/security.md
      - name: Management
        href: platform/management.md
    - name: AI on Azure infrastructure (IaaS)
      items:
      - name: Implementation options
        href: infrastructure/cycle-cloud.md
      - name: AI design areas
        items:
          - name: Compute
            href: infrastructure/compute.md
          - name: Storage
            href: infrastructure/storage.md
          - name: Networking
            href: infrastructure/networking.md
          - name: Governance
            href: infrastructure/governance.md
          - name: Management
            href: infrastructure/management.md
          - name: Security
            href: infrastructure/security.md
      - name: Well-architected
        href: infrastructure/well-architected.md
  - name: Govern AI
    href: govern.md
  - name: Secure AI
    href: secure.md
  - name: Manage AI 
    href: manage.md  
  - name: Additional resources
    items:
      - name: AI Center of Excellence
        href: center-of-excellence.md


