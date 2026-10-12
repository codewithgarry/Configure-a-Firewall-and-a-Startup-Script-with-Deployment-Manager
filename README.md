# Configure a Firewall and a Startup Script with Deployment Manager (GSP302)

![Google Cloud](https://img.shields.io/badge/Google_Cloud-4285F4?logo=googlecloud&logoColor=white)
![Lab](https://img.shields.io/badge/Lab-GSP302-34A853)
![IaC](https://img.shields.io/badge/IaC-Deployment_Manager-orange)

Reference solution for the Google Cloud challenge lab **Configure a Firewall and a Startup Script with Deployment Manager** (GSP302).

## 📖 Overview

You complete a Deployment Manager template so that one deployment creates:

- A Compute Engine VM that installs **Apache** with a startup script.
- A firewall rule that allows **HTTP (tcp/80)** to instances tagged `http`.

## 🧰 Services used

Cloud Deployment Manager · Compute Engine · VPC firewall rules

## 📁 Repository structure

```text
.
├── README.md
├── qwiklabs.jinja   # completed template: VM + startup script + firewall rule
└── qwiklabs.yaml    # deployment config (unchanged from the lab)
```

## 🚀 Solution

### 1. Get the lab files

```bash
mkdir deployment_manager && cd deployment_manager
gsutil cp gs://spls/gsp302/* .
```

### 2. Replace the template

Replace the contents of `qwiklabs.jinja` with [`qwiklabs.jinja`](qwiklabs.jinja) from this repo. Leave `qwiklabs.yaml` and `qwiklabs.jinja.schema` unchanged.

### 3. Deploy

```bash
gcloud deployment-manager deployments create deployment-templates --config qwiklabs.yaml
```

### 4. Verify

```bash
gcloud compute instances list
curl http://$(gcloud compute instances describe vm-test --zone us-central1-a \
  --format='value(networkInterfaces[0].accessConfigs[0].natIP)')
```

You should see the Apache default page.

## 🔎 Version notes

- Deployment Manager is deprecated in favour of **Infrastructure Manager** and **Terraform**.
- The original lab used the `debian-9` image family, which is retired. The template uses `debian-11`.

---

## ⚠️ Notes

- Resource names, zones, regions and ports are generated per lab session. Always use the values shown in **your** lab instructions.
- These steps were written when the lab was live. Google revises labs over time, so the current version may differ.

## 📌 Disclaimer

This repository is a study reference. Attempt the lab on your own first, then compare approaches. It is not affiliated with or endorsed by Google.

## 👤 Author

**Girish Sharma** · Cloud & DevOps Engineer · [GitHub](https://github.com/codewithgarry) · [LinkedIn](https://www.linkedin.com/in/codewithgarry/)
