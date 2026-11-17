# Jekyll Demo Deployment Example

**PREREQUISITES:**

- Ansible Core on your control node (or target if you deploy locally):
  ```
  sudo apt update && sudo apt install -y ansible-core`
  ```

**QUICKSTART:**

To deploy the application to the local machine for testing:
```
ansible-playbook playbook.yaml -i inventory_localhost.ini
```

To deploy to a remote VM, create an `inventory.ini` file specifying the target hosts and run:
```
ansible-playbook playbook.yaml -i inventory.ini
```

By default the playbook reads the subpath from the SimpleVM metadata
(`location_url` in `/etc/simplevm/metadata.json`).
To override it manually, pass `location_url` via `-e`:
```
ansible-playbook playbook.yaml -i inventory.ini -e location_url="jekyll_100"
```

---

This repository contains two main parts:

- a **Jekyll application** located in the `app/` directory
- an **Ansible playbook** used to deploy that application to a virtual machine

The purpose of this repository is to provide a simple example of how an **Jekyll app** can be deployed automatically to a newly created instance.

After a new VM has been created, the included Ansible playbook can be used to:

- install the required software
- build the static webpages
- serve them with Nginx on port `3838` under a subpath

This makes it possible to quickly provision a fresh machine and make the example application available with minimal manual setup.

## How it Works

The deployment process is straightforward:
1. Create a new instance in SimpleVM.
2. Connect to your VM with the given ssh command.
3. Run the ansible playbook.
4. Access the web site!

Once deployed, the application can be accessed through the corresponding link provided in **SimpleVM**, for example through the **Web Service** section.

## Notes

This repository is intended as a minimal demonstration example for automated deployment of an application in a VM-based environment.

It can be used as a starting point for testing, teaching, or extending similar deployment workflows in SimpleVM.
