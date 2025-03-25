# 🧪 Simple Load Balancer Lab (Vagrant + Ansible)

This lab simulates a basic load-balanced environment using **Vagrant**, **Ansible**, and **Rocky Linux**.

It sets up:
- `web1` and `web2`: Apache web servers
- `lb`: HAProxy load balancer
- All nodes connected via a private network (`192.168.152.0/24`)

---

## ⚙️ Lab Architecture

```
            +--------------------+
            |    Load Balancer   |
            |    (HAProxy - lb)  |
            |   192.168.152.10   |
            +---------+----------+
                      |
        +-------------+-------------+
        |                           |
+----------------+       +----------------+
|   Web Server 1  |       |   Web Server 2  |
| (Apache - web1) |       | (Apache - web2) |
| 192.168.152.11  |       | 192.168.152.12  |
+----------------+       +----------------+
```

---

## 📦 Tech Stack

- [Vagrant](https://www.vagrantup.com/)
- [Ansible (Local Provisioning)](https://docs.ansible.com/)
- [HAProxy](http://www.haproxy.org/)
- [Apache HTTPD](https://httpd.apache.org/)
- Rocky Linux 9 base image (`generic/rocky9`)

---

## 🚀 Getting Started

### 🔧 Prerequisites

- VMware Workstation Pro
- Vagrant
- `vagrant-vmware-desktop` plugin

### 📂 Folder Structure

```
simple-lb-lab/
├── Vagrantfile
├── README.md
├── .gitignore
├── ansible/
│   ├── site.yml
│   └── roles/
│       ├── web/
│       │   └── tasks/main.yml
│       └── lb/
│           └── tasks/main.yml
├── web/
│   ├── index.html
│   └── styles.css
```

### ▶️ To Run the Lab

```bash
vagrant up --provider=vmware_desktop
```

To SSH into a VM:
```bash
vagrant ssh web1
```

To reprovision:
```bash
vagrant reload --provision
```

---

## 🔐 Firewall Considerations

Rocky Linux enables `firewalld` by default. Ansible roles open port `80` on the web servers to allow traffic from the load balancer.

---

## 🖥️ Web Interface

Once running, visit:
- `http://192.168.152.10` → load-balanced page
- You should see alternating content from `web1` and `web2`

---

## 🧑‍💻 Author

Maintained by: Alexandros Mandravillis  
Built as a learning and DevOps experimentation lab.
