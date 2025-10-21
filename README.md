# 🚀 Elevate Labs Task 2: Launch a Virtual Machine (VM) Instance

![AWS Badge](https://img.shields.io/badge/AWS-EC2-orange?logo=amazonaws)
![Ubuntu Badge](https://img.shields.io/badge/Ubuntu-22.04%20LTS-blue?logo=ubuntu)
![SSH Badge](https://img.shields.io/badge/SSH-Remote%20Access-green?logo=gnu-bash)
![Linux Badge](https://img.shields.io/badge/WSL-Linux%20Subsystem-lightgrey?logo=linux)

> ✅ **Objective:** Deploy a virtual machine using AWS EC2 and securely access it via EC2 INSTANCE CONNECT from my REMOTE Linux subsystem (FROM AWS CONSOLE ITSELF). This task demonstrates real-world cloud infrastructure setup and connectivity.

---

## 🧠 What This Project Demonstrates

- ✅ EC2 provisioning with Ubuntu 22.04 LTS
- ✅ Key pair generation and secure SSH access
- ✅ Networking setup with setting up HTTP,HTTPS,SSH TRAFFIC
- ✅ Real-time troubleshooting and documentation


- ✅ Professional presentation with diagrams and screenshots

---

# 🚀 Launching an EC2 Instance on AWS


Welcome to my cloud infrastructure showcase! This task demonstrates how I launched a virtual machine (VM) using **Amazon EC2**, accessed it via browser-based SSH, and documented the configuration for clarity and reproducibility.

---



## 📸 Screenshots

EC2 Instance Running:

<img width="2223" height="691" alt="ec2-instance-running png" src="https://github.com/user-attachments/assets/1f62ff61-d7fa-49e1-9f63-baed8ecb7993" />

---

SSH ACCESS TO THE WEB BROWSER USING EC2 INSTANCE CONNECT:

<img width="2151" height="849" alt="ec2-ssh-terminal png" src="https://github.com/user-attachments/assets/e01af827-4c54-4854-a791-5864ab5a42e2" />

---

<img width="2270" height="1255" alt="inside_the_ubuntu_machine png" src="https://github.com/user-attachments/assets/8748f60d-0c27-4db8-84f6-1ec689b10f16" />

---

# 🧩 EC2 Instance Creation Challenges

### 🌍 Region Selection Confusion
- ❌ Initially launched the instance in a region different from my default (e.g., `ap-south-1` instead of `us-east-1`).
- ✅ Realized EC2 Instance Connect only works in supported regions and re-launched in `us-east-1`.

### 🔐 SSH Access Issues
- ❌ Tried connecting via `.pem` file in terminal but faced firewall and permission errors.
- ✅ Switched to **EC2 Instance Connect** (browser-based SSH), which worked instantly without key pair setup.

### 🔄 Instance Type Selection
- ❌ Was unsure whether to choose `t2.micro`, `t3.micro`, or `t2.nano`.
- ✅ Researched Free Tier eligibility and performance trade-offs, then selected `t2.micro` for balance.

### 🛡️ Security Group Misconfiguration
- ❌ Forgot to allow inbound SSH (port 22), which blocked access.
- ✅ Edited the security group to allow SSH from my IP and added HTTP (port 80) for future web server setup.

### 🧠 AMI Selection Doubts
- ❌ Confused between Amazon Linux, Ubuntu, and other AMIs.
- ✅ Chose **Ubuntu 22.04 LTS** for familiarity and compatibility with internship tasks.

---

> 💡 These challenges helped me understand EC2 architecture, region behavior, and secure access setup. I now feel confident launching and managing VMs on AWS.

---

## 🧠 Advanced EC2 CLI Commands for Real-World Challenges

| ⚠️ Scenario / Task                      | 💻 CLI Command Example                                                                 |
|----------------------------------------|----------------------------------------------------------------------------------------|
| **Check instance metadata (from EC2)** | `curl http://169.254.169.254/latest/meta-data/`                                       |
| **List stopped instances**             | `aws ec2 describe-instances --filters Name=instance-state-name,Values=stopped`        |
| **Find instance by tag**               | `aws ec2 describe-instances --filters Name=tag:Name,Values=MyAppServer`               |
| **Get instance launch time**           | `aws ec2 describe-instances --instance-ids i-xxxxxxxx --query 'Reservations[*].Instances[*].LaunchTime'` |
| **Attach volume to instance**          | `aws ec2 attach-volume --volume-id vol-xxxxxxxx --instance-id i-xxxxxxxx --device /dev/sdf` |
| **Detach volume from instance**        | `aws ec2 detach-volume --volume-id vol-xxxxxxxx`                                      |
| **Modify instance type (resize)**      | `aws ec2 modify-instance-attribute --instance-id i-xxxxxxxx --instance-type "{\"Value\": \"t3.medium\"}"` |
| **Create Elastic IP**                  | `aws ec2 allocate-address`                                                            |
| **Associate Elastic IP**               | `aws ec2 associate-address --instance-id i-xxxxxxxx --allocation-id eipalloc-xxxxxxxx` |
| **Disassociate Elastic IP**            | `aws ec2 disassociate-address --association-id eipassoc-xxxxxxxx`                     |
| **Create new security group**          | `aws ec2 create-security-group --group-name MySG --description "My security group"`   |
| **Add inbound rule to SG**             | `aws ec2 authorize-security-group-ingress --group-id sg-xxxxxxxx --protocol tcp --port 80 --cidr 0.0.0.0/0` |
| **Revoke inbound rule from SG**        | `aws ec2 revoke-security-group-ingress --group-id sg-xxxxxxxx --protocol tcp --port 80 --cidr 0.0.0.0/0` |
| **Create EC2 instance with CLI**       | `aws ec2 run-instances --image-id ami-xxxxxxxx --count 1 --instance-type t3.micro --key-name MyKey --security-group-ids sg-xxxxxxxx --subnet-id subnet-xxxxxxxx` |
| **Enable termination protection**      | `aws ec2 modify-instance-attribute --instance-id i-xxxxxxxx --disable-api-termination` |
| **Check termination protection status**| `aws ec2 describe-instance-attribute --instance-id i-xxxxxxxx --attribute disableApiTermination` |
| **Create AMI backup of instance**      | `aws ec2 create-image --instance-id i-xxxxxxxx --name "Backup-AMI"`                   |
| **List snapshots by volume**           | `aws ec2 describe-snapshots --filters Name=volume-id,Values=vol-xxxxxxxx`             |
| **Delete unused AMI**                  | `aws ec2 deregister-image --image-id ami-xxxxxxxx`                                    |
| **Delete snapshot**                    | `aws ec2 delete-snapshot --snapshot-id snap-xxxxxxxx`                                 |

---

## 🏗️ Future Architecture Vision: EC2-Based Application Deployment

To scale my cloud projects beyond basic EC2 provisioning, I plan to adopt a production-grade architecture that includes:

- ✅ EC2 instances behind a Load Balancer
- ✅ Auto Scaling Groups for elasticity
- ✅ VPC with public/private subnets
- ✅ Security Groups and IAM roles
- ✅ S3 for static assets and backups
- ✅ CloudWatch for monitoring and alerts

![Future EC2 Architecture](https://miro.medium.com/v2/resize:fit:1358/1*Y_yVaRGvQtYgp2zXDzv0pw.gif)

> This architecture reflects my goal to build resilient, scalable, and secure cloud-native applications using AWS best practices.


## 🧰 SSH Tools: MobaXterm vs PuTTY

When accessing EC2 instances remotely, two popular SSH clients used in corporate and academic environments are **MobaXterm** and **PuTTY**. Here's a clear comparison:

| Feature                     | **MobaXterm**                                      | **PuTTY**                                         |
|-----------------------------|----------------------------------------------------|---------------------------------------------------|
| 🖥️ Interface                | Graphical + tabbed terminal                        | Basic GUI with single session window              |
| 🔐 SSH Support              | Built-in SSH, SFTP, X11, and remote desktop        | SSH only (SFTP via separate tool: WinSCP)         |
| 📁 File Transfer            | Integrated SFTP browser (drag-and-drop)            | Requires external tool (WinSCP)                   |
| 🧠 Usability                | Beginner-friendly with rich features               | Lightweight and minimal                           |
| 📦 Portability              | Portable version available                         | Portable version available                        |
| 🧰 Extra Tools              | Includes X11 server, RDP, VNC, FTP, and more       | SSH, Telnet, Serial, basic logging                |
| 🧪 EC2 Compatibility        | Supports `.pem` files directly                     | Requires `.pem` to `.ppk` conversion via PuTTYgen |
| 🧑‍💻 Ideal For              | DevOps, cloud engineers, multi-session workflows   | Lightweight SSH access and scripting              |

---

## 💡 Lessons Learned

This task helped me move from basic EC2 usage to understanding real-world cloud infrastructure challenges. Here's what I learned:

- 🌍 **Region Selection Matters:** I initially launched my EC2 instance in `ap-south-1`, but EC2 Instance Connect wasn’t supported there. I re-launched in `us-east-1`, learning to always verify region compatibility before provisioning.

- 🔐 **SSH Access Isn’t Always Plug-and-Play:** I faced permission errors using `.pem` files in WSL. Switching to EC2 Instance Connect (browser-based SSH) taught me how to troubleshoot access issues and use alternate methods.

- ⚙️ **Choosing the Right Instance Type Requires Strategy:** I compared `t2.micro`, `t3.micro`, and `t2.nano`, and learned how Nitro system architecture affects performance, cost, and Free Tier eligibility.

- 🛡️ **Security Groups Are Critical:** I forgot to allow inbound SSH (port 22), which blocked access. I fixed it by editing the security group and also added HTTP/HTTPS for future web server deployment.

- 📸 **Documentation Is a Superpower:** Organizing screenshots, diagrams, and CLI commands into folders helped me troubleshoot faster and made my repo a reusable learning resource for others.

> 🚀 This task gave me hands-on experience with Infrastructure-as-a-Service (IaaS), and boosted my confidence in deploying, securing, and documenting cloud-based virtual machines.

---

## ☁️ Cloud Service Models: IaaS vs PaaS vs SaaS

Understanding the three core cloud service models helps clarify where EC2 fits in the cloud stack:

| Model | Description | Example | User Controls |
|-------|-------------|---------|---------------|
| 🧱 **IaaS** (Infrastructure as a Service) | Provides virtualized computing resources over the internet | AWS EC2, Azure VM | OS, runtime, storage, networking |
| 🛠️ **PaaS** (Platform as a Service) | Offers hardware and software tools over the internet | AWS Elastic Beanstalk, Heroku | App code, data |
| 📦 **SaaS** (Software as a Service) | Delivers software applications via browser | Gmail, Dropbox, Salesforce | Just usage — everything else is managed |

> 💡 This EC2 project is a classic example of **IaaS**, where I control the OS, networking, and runtime environment.

---

## 🚀 Recent Advancements in EC2 Technology (2025)

Amazon EC2 continues to evolve with powerful new features and instance types designed for modern workloads. Here's what's new:

### 🧠 AI/ML-Optimized Instances
- **Trn2 Instances**: Built for training large-scale machine learning models using AWS Trainium chips.
- **Inf2 Instances**: Designed for high-throughput inference tasks using AWS Inferentia2 accelerators.

### 💰 Cost-Efficient Compute
- **Graviton4 Instances**: ARM-based processors offering up to 30% better price-performance than previous generations.
- **EC2 Spot Advisor**: A tool that recommends optimal spot instance types based on historical interruption rates.

### 🌍 Global Infrastructure Expansion
- **Local Zones**: AWS now offers compute closer to end-users in metro areas for ultra-low latency.
- **Wavelength Zones**: EC2 integrated with 5G networks for edge computing use cases.

### 🔐 Security & Isolation
- **Nitro Enclaves**: Isolated compute environments for processing sensitive data securely.
- **IAM Roles Anywhere**: Enables secure access to AWS resources from outside AWS (e.g., on-prem servers).

### 📦 Deployment & Automation
- **Launch Templates with Versioning**: Define reusable EC2 configurations with version control.
- **EventBridge EC2 Scheduler**: Automate instance start/stop based on custom schedules and events.

---

## 🧠 Glossary of New Technical Terms

| Term                 | Description |
|----------------------|-------------|
| **Trainium**         | AWS-designed chip for ML training workloads |
| **Inferentia2**      | AWS chip for fast, cost-effective ML inference |
| **Graviton4**        | Latest ARM-based CPU offering high performance and efficiency |
| **Nitro Enclaves**   | Secure, isolated environments for sensitive data processing |
| **Local Zones**      | AWS infrastructure deployed in metro areas for low-latency access |
| **Wavelength Zones** | EC2 integrated with telecom 5G networks for edge computing |
| **IAM Roles Anywhere** | Lets external systems securely access AWS resources |
| **Launch Templates** | Predefined EC2 configurations with version control |
| **EventBridge Scheduler** | Automates EC2 actions based on events or time triggers |

---




## ⚙️ VM Configuration Summary

```txt
🖥️ OS: Ubuntu 22.04 LTS  
🌍 Region: ap-south-1 (Asia Pacific(MUMBAI))  
📦 Instance Type: t3.micro (Free Tier Eligible)

bash commands
uname -a
ls
whoami




