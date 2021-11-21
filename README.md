# Ansible Role: Tessera

## Description

This repo contains an Ansible playbook to deploy [Tessera](https://github.com/ConsenSys/tessera) on a bare-metal server.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Role Variables](#role-variables)
  - [Recommended Required Role Variables](#Recommended-Required-Role-Variables)
  - [Full List of Role Variables](#Full-List-of-Role-Variables)
- [Example Usage](#example-usage)
- [Licence](#licence)
- [Author Information](#author-information)

## Prerequisites

1. Java JDK 11+
2. Build tools for building libsodium

## Role Variables

Variables are defined in `defaults/main.yml` and can be directly overriden by editing the file, passing in command-line parameters, or vars in a playbook. The majority of the variables are options pertaining to the configuration file for Tessera, which can be found in its [docs](https://docs.tessera.consensys.net/en/stable/Reference/SampleConfiguration/).

### Recommended Required Role Variables

The below table lists the recommended role variables that should be used. Please see the [second](#Full-List-of-Role-Variables) table if you would like to see the entire list of variables that can be modified.

| Name              | Default                      | Required?                                                                                                               |
| ----------------- | ---------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| tessera_version   | unset                        | Yes                                                                                                                     |
| run_with_besu     | false                        | Yes, if running with Besu. Leave unset or false if using with GoQuorum.                                                 |
| server_configs    | unset                        | Yes. However, if left unset, default config will be used suitable for dev environment. Check `templates/config.json.j2` |
| peers             | unset                        | Yes. However, if left unset, default will be itself. Check `templates/config.json.j2`                                   |
| public_key        | unset                        | Public key.                                                                                                             |
| config_details    | unset                        | Configuration details for the protected or unprotected inline key pairs.                                                |
| jdbc_url          | Set to tessera_config_dir/db | Yes. Default will set to tessera_config_dir/db as a local file.                                                         |
| jdbc_username     | "sa"                         | Yes. Make sure to change.                                                                                               |
| jdbc_password     | ""                           | Yes. Make sure to change.                                                                                               |
| default_log_level | INFO                         | No. Can be set to 'DEBUG' if necessary.                                                                                 |

### Full List of Role Variables

| Name                             | Default                                    | Description                                                                                                                                                                                                                                        |
| -------------------------------- | ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| tessera_version                  | unset                                      | Version of Tessera to install. Must be set for the role to run.                                                                                                                                                                                    |
| tessera_user                     | tessera                                    | The user that will be created on the system for Tessera to run on.                                                                                                                                                                                 |
| tessera_group                    | tessera                                    | Group that the user will be long to.                                                                                                                                                                                                               |
| tessera_download_url             | Predefined                                 | URL to Tessera tar.                                                                                                                                                                                                                                |
| enclave_download_url             | Predefined                                 | URL to Enclave tar.                                                                                                                                                                                                                                |
| azure_key_vault_download_url     | Predefined                                 | URL to Azure Key Vault tar.                                                                                                                                                                                                                        |
| aws_key_vault_download_url       | Predefined                                 | URL to AWS Key Vault tar.                                                                                                                                                                                                                          |
| hashicorp_key_vault_download_url | Predefined                                 | URL to Hashicorp Key Vault tar.                                                                                                                                                                                                                    |
| libsodium_download_url           | Predefined                                 | URL to Libsodium tar.gz.                                                                                                                                                                                                                           |
| tessera_base_dir                 | /opt/tessera                               | Base directory for Tessera binary and dependencies.                                                                                                                                                                                                |
| tessera_install_dir              | /opt/tessera/tessera-{{ tessera_version }} | Installation directory for Tessera.                                                                                                                                                                                                                |
| tessera_config_dir               | /etc/tessera                               | Configuration directory for Tessera.                                                                                                                                                                                                               |
| tessera_log_dir                  | /var/log/tessera                           | Log directory for Tessera.                                                                                                                                                                                                                         |
| tessera_libsodium_dir            | /opt/tessera/libsodium                     | Libsodium installation directory.                                                                                                                                                                                                                  |
| default_log_level                | INFO                                       | Set the log level for Tessera.                                                                                                                                                                                                                     |
| jdbc_url                         | ---                                        | JDBC connection URL.                                                                                                                                                                                                                               |
| jdbc_username                    | "sa"                                       | JDBC username.                                                                                                                                                                                                                                     |
| jdbc_password                    | ""                                         | JDBC password.                                                                                                                                                                                                                                     |
| disable_peer_discovery           | false                                      | If set to true, then communication is limited to peers in config file.                                                                                                                                                                             |
| use_whitelist                    | false                                      | If set to true, then connection to Tessera will be restricted to specified peers.                                                                                                                                                                  |
| run_with_besu                    | false                                      | Set this to true if Tessera will be run with Besu instead of GoQuorum.                                                                                                                                                                             |
| bootstrap_mode                   | false                                      | If set to true, then node functions as bootstrap for other nodes.                                                                                                                                                                                  |
| server_configs                   | []                                         | Refer to [docs](https://docs.tessera.consensys.net/en/stable/Reference/SampleConfiguration/#serverconfigs).                                                                                                                                        |
| peers                            | []                                         | List of peers to connect.                                                                                                                                                                                                                          |
| public_key                       | ""                                         | Public key for Tessera.                                                                                                                                                                                                                            |
| config_details                   | ""                                         | Configuration details for the protected or unprotected inline key pairs.                                                                                                                                                                           |
| private_key_path                 | ""                                         | Path to private key.                                                                                                                                                                                                                               |
| public_key_path                  | ""                                         | Path to public key.                                                                                                                                                                                                                                |
| private_key                      | ""                                         | Private key for Tessera.                                                                                                                                                                                                                           |
| aws_secret_manager               | false                                      | Set this to true if using AWS Secrets Manager.                                                                                                                                                                                                     |
| aws_region                       | us-east-1                                  | Set this to desired AWS region for Secrets Manager.                                                                                                                                                                                                |
| aws_SecretsManager_PublicKeyId   | ""                                         | AWS Secrets Manager Public Key ID.                                                                                                                                                                                                                 |
| aws_SecretsManager_PrivateKeyId  | ""                                         | AWS Secrets Manager Private Key ID.                                                                                                                                                                                                                |
| azure_key_vault                  | false                                      | Set this to true if using Azure Key Vault.                                                                                                                                                                                                         |
| azure_Vault_PrivateKeyId         | ""                                         | Azure Private Key ID.                                                                                                                                                                                                                              |
| azure_Vault_PublicKeyId          | ""                                         | Azure Public Key ID.                                                                                                                                                                                                                               |
| azure_Vault_PublicKeyVersion     | ""                                         | Azure Public Key Version.                                                                                                                                                                                                                          |
| azure_Vault_PrivateKeyVersion    | ""                                         | Azure Private Key Version.                                                                                                                                                                                                                         |
| hashicorp_vault                  | false                                      | Set to true if using Hashicorp Vault.                                                                                                                                                                                                              |
| vault_url                        | "https://localhost:8200"                   | Set the vault URL.                                                                                                                                                                                                                                 |
| tls_KeyStorePath                 | ""                                         | Path to TLS Key Store.                                                                                                                                                                                                                             |
| tls_TrustStorePath               | ""                                         | Path to Trust Store.                                                                                                                                                                                                                               |
| app_role_Path                    | not-default                                |                                                                                                                                                                                                                                                    |
| hashicorp_vaultSecretEngineName  | ""                                         | Vault Secret Engine Name.                                                                                                                                                                                                                          |
| hashicorp_vaultSecretName        | ""                                         | Secret Name.                                                                                                                                                                                                                                       |
| hashicorp_vaultSecretVersion     | ""                                         | Secret Version.                                                                                                                                                                                                                                    |
| hashicorp_vaultPrivateKeyId      | ""                                         | Private Key ID.                                                                                                                                                                                                                                    |
| hashicorp_vaultPublicKeyId       | ""                                         | Public Key ID.                                                                                                                                                                                                                                     |
| enable_remoteKeyValidation       | false                                      | Checks that a remote node owns the public keys being advertised.                                                                                                                                                                                   |
| enable_privacyEnhancements       | false                                      | Enable Party Protection (PP) and Private State Validation (PSV).                                                                                                                                                                                   |
| enable_multiplePrivateStates     | false                                      | Enable Multiple Private States feature.                                                                                                                                                                                                            |
| always_send_to                   | []                                         | Comma-separated list of public keys to include as recipients for every transaction sent through the node. This allows you to configure a node that is sent a copy of every transaction, even if it is not specified as a party to the transaction. |
| symmetric_cipher                 | "AES/GCM/NoPadding"                        |                                                                                                                                                                                                                                                    |
| elliptic_curve                   | "secp256r1"                                |                                                                                                                                                                                                                                                    |
| nonce_length                     | "24"                                       |                                                                                                                                                                                                                                                    |
| shared_key_length                | "32"                                       |                                                                                                                                                                                                                                                    |

## Example Usage

Amazon Linux 2:

1. `sudo amazon-linux-extras install epel -y`
2. `sudo yum install ansible`
3. `git clone git@github.com:ConsenSys/ansible-role-tessera.git`
4. `cd ansible-role-tessera`
5. `sudo ansible-playbook -e tessera_version=21.10.0 -e config_details='{"data":{"bytes":"Wl+xSyXVuuqzpvznOS7dOobhcn4C5auxkFRi7yLtgtA="},"type":"unlocked"}' -e public_key="BULeR8JyUWhiuuCMU/HLA0Q5pzkYT+cHII3ZKBey3Bo=" tessera.yml -vvv`

Ubuntu/Debian:

1. `sudo apt update`
2. `sudo apt install ansible`
3. `git clone git@github.com:ConsenSys/ansible-role-tessera.git`
4. `cd ansible-role-tessera`
5. `sudo ansible-playbook -e tessera_version=21.10.0 -e config_details='{"data":{"bytes":"Wl+xSyXVuuqzpvznOS7dOobhcn4C5auxkFRi7yLtgtA="},"type":"unlocked"}' -e public_key="BULeR8JyUWhiuuCMU/HLA0Q5pzkYT+cHII3ZKBey3Bo=" tessera.yml -vvv`

_Note_: The above `config_details` and `public_key` information is for demonstration purposes only in a dev environment. They should NOT be used in production. Please see [Tessera docs](https://docs.tessera.consensys.net/en/stable/HowTo/Generate-Keys/Generate-Keys/) on how to generate new keys and use Vault services.

_Note_: The above command should only be used for dev environments. Usually you would need to specify your own `peers` and `server_config` to meet your requirements.

Alternative to putting environment variables in command-line:

1. Edit existing `tessera.yml` in the root directory of the project.
2. Add `vars` to `tessera.yml` like below:

```yaml
- hosts: localhost
  connection: local
  force_handlers: True
  tasks:
    - include_role:
        name: tessera
  vars:
    tessera_version: 21.10.0
    config_details: '["data":{"bytes":"Wl+xSyXVuuqzpvznOS7dOobhcn4C5auxkFRi7yLtgtA="},"type":"unlocked"}]'
    public_key: BULeR8JyUWhiuuCMU/HLA0Q5pzkYT+cHII3ZKBey3Bo=
```

3. Run the result with the following: `ansible-playbook -v tessera.yml -vvv`

## Licence

Apache

## Author Information

ConsenSys, 2021
