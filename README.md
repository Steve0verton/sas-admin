# SAS Administration Toolkit

Collection of Ansible orchestration playbooks for day to day SAS administration tasks including SAS program batch execution.  SAS Viya version 3.X is the intended platform **(not SAS Viya version 4.x)**.  SAS 9.X may be supported by certain Ansible playbooks within this repository but should be reconciled and assessed with discretion.  Playbooks for AWS cloud resource management are intended to be used for environment creation and management in a more efficient and standardized manner for cloud deployments.

**Disclaimer:** Ansible tasks attempt to be a universal as possible. Confirm environment references are supported by the target environment capabilities and security requirements. For example, Ansible changing user to ROOT or writing files to /tmp. Review, test and confirm Ansible playbook tasks in non-production environments before supporting production activities.

## Table of Contents

* [Project Directory Structure](#project-directory-structure)
* [Installation](#installation)
  * [Ansible](#ansible)
  * [AWS CLI Installation](#aws-cli-installation)
  * [AWS CLI Configuration](#aws-cli-configuration)
* [Usage](#usage)
* [Standards](#standards)
  * [File Properties](#file-properties)
  * [Header Properties](#header-properties)
  * [Coding Standards](#coding-standards)
* [Reference](#reference)
* [Author Contact](#author)


## Project Directory Structure

[admin](./admin):
 * Common administration tasks to manage SAS environments
 * Ansible playbooks and tasks written in YAML
 * Requires Linux operating system
 * Some tasks reference AWS cloud services and require playbook editing if AWS is not required
 * Requires configured AWS command line interface tool
 * Leverages SAS Viya deployment Ansible inventory file
 * Primary focus on SAS administration with some AWS cloud enablement that can be replaced

[aws](./aws):
 * Build and manage AWS resources for SAS deployments
 * Ansible playbooks and tasks written in YAML
 * Amazon Web Services dependent
 * Requires configured AWS command line interface tool
 * Primary focus on AWS cloud resource administration

[job_execution](./job_execution):
 * Execute SAS on local or remote machines for scheduled batch processing
 * Execute API calls on SAS Viya endpoints
 * Ansible playbooks and tasks written in YAML
 * Requires Linux operating system
 * Requires user provided SAS program to execute
 * Requires SAS Foundation
 * Assumes any SAS dependencies such as CAS or metadata aware connections are made within program or autoexec definition

[validation](./validation):
 * Tasks to validate SAS microservices
 * Ansible playbooks and tasks written in YAML
 * Requires configured AWS command line interface tool

## Installation

Clone or download the repository to an Ansible control node (also referred to as controller). For basic concepts of Ansible refer to [Ansible Documentation](https://docs.ansible.com/ansible/latest/network/getting_started/basic_concepts.html). It may be most efficient to clone the repository into a parent directory already organized for broader tasks.  In other words, many tasks within the repository were designed to be pieces of a broader set of playbooks and could potentially be customized to support a range of use cases and deployment types. **A qualified administrator should test and confirm all playbooks prior to running in a production environment.**

### Ansible

[SAS Support documentation](https://go.documentation.sas.com/?cdcId=calcdc&cdcVersion=3.5&docsetId=dplyml0phy0lax&docsetTarget=p1puupgtsay2r5n1h6k11n6lpl97.htm&locale=en#) provides steps to install Ansible.

Ansible playbooks within the repository were designed and developed following [SAS third party requirements for Ansible](https://support.sas.com/en/documentation/third-party-software-reference/viya/35/support-for-operating-systems.html).

### AWS CLI Installation

AWS CLI version 1 is required to execute playbooks within the **aws** directory. AWS CLI version 2 should also work but has not been tested. The following steps can be used to install the AWS CLI version 1 on a linux machine.

```shell
cd /tmp
curl -O https://bootstrap.pypa.io/get-pip.py
sudo python get-pip.py
sudo pip install awscli --upgrade
sudo pip install boto
sudo pip install boto3
```

For further instruction reference [AWS Documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html).

### AWS CLI Configuration

The AWS CLI must be configured on all target hosts and the control node running the playbook.  Many Ansible AWS modules require the AWS_ACCESS_KEY and AWS_SECRET_KEY set as an environment variable, which may be different from how the AWS configuration tool sets up the target environment. Amazon AMIs can be leveraged to standardize a base snapshot for target EC2 instances with tools such as the AWS CLI already installed and configured.

As an example, the following environment variables can be set using a file within **/etc/profile.d/**
```shell
export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
export AWS_DEFAULT_REGION=us-east-1
```

## Usage

Ansible playbooks and tasks should be carefully inspected, analyzed and tested before leveraging in a full production environment.  Playbooks are meant to provide a process to follow with configuration dependening on the target environment.  Broader playbooks and process flows can be constructed from the individual components.  Additional thoughts and suggestions are encouraged. Please leverage GitHub issue tracking to document.

## Standards

### File Properties

 - filenames must be lowercase using underscores
 - unix style line endings (LF)
 - UTF-8

### Header Properties

 - **Purpose:** very short description of the purpose and goal of the macro.
 - **Key Dependencies:** short description of key dependencies itemized in a list, including any YAML variables which need to be set.
 - **Notes:** general notes and important considerations for the overall playbook (if any).

Additional properties such as last modified timestamps, authorship and revision history are maintained within the git repository.

### Coding Standards

 - Indentation = 2 spaces with no tabs.
 - Empty line separating each Ansible task.
 - Tasks are named.
 - Boolean values for Ansible plays are specified as "yes" and "no".
 - Important variables are defined within play using **vars** list.
 - The phrase **NOTE:** is used to highlight important notes throughout code.
 - The phrase **TODO:** is used to note future enhancements.
 - Universal text to highlight replacement of text with environment-specific value: **REPLACEME**.

## Reference

 - [How Ansible Works](https://www.ansible.com/overview/how-ansible-works) - RedHat

## Author Contact

 - [Steve Overton](https://www.linkedin.com/in/overton/)
