+++
date = '2026-03-10T21:07:45+07:00'
draft = false
title = 'TIL: How to Connect to a GKE Cluster Using the Google Cloud CLI'
tags = ["gcp", "gke", "kubernetes", "gcloud"]
categories = ["Cloud"]
+++

If you need to access a Google Kubernetes Engine (GKE) cluster but aren't sure where to start, you can easily find your project, locate the cluster, and configure your local environment using the `gcloud` CLI.

Here is a quick step-by-step guide on how to do it.

---

### Step 1: Find Your Project ID

First, you need to identify the exact Project ID where your cluster lives. You can list all the Google Cloud projects you have access to with the following command:

```bash
gcloud projects list

```

**Example Output:**

```text
PROJECT ID                      NAME                        PROJECT NUMBER
prj-stg-app123                  prj-stg-app                 12345678910
prj-prod-app987654              prj-prod-app                9876543210

```

*Note the `PROJECT ID` (e.g., `prj-prod-app987654`), as you will need it for the next steps.*

### Step 2: List Clusters in the Project

Once you have your Project ID, you can list all the GKE clusters running inside that specific project to find the name and region of your target cluster:

```bash
gcloud container clusters list --project=<your-project-id>

```

**Example:**

```bash
gcloud container clusters list --project=prj-prod-app987654

```

### Step 3: Get Cluster Credentials

To actually interact with the cluster using `kubectl`, you need to pull down the credentials and add them to your local `kubeconfig` file. Use the `get-credentials` command along with the cluster name, region, and project ID:

```bash
gcloud container clusters get-credentials <cluster-name> \
    --region=<region-name> \
    --project=<project-id>

```

**Example:**

```bash
gcloud container clusters get-credentials prod-banking-k8s \
    --region=asia-southeast2 \
    --project=prj-prod-app987654

```

Once this command completes successfully, your `kubectl` context will automatically switch to this new cluster.

---

### 💡 Pro-Tip: Managing Multiple Contexts

If you work across multiple clusters and environments (like dev, staging, and prod), switching between `kubectl` contexts manually can get tedious.

I highly recommend checking out **`kubectx`** and **`kubens`**. They are absolute lifesavers for navigating multiple Kubernetes environments quickly.

You can read more about it here: [kubectx: The ultimate tool to manage Kubernetes contexts](https://ahmet.im/blog/kubectx/).

---

Would you like me to add some basic `kubectl` commands to this article for testing the connection once the context is set?
