Di projek kalii ini saya akan menjelaskan bagiamana cara membangun sebuah infrastructure cloud aws tanpa mengeluarkan uang karena full gratis!!,sebenarnya ini adalah projek
phase 2 dari projek sebelumnya yang [ini](https://rizkiyusupk.github.io/devops/clouds/linux/server/iac/infrastructure/aws1/) dan menggabungkan projek [KVM/QEMU PHASE 2](https://rizkiyusupk.github.io/devops/kubernetes/linux/server/iac/infrastructure/observ-tools/),
di projek ini saya akan melengkapi projek 
sebelumnya dengan infrastructure yang sebelumnya sudah saya bangun,dengan menambahkan tools seperti k8s,jenkins,dan observ tools ditambah alert lewat telegram,kurang lebih 
begitu langsung saja masuk ke pembahasanya


| Node        | CPU     | RAM  | Storage | Network                             |
|-------------|---------|------|---------|------------------------------------ |
| **Master**  | 2 cores | 2GB  | 10GB    | 1 Adapters   ( Static Ip )          |
| **Worker 1**| 2 cores | 2GB  | 10GB    | 1 Adapters   ( Static Ip )          |
| **Worker 2**| 2 cores | 2GB  | 10GB    | 1 Adapters   ( Static Ip )          |
| **Jenkins** | 7 cores | 7GB  | 240GB   |                Wlan                 |


![sdub](/assets/images/aws2/workflow-aws-2.png)

### Tools
- **Wsl** : v0.2.1
- **Terraform** : v1.15.8
- **Localstack** : v2026.6.3
- **Docker** : v29.1.3
- **Python** : v3.12.3
- **Aws Cli** : v1.45.52
- **OS Laptop 1** : Windows 11 Pro
- **OS WSL2 Subsystem** : Ubuntu 24.04 LTS
- **OS Ubuntu VM (K8s Nodes)** : 24.04 LTS
- **OS Ubuntu Jenkins Node (Bare Metal)** : 25.04
- **Kubernetes** : 1.28
- **Containerd** : 2.2.4
- **Java** : 21
- **Jenkins** : 2.56
- **Network** : Flannel
- **Git Bash** : 2.51.1
- **Terraform** :  v1.15.6
- **Ansible** : v2.16+
- **Helm** : v3.x
- **Telegram Bot** :
- **KVM** : 8.2.2
- **QEMU** : 8.2.2
- **Libvirt** : 10.0.0
- **Alertmanager** : v0.33.1
- **Loki** : 3.6.7
- **Loki Canary** : 3.6.7
- **Loki Gateway (nginx)** : 1.29-alpine
- **Grafana** : 13.1.0
- **Prometheus Operator** : v0.92.1
- **Prometheus Config Reloader** : v0.92.1
- **Kube State Metrics** : v2.19.1
- **Prometheus** : v3.13.1
- **Node Exporter** : v1.12.0
- **Promtail** : 3.5.1
- **Ngrok**
- **Gitlab** : SaaS
### Reasoning
Kenapa saya memilih untuk membangun phase 2? karena saya penasaran apakah bisa menintegrasikan aws environtment dengan tools tools stand alone dan ini juga sebagai bentuk 
pembelajaran bagi saya agar saya familiar dengan service yang ada di aws,dan kenepaa saya memilih untuk menggunakan localstack alasan utamanya  karena gratis

### STRUCTURE FOLDER 

Untuk structure folder yang digunakan dalam projek ini ada tiga yang pertama itu untuk terraform dan yang kedua itu ansible terakhir itu ada di cluster,

```
terraform-setup/
├── .terraform/
├── compute.tf
├── main.tf
├── prep-vm.tf
├── terraform.tfstate
├── terraform.tfstate.backup
├── s3.tf
├── sns.tf
├── sqs.tf
├── sqs-trigger-lambda.tf
├── iam-attachment-role.tf
├── iam-attachment-role-consumer.tf
├── lambda_function_consumer.py
├── lambda_function.py
├── lambda-permission.tf
├── lambda.tf
├── lambda-2.tf
├── cloud-watch.tf
├── cloud-watch-metrics.tf
├── dynamodb.tf
├── terraform.tfvars
```

lalu yang kedua

```
k8s/
├── ansible.cfg
├── inventory
├── playbook-allow-port.yaml
├── playbook-enable-service-baremetal.yaml
├── playbook-ip.yaml
├── playbook-install-java-baremetal.yaml
├── playbook-install-jenkins-baremetal.yaml
├── playbook-install-kubectl-baremetal.yaml
├── playbook-join.yaml
├── playbook-kubernetes.yaml
├── playbook-pkg.yaml
|__ playbook-swap.yaml
```

dan yang terakhir yang ketiga di cluster 

```
cluster-side/
├── alertmanager-telegram.yaml
```
