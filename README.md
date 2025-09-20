# EC2 SSH Management with Ansible: Seamless Passwordless & Password Authentication

## 🚀 Overview

This guide explains step-by-step how to set up hybrid SSH management for AWS EC2 instances using Ansible, **entirely from the command prompt**. You’ll configure both key-based (passwordless) and password-based authentication, enabling flexible automation across diverse environments.
![image2](image2)

---

## 🖥️ Prerequisites

- AWS account and EC2 instances (at least two: one for key-based, one for password-based SSH)
- Ansible installed on your control node (`pip install ansible`)
- SSH keys generated and available for key-based authentication
- Access to the command prompt (Linux/macOS/WSL/Windows Terminal)

---

## 1️⃣ Clone the Repository

```bash
git clone https://github.com/Naveen15github/EC2-SSH-Management-with-Ansible-Seamless-Passwordless-Password-Authentication.git
cd EC2-SSH-Management-with-Ansible-Seamless-Passwordless-Password-Authentication
```

---

## 2️⃣ Configure Inventory File

Create or edit `inventory` to define your managed nodes:

```ini
[passwordless]
manage_node1 ansible_host=EC2_PUBLIC_IP_1 ansible_user=ec2-user ansible_ssh_private_key_file=~/.ssh/id_rsa

[password]
manage_node2 ansible_host=EC2_PUBLIC_IP_2 ansible_user=ec2-user ansible_ssh_pass=YOUR_PASSWORD
```

Replace `EC2_PUBLIC_IP_1`, `EC2_PUBLIC_IP_2`, and `YOUR_PASSWORD` with actual values.

---

## 3️⃣ Prepare Your Ansible Playbook

Create `hybrid-ec2-management.yml`:

```yaml
---
- name: Hybrid EC2 SSH Management
  hosts: all
  tasks:
    - name: Ping EC2 Instance
      ansible.builtin.ping:
```

---

## 4️⃣ Test SSH Connectivity

Check passwordless node:

```bash
ssh -i ~/.ssh/id_rsa ec2-user@EC2_PUBLIC_IP_1
```

Check password node:

```bash
ssh ec2-user@EC2_PUBLIC_IP_2
# Enter password when prompted
```

---

## 5️⃣ Run the Ansible Playbook

```bash
ansible-playbook -i inventory hybrid-ec2-management.yml
```

- This will ping all defined nodes (both passwordless and password authentication) and display results.

---

## 6️⃣ Example Output Screenshots

### EC2 Instances in AWS Console

![image2](image2)

### SSH Connectivity Success

![image3](image3)


*(Replace `image1`, `image2`, etc. with your actual screenshots in the `images/` directory.)*

---

## 7️⃣ Troubleshooting Tips

- Ensure security groups allow SSH (port 22) from your control node IP.
- Verify SSH key permissions (`chmod 600 ~/.ssh/id_rsa`).
- For password nodes, check that password authentication is enabled in `sshd_config`.

---

## 8️⃣ Repository Structure

```
├── inventory
├── hybrid-ec2-management.yml
├── README.md
├── images/
│   ├── image1.png
│   ├── image2.png
│   ├── image3.png
│   └── image4.png
```

---

## 9️⃣ References

- [Ansible Documentation](https://docs.ansible.com/)
- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)

---

## 1️⃣0️⃣ Author

**Naveen15github**  
[GitHub Profile](https://github.com/Naveen15github)
