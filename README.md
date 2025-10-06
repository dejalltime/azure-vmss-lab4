# Lab 4 – Understanding Virtual Machine Scale Sets (VMSS) in Azure

## Overview

In this lab, we’ll explore **Azure Virtual Machine Scale Sets (VMSS)** — the Azure equivalent of AWS Auto Scaling Groups (ASG).  
You’ll learn how to **automatically scale virtual machines** based on performance metrics such as CPU usage, while maintaining high availability and fault tolerance.

By the end of this lab, you’ll understand how to:

- Create and configure a **VM Scale Set** using the Azure Portal (or CLI).
- Deploy a sample web app across multiple VM instances.
- Set up **manual** and **automatic scaling rules**.
- Observe how Azure automatically **scales out** and **scales in** your instances based on load.

---

## ⚙️ Technologies Used

- **Azure Virtual Machine Scale Sets (VMSS)**
- **Azure Virtual Network (VNet)**
- **Azure Load Balancer**
- **Azure Monitor / Autoscale Settings**
- **Azure Portal / CLI**

---

## Learning Objectives

1. Understand how Virtual Machine Scale Sets (VMSS) simplify the deployment and management of multiple identical VMs.
2. Learn how to configure a **custom image** or **standard image** for scale set instances.
3. Implement **autoscaling rules** based on metrics (e.g., CPU utilization).
4. Verify scale-in and scale-out behavior dynamically.

---

## Architecture Diagram

The diagram below illustrates a simple deployment of a **Virtual Machine Scale Set** behind a Load Balancer.  
Traffic is distributed evenly, and autoscale rules adjust the number of instances based on demand.

```
                   ┌────────────────────────┐
                   │     Azure Load Balancer│
                   └─────────────┬──────────┘
                                 │
          ┌──────────────────────┼──────────────────────┐
          │                      │                      │
   ┌──────────────┐       ┌──────────────┐       ┌──────────────┐
   │ VM Instance 1│       │ VM Instance 2│  ...  │ VM Instance N│
   └──────────────┘       └──────────────┘       └──────────────┘
          │                      │                      │
          └──────────────────────┴──────────────────────┘
                      Virtual Machine Scale Set
```

---

## Lab Tasks

### **Task 1 – Introduction**

Get familiar with the lab objectives and the concept of VM Scale Sets in Azure.

---

### **Task 2 – Create Virtual Machine and Custom Image**

1. Launch a standard **Virtual Machine** (e.g., Ubuntu 22.04 LTS).
2. Install and start a **Node.js web server** that displays the instance’s private IP address.
3. Capture a **custom image** from this VM to be used by the Scale Set.

---

### **Task 3 – Create and Configure the Virtual Machine Scale Set**

1. Create a new **VM Scale Set** using the custom image or a standard marketplace image.
2. Attach it to an existing or new **Virtual Network** and **Load Balancer**.
3. Configure:
   - Initial instance count (e.g., 2)
   - Instance size (e.g., Standard_B1s)
   - Scaling policy (manual or automatic)

---

### **Task 4 – Define Autoscale Rules**

1. Open **Azure Monitor → Autoscale Settings** for your VM Scale Set.
2. Add rules such as:
   - **Scale Out**: Add 1 instance if average CPU > 70% for 5 minutes.
   - **Scale In**: Remove 1 instance if average CPU < 30% for 5 minutes.
3. Save and apply the configuration.

---

### **Task 5 – Test Scaling Behavior**

1. Use a **load testing tool** (e.g., Apache Benchmark or `hey`) to simulate high CPU load on the instances.
2. Monitor scaling activity under:
   - **Azure Portal → VMSS → Instances**
   - **Azure Monitor → Autoscale logs**
3. Observe automatic scale-out when CPU increases and scale-in when idle.

---

### **Task 6 – Clean Up**

To avoid unnecessary costs, delete:

- The **Scale Set**
- The **Load Balancer**
- Any associated **resource groups** or **storage resources**

---

## Summary

In this lab, you learned how to:

- Create and configure Azure Virtual Machine Scale Sets (VMSS)
- Define scaling rules using Azure Monitor metrics
- Observe automatic scaling in action

This approach ensures that your application can handle changing workloads efficiently — **scaling automatically without manual intervention.**
