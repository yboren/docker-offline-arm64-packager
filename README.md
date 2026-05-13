# Docker Image Transfer ARM64 🚀

An automated cloud utility leveraging GitHub Actions to batch convert and package Docker images into **native ARM64 (aarch64)** offline installation packages. 

Perfect for deploying applications (e.g., Dify, LLM infrastructure, databases) into air-gapped ARM64 cloud servers, enterprise private clouds, or local Apple Silicon (M1/M2/M3/M4) Mac development environments.

## ✨ Key Features
- **Zero Local Setup**: No need to configure complex Docker Buildx, QEMU, or binfmt environments on your local x86 machine.
- **Batch Processing**: Manage all your microservices/dependencies inside a single text file (`docker-list.txt`).
- **High-Speed Cloud Transfer**: Leverages GitHub's high-speed backbone network to fetch layers and convert architectures in minutes.
- **Flexible Triggers**: Run it manually via a button or trigger it automatically on every push to the image list.

---

## 🛠️ Step-by-Step Guide

### Step 1: Update the Image List
Modify the `docker-list.txt` file in the root directory of this repository. Add the images you want to download (one per line, comments starting with `#` are supported):
```text
# Example: Dify Core Components
difyai/dify-api:latest
difyai/dify-web:latest

# Infrastructure Dependencies
postgres:15-alpine
redis:7-alpine
```

### Step 2: Trigger the Workflow
1. Commit and push your changes to `docker-list.txt`.
2. Navigate to the **Actions** tab of this GitHub repository.
3. Select **"Batch Download ARM64 Images"** from the left sidebar.
4. Click the **Run workflow** dropdown on the right side and click the green button.

### Step 3: Download the Offline Tarballs
Once the run completes (usually takes 5-10 minutes for ~30 images), click into the specific workflow run. Scroll down to the **Artifacts** section and click `docker-arm64-batch-package` to download the unified zip archive to your local computer.

### Step 4: Batch Import into your ARM64 Linux Server
Extract the zip file to get your `.tar.gz` files. Transfer them to your target **ARM64 Linux Server**, and run this single-line command in that directory to import all 30+ images into Docker instantly:
```bash
ls *.tar.gz | xargs -I {} sh -c "zcat {} | docker load"
```

---

## 📂 Repository Structure
```text
├── .github/workflows/   # GitHub Actions pipeline configuration
├── docker-list.txt      # The target image manifest file (your main workspace)
├── LICENSE              # MIT License file
└── README.md            # Project documentation and guide
```

## 📄 License
This project is licensed under the [MIT License](LICENSE). Feel free to fork, modify, and distribute it.

