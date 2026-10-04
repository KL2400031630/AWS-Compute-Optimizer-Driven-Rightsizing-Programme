# ☁️ AWS Compute Optimizer Driven Rightsizing Programme

> **Turning cloud usage data into smarter infrastructure decisions.**

An AWS cloud cost-optimization project that demonstrates how **Amazon EC2**, **Amazon CloudWatch**, and **AWS Compute Optimizer** can be used together to identify underutilized resources and support **data-driven rightsizing decisions**.

---

## 👥 Team

| Name | Role |
|---|---|
| **Prem Prakash** | Team Member |
| **Tentu Divya Amrutha** | Team Member |
| **Chimakurthi Lakshmi Janani** | Team Member |
| **Samarth V Ratnam** | Team Member |

---

# 🎯 Project Overview

Cloud infrastructure is often provisioned with more capacity than an application actually requires.

While over-provisioning can provide a safety margin for performance, it can also result in:

- 💸 Unnecessary cloud expenditure
- 🖥️ Underutilized compute resources
- 📉 Poor resource efficiency
- 🔍 Difficulty identifying optimization opportunities
- 🔄 Continuous resource-management overhead

This project explores a **rightsizing-driven cloud optimization workflow** using AWS-native services.

The solution monitors EC2 workload behavior through **Amazon CloudWatch**, uses **AWS Compute Optimizer** to analyze resource utilization, and uses those insights to support better infrastructure sizing decisions.

---

# 💡 Core Idea

The project follows a simple continuous optimization loop:

```text
                ┌────────────────────┐
                │     AWS Resource   │
                │        EC2         │
                └─────────┬──────────┘
                          │
                          ▼
                ┌────────────────────┐
                │   Amazon CloudWatch│
                │  Usage & Metrics   │
                └─────────┬──────────┘
                          │
                          ▼
                ┌────────────────────┐
                │ AWS Compute        │
                │ Optimizer          │
                └─────────┬──────────┘
                          │
                          ▼
                ┌────────────────────┐
                │ Optimization       │
                │ Recommendation     │
                └─────────┬──────────┘
                          │
                          ▼
                ┌────────────────────┐
                │ Cost & Performance │
                │ Evaluation         │
                └─────────┬──────────┘
                          │
                          ▼
                    Rightsizing
                          │
                          ▼
                  Monitor Again
                          │
                          └───────────────► 🔄
```

The objective is not simply to reduce cost.

The objective is:

> **Reduce unnecessary resource capacity while maintaining acceptable workload performance.**

---

# 🧩 Problem Statement

Organizations running workloads in the cloud can easily accumulate over-provisioned resources.

For example:

```text
Allocated Capacity
████████████████████████████████████

Actual Workload
███
```

If a resource consistently operates far below its allocated capacity, there may be an opportunity to move to a more appropriate resource configuration.

However, manually analyzing every resource is difficult at scale.

A better approach is to:

```text
Monitor → Analyze → Recommend → Evaluate → Optimize → Monitor
```

This project demonstrates that approach using AWS-native services.

---

# 🏗️ Architecture

```text
                         AWS ACCOUNT
                              │
                              ▼
                    ┌──────────────────┐
                    │   Amazon EC2     │
                    │                  │
                    │  t3.micro        │
                    │  Demo Workload   │
                    └────────┬─────────┘
                             │
                             │ Metrics
                             ▼
                    ┌──────────────────┐
                    │ Amazon CloudWatch│
                    │                  │
                    │ CPU Utilization  │
                    │ Network In       │
                    │ Network Out      │
                    └────────┬─────────┘
                             │
                             │ Workload History
                             ▼
                    ┌──────────────────┐
                    │ AWS Compute      │
                    │ Optimizer        │
                    │                  │
                    │ Recommendations  │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Cost & Performance│
                    │ Evaluation       │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │   Rightsizing    │
                    │    Decision      │
                    └────────┬─────────┘
                             │
                             ▼
                       Monitor Again
```

---

# ☁️ AWS Services

## Amazon EC2

Amazon EC2 provides the compute resource used for the practical demonstration.

