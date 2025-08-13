# 🚀 Create Terraform Infrastructure with Docker  

[![Terraform](https://img.shields.io/badge/Terraform-v1.7-blueviolet)](https://www.terraform.io/)  
[![Docker](https://img.shields.io/badge/Docker-Enabled-blue)](https://www.docker.com/)  

This project demonstrates how to provision and destroy an **NGINX** container using **Terraform** with the Docker provider.  

---

## ⚙️ Prerequisites  
Before you start, make sure you have:  
- **[Terraform](https://developer.hashicorp.com/terraform/downloads)** ≥ 1.7  
- **[Docker](https://docs.docker.com/get-docker/)** installed and running  

---

## 📝 Step 1: Configure `terraform.tf`  
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.2"
    }
  }
  required_version = "~> 1.7"
}
🛠 Step 2: Configure main.tf

provider "docker" {}

resource "docker_image" "nginx" {
  name         = "docker.mirror.hashicorp.services/nginx:latest"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "tutorial"

  ports {
    internal = 80
    external = 8000
  }
}
🚀 Step 3: Initialize the Project

terraform init
This will download the Docker provider plugin.

📦 Step 4: Apply the Configuration

terraform apply
When prompted, type yes and press ENTER.

🔍 Step 5: Verify the NGINX Container

docker ps
You should see the tutorial container running with port 8000 exposed.

🗑 Step 6: Destroy the Infrastructure

terraform destroy
When prompted, type yes and press ENTER.

⚡ Quick Start (All Commands)

terraform init
terraform apply -auto-approve
docker ps
terraform destroy -auto-approve

✅ You have successfully provisioned and destroyed an NGINX web server using Terraform and Docker!
