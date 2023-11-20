# Terraform Beginner Bootcamp 2023

- [Terraform Beginner Bootcamp 2023](#terraform-beginner-bootcamp-2023)
  - [Semantic Versioning :mage:](#semantic-versioning-mage)
  - [Install the Terraform CLI](#install-the-terraform-cli)
    - [Considerations with the Terraform CLI changes](#considerations-with-the-terraform-cli-changes)
    - [Refactoring into Bash Scripts](#refactoring-into-bash-scripts)
    - [Considerations for Linux Distribution](#considerations-for-linux-distribution)
      - [Shebang Considerations](#shebang-considerations)
      - [Execution Considerations](#execution-considerations)
      - [Linux Permissions Considerations](#linux-permissions-considerations)
    - [Github Lifecycle (Before, Init, Command)](#github-lifecycle-before-init-command)

## Semantic Versioning :mage:

This project is going to utilise semantic tagging for its versioning. [semver.org](https://semver.org/)

The general format:

**MAJOR.MINOR.PATCH**, e.g. `1.0.1`

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes

## Install the Terraform CLI

### Considerations with the Terraform CLI changes

The previous instructions in the `.gitpod.yml` file had deprecated instructions which caused keyring issues. Referred to the Terraform installation instructions and updated accordingly.

[Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

### Refactoring into Bash Scripts

While fixing the Terraform CLI gpg depreciation issues we notice that bash scripts steps were a considerable amount more code. So we decided to create a bash script to install the Terraform CLI.

The updated instructions were more detailed. To simplify this and reduce the amount of code in `gitpod.yml` the steps were placed in a bash script file and referenced via the `gitpod.yml` file.

The bash script is located here: [`./bin/install_terraform_cli`](/bin/install_terraform_cli)

- This will keep the Gitpod Task File ([.gitpod.yml](.gitpod.yml)) tidy.
- This allow us an easier to debug and execute manually Terraform CLI install
- This will allow better portablity for other projects that need to install Terraform CLI.



### Considerations for Linux Distribution

This project is built against Ubunutu.
Please consider checking your Linux Distrubtion and change accordingly to distrubtion needs. 

[How To Check OS Version in Linux](
https://www.cyberciti.biz/faq/how-to-check-os-version-in-linux-command-line/)

Example of checking OS Version:

```sh
$ cat /etc/os-release
PRETTY_NAME="Ubuntu 22.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```
#### Shebang Considerations

A Shebang (prounced Sha-bang) tells the bash script what program that will interpet the script. eg. `#!/bin/bash`

ChatGPT recommended this format for bash: `#!/usr/bin/env bash`

- For portability for different OS distributions 
- Will search the user's PATH for the bash executable

(Shebang)[https://en.wikipedia.org/wiki/Shebang_(Unix)]

#### Execution Considerations

When executing the bash script we can use the `./` shorthand notiation to execute the bash script.

eg. `./bin/install_terraform_cli`

If we are using a script in `.gitpod.yml` we need to point the script to a program to interpret it.

eg. `source ./bin/install_terraform_cli`

#### Linux Permissions Considerations

In order to make our bash scripts executable we need to change linux permission for the fix to be executable at the user mode.

```sh
chmod u+x /bin/install_terraform_cli
```

alternatively:

```sh
chmod 744 /bin/install_terraform_cli
```

(CHMOD) [https://en.wikipedia.org/wiki/Chmod]

### Github Lifecycle (Before, Init, Command)

We need to be careful when using the Init because it will not rerun if we restart an existing workspace.

[Gitpod Tasks](https://www.gitpod.io/docs/configure/workspaces/tasks)