### Demonstration configuration

| Property | Value |
|---|---|
| Service | Amazon EC2 |
| Instance Type | `t3.micro` |
| Region | `us-east-1` |
| Availability Zone | `us-east-1c` |
| Operating System | Amazon Linux 2023 |
| Purpose | Rightsizing Demonstration |

---

## 📊 Amazon CloudWatch

Amazon CloudWatch was used to observe the behavior of the EC2 instance.

The monitoring workflow focused on metrics including:

```text
CPUUtilization
NetworkIn
NetworkOut
```

These metrics provide visibility into how heavily the instance is being utilized.

Example:

```text
EC2
 │
 ├── CPUUtilization
 │
 ├── NetworkIn
 │
 └── NetworkOut
```

CloudWatch therefore acts as the **measurement layer** of the rightsizing workflow.

---

# 🤖 AWS Compute Optimizer

AWS Compute Optimizer provides recommendations based on resource utilization and workload behavior.

The intended workflow is:

```text
EC2 Workload
     │
     ▼
CloudWatch Metrics
     │
     ▼
Compute Optimizer
     │
     ▼
Optimization Recommendation
     │
     ├── Current Configuration
     ├── Recommended Configuration
     ├── Performance Considerations
     └── Potential Savings
```

The recommendation should then be evaluated before making any production change.

---

# 🔬 Practical Implementation

The project was implemented as a controlled AWS demonstration.

## 1. EC2 Instance

A `t3.micro` EC2 instance was launched in:

```text
Region: us-east-1
Availability Zone: us-east-1c
```

The instance was given a meaningful project tag:

```text
Name = rightsizing-demo-ec2
```

---

## 2. CloudWatch Monitoring

CloudWatch metrics were inspected for the running EC2 instance.

The following metrics were observed:

```text
CPUUtilization
NetworkIn
NetworkOut
```

The monitoring window provided an initial view of the workload's resource consumption.

---

## 3. Compute Optimizer

The EC2 resource was then made available for analysis through AWS Compute Optimizer.

Compute Optimizer may require sufficient workload history before producing a recommendation.

During the initial demonstration, the dashboard displayed:

```text
Data not available
```

This is expected when insufficient historical utilization data is available.

Therefore, the project does **not** claim a specific Compute Optimizer recommendation where one had not yet been generated.

---

# 📈 Observations

During the CloudWatch observation period, the demonstration EC2 instance showed very low CPU utilization.

The observed CPU utilization was approximately:

```text
0.07% – 0.17%
```

This indicates that the demonstration workload was lightly utilized during the observed period.

Network activity was also captured through:

```text
NetworkIn
NetworkOut
```

These metrics demonstrate how actual workload behavior can be used as evidence when evaluating resource allocation.

---

# 🧠 Why Rightsizing?

Consider a hypothetical resource:

```text
Provisioned Capacity
████████████████████████████████████

Actual Utilization
██
```

The gap between provisioned capacity and actual workload may represent an optimization opportunity.

Rightsizing attempts to move toward:

```text
Provisioned Capacity
████████

Actual Utilization
██████
```

while still maintaining an appropriate performance margin.

---

# 💰 Cost Optimization Strategy

The project treats cost optimization as a balance between:

```text
              COST
                │
                ▼
       ┌────────────────┐
       │  Rightsizing   │
       └───────┬────────┘
               │
       ┌───────┴────────┐
       ▼                ▼
  Lower Cost       Performance
                       Safety
```

A resource should not simply be downsized because its CPU usage is low.

The decision should consider:

- CPU utilization
- Memory requirements
- Network workload
- Application behavior
- Workload variability
- Performance requirements
- Potential cost savings

---

# 🔄 Continuous Rightsizing Lifecycle

The proposed long-term workflow is:

