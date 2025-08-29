
# Ansible ELK & RabbitMQ Stack

This project automates the deployment of an Elasticsearch cluster, Kibana, and a RabbitMQ cluster using Ansible. It supports multiple environments and leverages Ansible roles and vault for secure configuration management.

## Features

- **Deploys Elasticsearch (master and nodes) and RabbitMQ in clusters**
- **Deploys Kibana**
- **Supports multiple environments** (development, staging, production) via inventory files
- **Uses Ansible roles** for modular, reusable automation
- **Secures secrets** using Ansible Vault

## Project Structure

- `inventory/` — Environment-specific inventory files and group variables
- `playbooks/` — Main playbooks and role definitions
- `roles/` — Role implementations for Elasticsearch, Kibana, RabbitMQ
- `secrets.yml` — Encrypted secrets (do not share this file)

## Using Ansible Vault

Create a new encrypted secrets file:

```bash
ansible-vault create secrets.yml
```

Encrypt a single value and append it to a vars file (e.g., for production Elasticsearch password):

```bash
ansible-vault encrypt_string '123456789' --name 'elastic_prod1_password' >> inventory/group_vars/prod.yml
```

View an encrypted file:

```bash
ansible-vault view secrets.yml
```

## Running the Playbook

To deploy to a specific environment (e.g., staging):

```bash
ansible-playbook --ask-vault-pass -i inventory/stage.ini playbooks/site.yml
```

Replace `stage.ini` with `prod.ini` or `dev.ini` as needed.

---

**Note:**
- Never commit unencrypted secrets or sensitive data.
- Make sure to update your `.gitignore` to exclude files like `secrets.yml` and any other sensitive files.
