# Core Jenkins Functions and Administration
---

## Jenkins Architecture
---
#### Jenkins Controller/Agent:

In Jenkins, the term “master/slave” has been replaced with **controller/agent**. The **controller** schedules and orchestrates work, while **agents** execute build tasks on worker nodes. The change reflects both modern terminology and clearer separation of duties and security boundaries.

#### Architecture

![Controller/Agent Architecture](/images/jenkins_architecture.png)

Key differences and roles
- **Controller (Master):**
  - Central node that manages configuration, job scheduling, queueing, and UI/API interactions.
  - Decides which agent runs a job based on labels, availability, and constraints.
  - Monitors agents and aggregates build results and artifacts.

- **Agent (Slave):**
  - Worker node (VM, bare metal, or container) that connects to the controller and runs builds/tests as directed.
  - Can be specialized by OS or tooling (e.g., Windows, Linux, macOS) and selected via labels for targeted workloads.
  - Typically requires Java and network connectivity to the controller; can connect via SSH, JNLP/Inbound, or cloud integrations.

**Why the shift in terminology and architecture emphasis?**
- Jenkins historically allowed agents broad access on the controller, which posed security risks in multi-team or partially trusted environments.
- Jenkins introduced an **Agent → Master (Controller) Access Control** subsystem to limit what agent-sent code can do on the controller, creating a safer boundary; admins can tune or disable it if all nodes are equally trusted.
- *Modern docs and community guidance use “controller/agent,” though many articles still reference “master/slave.”*

Common usage patterns
- **Scalability and parallelism:** Distribute jobs to multiple agents to run builds/tests in parallel, improving throughput for large projects.
- **Heterogeneous environments:** Use labeled agents for OS- or tool-specific tasks (e.g., Windows UI tests, Linux backend builds, macOS UI checks).
- **Resource isolation:** Keep heavy workloads off the controller; run builds on agents with dedicated resources or ephemeral cloud nodes.

Security considerations
- Treat the controller as a high-trust node; lock down plugins and credentials there.
- Use the Agent→Master access control to restrict agent-initiated operations on the controller unless all nodes are fully trusted.
- Keep agents updated and least-privileged; prefer ephemeral agents for untrusted or variable workloads.

In pipelines
- Assign where to run using the Pipeline’s **agent** directive or stage-level agents and **labels** to target specific worker nodes.