```text
┌──────────────┐
│   Deploy     │
└──────┬───────┘
       ▼
┌──────────────┐
│    Monitor   │
└──────┬───────┘
       ▼
┌──────────────┐
│    Analyze   │
└──────┬───────┘
       ▼
┌──────────────┐
│  Recommend   │
└──────┬───────┘
       ▼
┌──────────────┐
│    Evaluate  │
└──────┬───────┘
       ▼
┌──────────────┐
│   Rightsize  │
└──────┬───────┘
       ▼
┌──────────────┐
│ Monitor Again│
└──────┬───────┘
       │
       └──────────────► 🔄
```

This transforms rightsizing from a one-time activity into a continuous optimization process.

---

# 🔐 Security Considerations

Cloud optimization should always be performed without compromising security.

The demonstration environment considered:

- IAM-based access control
- Restricted administrative access
- Controlled SSH access
- Resource tagging
- Avoidance of unnecessary public exposure
- Controlled test resources

For production environments, rightsizing actions should be reviewed and approved before being applied.

---

# 🏷️ Resource Tagging

The EC2 instance was tagged to make it easier to identify within the AWS environment.

Example:

```text
Name        → rightsizing-demo-ec2
Environment → Demo
Project     → AWS-Rightsizing
Purpose     → Compute-Optimizer
```

Meaningful tagging is particularly important when managing large cloud environments.

---

# 📊 Evaluation Framework

A rightsizing decision can be evaluated using the following dimensions:

| Dimension | Question |
|---|---|
| CPU | Is the allocated CPU capacity being used? |
| Memory | Is memory capacity appropriate for the workload? |
| Network | Does the workload require the current network capacity? |
| Cost | Can the resource configuration be made cheaper? |
| Performance | Will rightsizing negatively affect the application? |
| Stability | Does workload demand fluctuate significantly? |

The final decision should therefore be:

```text
             Utilization
                  +
            Cost Analysis
                  +
         Performance Risk
                  +
          Workload Pattern
                  │
                  ▼
          RIGHTSIZING DECISION
```

---

# ⚠️ Current Limitations

The current demonstration has several limitations.

### Limited Workload History

AWS Compute Optimizer requires sufficient historical workload data to produce meaningful recommendations.

### Controlled Workload

The EC2 instance was used as a demonstration environment rather than a production workload.

### Recommendation Availability

A Compute Optimizer recommendation was not immediately available during the initial observation period.

### No Automatic Production Changes

The demonstration does not automatically modify production infrastructure.

This is intentional because rightsizing changes should be evaluated before deployment.

---

# 🚀 Future Scope

The project can be expanded significantly.

## 1. Automated Recommendation Collection

Automatically retrieve Compute Optimizer recommendations using AWS APIs.

```text
Compute Optimizer
       ↓
     API
       ↓
Recommendation Engine
```

---

## 2. Automated Cost Analysis

Integrate AWS cost information to calculate:

```text
Current Cost
      -
Optimized Cost
      =
Potential Savings
```

---

## 3. Approval Workflow

Introduce human approval before applying optimization recommendations.

```text
Recommendation
      ↓
Cost Analysis
      ↓
Performance Risk
      ↓
Human Approval
      ↓
Rightsizing
```

---

## 4. Automated Rightsizing

Approved recommendations could eventually be applied through AWS automation.

```text
Compute Optimizer
        ↓
Recommendation
        ↓
Approval
        ↓
Automation
        ↓
EC2 Modification
        ↓
CloudWatch Monitoring
```

---

## 5. Multi-Resource Optimization

The solution can be expanded to analyze additional AWS resources supported by Compute Optimizer.

---

## 6. Dashboard

A future version could provide a centralized dashboard displaying:

```text
┌─────────────────────────────────────┐
│       CLOUD OPTIMIZATION            │
├─────────────────────────────────────┤
│ Resources Analyzed       100         │
│ Optimization Candidates   24         │
│ Potential Savings       $XXX         │
│ Performance Risk          Low        │
│ Recommendations           18         │
└─────────────────────────────────────┘
```

---

# 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| **Amazon EC2** | Compute workload |
| **Amazon CloudWatch** | Monitoring and metrics |
| **AWS Compute Optimizer** | Rightsizing recommendations |
| **AWS IAM** | Access control |
| **GitHub** | Source/documentation management |
| **Microsoft PowerPoint** | Project presentations |
| **Microsoft Word** | Project report |

