### What is Infrastructure as Code (IaC)?

Infrastructure as Code (IaC) is the practice of managing and provisioning IT infrastructure -such as servers, virtual machines, networks, and databases - using machine-readable definition files, rather than manual, physical configuration or interactive tools. 

Instead of a system administrator manually clicking through a console or physically setting up hardware, they write code that defines the desired state of the infrastructure. This code can then be used to automatically and consistently deploy and manage the environment.

### How it Works

The core idea is to automate the setup and management of infrastructure. This is typically done through a **declarative** or **imperative** approach:

- **Declarative:** You define the **desired end-state** of your infrastructure, and the IaC tool figures out the steps to get there. For example, you might declare, "I want two web servers and a database." The tool, like Terraform, will then handle the creation, configuration, and dependencies to achieve that state. This is often seen as the preferred method because it focuses on _what_ you want, not _how_ to get it.
- **Imperative:** You define the **specific steps or commands** needed to reach the desired state. This is like writing a script with a series of instructions: "First, create a virtual machine, then install the web server software, and finally, configure the network." This approach gives you more control over the process, but it can be more complex to manage.

### Key Benefits

IaC offers significant advantages for modern software development and operations.

- **Consistency and Reproducibility**: Manual configuration is prone to human error and "configuration drift," where environments become inconsistent. IaC ensures that the same environment can be recreated flawlessly every time, which is critical for moving code from development to testing and production.
- **Speed and Efficiency**: Automating infrastructure provisioning dramatically reduces the time it takes to set up new environments, whether for a new project, a testing environment, or scaling an application.
- **Version Control**: Because infrastructure is defined in code, you can use version control systems like Git. This allows for change tracking, collaboration, peer review, and the ability to easily roll back to a previous, stable configuration if an error occurs.
- **Cost Reduction**: IaC can help reduce costs by automating the provisioning of resources and preventing the over-provisioning of services. It also makes it easier to de-provision unused resources, so you only pay for what you need.

---
## Terraform Introduction

Terraform is a popular **Infrastructure as Code (IaC)** tool that helps us provision and manage cloud and on-premises resources. Created by HashiCorp, it uses a declarative approach, meaning you describe the **desired end-state** of your infrastructure, and Terraform figures out how to achieve it.

### How it Works

![[terraform_working.png]]

Terraform's core workflow is a cycle of writing, planning, and applying. It works by communicating with cloud providers' APIs through "providers," which are plugins that allow Terraform to manage resources on platforms like AWS, Google Cloud, and Azure.

The process you outlined is a perfect summary of this workflow:

- **Write your Terraform files**: We create configuration files using HashiCorp Configuration Language (HCL) to define the infrastructure you want to provision. For example, you might declare that you want to create a virtual machine, a network, and a database.
- **Run Terraform commands**: We interact with our configuration files using a command-line interface. The key phases are:
    - `terraform init`: Initializes a working directory containing Terraform configuration files. This command downloads the necessary provider plugins and modules.
    - `terraform validate`: Checks the configuration files for syntax errors and internal consistency.
    - `terraform plan`: Creates an execution plan. Terraform compares the configuration with the current state of the infrastructure (stored in a `terraform.tfstate` file) and shows exactly what it will create, update, or destroy to match your desired state. It's a "dry run" that lets us review changes before they are applied. * `terraform apply`: Executes the actions in the plan. This is where Terraform calls the target cloud provider's API to provision and manage the infrastructure. It also updates the state file to reflect the new state of the resources.
    - `terraform destroy`: This command is used to tear down all the resources managed by the current configuration. Terraform will generate a destruction plan and, upon approval, will delete the infrastructure.

Terraform's declarative nature and state management capabilities make it an incredibly powerful tool for ensuring that your infrastructure is consistent, reproducible, and easily managed.

---

Install Terraform on Arch:

```zsh
sudo pacman -S terraform
```

Version during the preparation: `1.13.1`