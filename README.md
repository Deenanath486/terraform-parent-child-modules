# Terraform Parent-Child Modules

A comprehensive example demonstrating best practices for organizing and using parent and child modules in Terraform for infrastructure as code.

## 📋 Overview

This repository showcases how to structure Terraform configurations using a modular approach with parent and child modules. This pattern promotes code reusability, maintainability, and follows Terraform best practices.

## 🎯 Features

- **Modular Architecture**: Clean separation of concerns with parent and child modules
- **Reusable Components**: Child modules can be used across multiple parent configurations
- **Best Practices**: Follows Terraform and HashiCorp conventions
- **Scalability**: Easy to extend and maintain as infrastructure grows
- **Examples**: Practical examples of common infrastructure patterns

## 📁 Project Structure

```
.
├── modules/
│   ├── child-module-1/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── child-module-2/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── ...
├── environments/
│   ├── dev/
│   │   └── main.tf
│   ├── staging/
│   │   └── main.tf
│   └── prod/
│       └── main.tf
├── main.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
└── README.md
```

## 🚀 Quick Start

### Prerequisites

- [Terraform](https://www.terraform.io/downloads.html) (v1.0 or higher recommended)
- [AWS CLI](https://aws.amazon.com/cli/) (if using AWS)
- Appropriate cloud provider credentials

### Installation

1. Clone the repository:
```bash
git clone https://github.com/Deenanath486/terraform-parent-child-modules.git
cd terraform-parent-child-modules
```

2. Initialize Terraform:
```bash
terraform init
```

3. Review the plan:
```bash
terraform plan
```

4. Apply the configuration:
```bash
terraform apply
```

## 📖 Usage Guide

### Parent Module

The parent module serves as the main orchestrator that:
- Calls child modules
- Provides variables to child modules
- Passes outputs between modules
- Manages the overall infrastructure

Example:
```hcl
module "child" {
  source = "./modules/child-module-1"
  
  variable1 = var.input_variable
  variable2 = var.another_variable
}

output "child_output" {
  value = module.child.output_value
}
```

### Child Modules

Child modules are self-contained units that:
- Handle specific infrastructure components
- Define their own variables and outputs
- Are reusable across different parent modules
- Maintain independence and single responsibility

Example structure:
```hcl
# variables.tf
variable "instance_type" {
  type = string
  description = "EC2 instance type"
}

# main.tf
resource "aws_instance" "example" {
  instance_type = var.instance_type
}

# outputs.tf
output "instance_id" {
  value = aws_instance.example.id
}
```

## 🔧 Configuration

### Variables

Modify `terraform.tfvars` or use command-line variables:
```bash
terraform apply -var="environment=dev" -var="region=us-east-1"
```

### Environments

Different configurations for different environments:
- **dev**: Development environment
- **staging**: Staging environment
- **prod**: Production environment

## 📚 Best Practices

1. **Naming Conventions**: Use clear, consistent naming for modules and resources
2. **Variable Validation**: Implement input validation in child modules
3. **Documentation**: Document all variables, outputs, and module purposes
4. **State Management**: Use remote state for team environments
5. **Module Versioning**: Tag modules in source control for version control
6. **DRY Principle**: Avoid code duplication by using modules effectively

## 🔗 Outputs

The parent module exposes important outputs for downstream use:
```hcl
output "resource_ids" {
  value       = module.child.resource_id
  description = "Resource IDs from child modules"
}
```

## 🛠️ Maintenance

### Updating Modules

To update module versions:
```bash
terraform get -update
```

### Destroying Infrastructure

```bash
terraform destroy
```

## 📝 Module Documentation

Each child module includes:
- `README.md` - Module-specific documentation
- `variables.tf` - Input variable definitions
- `outputs.tf` - Output value definitions
- `main.tf` - Resource definitions

## 🤝 Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 📞 Support

For questions or issues:
- Open an GitHub issue
- Check existing documentation
- Review Terraform [official documentation](https://www.terraform.io/docs)

## 🔗 Resources

- [Terraform Modules](https://www.terraform.io/docs/modules)
- [Best Practices](https://www.terraform.io/docs/cloud/recommended-practices)
- [Module Registry](https://registry.terraform.io/)

---

**Happy Terraforming! 🚀**