---

# 📁 Repository Structure

```text
Aws-Hackathon/
│
├── README.md
│
├── AWS-HACKATHON-Review-1.pptx
├── AWS-HACKATHON-Review-2.pptx
├── AWS-HACKATHON-Review-3.pptx
│
├── FINAL REPORT - AWS_Rightsizing_Report.docx.pdf
│
└── screenshots/
    ├── ec2/
    ├── cloudwatch/
    └── compute-optimizer/
```

> The repository is primarily a **project documentation and AWS demonstration repository** rather than a traditional application source-code repository.

---

# 📸 Project Evidence

The project documentation contains evidence covering:

- AWS EC2 configuration
- Resource tagging
- CloudWatch metrics
- CPU utilization
- Network utilization
- Compute Optimizer dashboard
- Rightsizing workflow
- Project architecture
- Cost optimization strategy

Screenshots are included to document the practical AWS implementation.

---

# 🧪 Demonstration Flow

The complete demonstration can be summarized as:

```text
STEP 01
Create EC2 Instance
        │
        ▼
STEP 02
Configure & Tag Resource
        │
        ▼
STEP 03
Monitor Using CloudWatch
        │
        ▼
STEP 04
Observe CPU & Network Metrics
        │
        ▼
STEP 05
Enable / Review Compute Optimizer
        │
        ▼
STEP 06
Allow Workload History Collection
        │
        ▼
STEP 07
Review Recommendation
        │
        ▼
STEP 08
Evaluate Cost vs Performance
        │
        ▼
STEP 09
Apply Rightsizing When Appropriate
        │
        ▼
STEP 10
Monitor Again
```

---

# 📚 Key Concepts Demonstrated

This project demonstrates practical understanding of:

- ☁️ Cloud Computing
- 💰 Cloud Cost Optimization
- 🖥️ Amazon EC2
- 📊 Amazon CloudWatch
- 🤖 AWS Compute Optimizer
- 🔐 AWS IAM
- 📈 Resource Utilization
- ⚙️ Infrastructure Optimization
- 📉 Rightsizing
- 🔄 Continuous Optimization
- 🛡️ Performance-Aware Cost Reduction

---

# 🎓 Academic Context

This project was developed as an **AWS Cloud Computing Hackathon project** with a focus on:

> **Cloud resource optimization through workload monitoring and intelligent rightsizing.**

The project combines theoretical cloud-cost optimization concepts with a practical AWS implementation.

---

# 🏁 Conclusion

Cloud optimization is not simply about choosing the cheapest resource.

It is about choosing the **right resource for the workload**.

This project demonstrates an AWS-native approach where:

```text
        REAL WORKLOAD
              │
              ▼
      ┌──────────────┐
      │ CloudWatch   │
      │   Metrics    │
      └──────┬───────┘
             │
             ▼
      ┌──────────────┐
      │   Compute    │
      │   Optimizer  │
      └──────┬───────┘
             │
             ▼
      ┌──────────────┐
      │ Optimization │
      │ Recommendation│
      └──────┬───────┘
             │
             ▼
      ┌──────────────┐
      │ Cost +       │
      │ Performance  │
      └──────┬───────┘
             │
             ▼
         RIGHTSIZE
             │
             ▼
       MONITOR AGAIN
             │
             └──────────► 🔄
```

The ultimate goal is to create a cloud environment that is:

**Efficient.  
Cost-conscious.  
Performance-aware.  
Continuously optimized.**

---

# 👥 Team

### Prem Prakash

### Tentu Divya Amrutha

### Chimakurthi Lakshmi Janani

### Samarth V Ratnam

---

# 🔗 Repository

**GitHub:**  
https://github.com/samarthratnam/Aws-Hackathon

---

## ⭐ If you found this project useful

Give the repository a ⭐ and feel free to explore the project documentation and AWS implementation.

---

> **Built with AWS ☁️ | Optimized with Data 📊 | Designed for Efficiency ⚡**
