# 🐳 Push a Docker Image to Docker Hub

<p align="center">

<img src="https://img.shields.io/badge/Docker-Docker%20Hub-2496ED?style=for-the-badge&logo=docker&logoColor=white" />
<img src="https://img.shields.io/badge/Cloud%20Computing-Laboratory-6C63FF?style=for-the-badge" />
<img src="https://img.shields.io/badge/Registry-Docker%20Hub-0DB7ED?style=for-the-badge&logo=docker&logoColor=white" />
<img src="https://img.shields.io/badge/Platform-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white" />
<img src="https://img.shields.io/badge/PowerShell-Command%20Line-5391FE?style=for-the-badge&logo=powershell&logoColor=white" />

</p>

<p align="center">
  <b>Cloud Computing Laboratory — Experiment 3</b>
</p>

<p align="center">
  <i>Push a Docker Image to Docker Hub</i>
</p>

---

## 📌 Experiment Overview

This experiment demonstrates how to publish an existing Docker image to **Docker Hub**, an online registry for storing and sharing Docker images.

The Docker image `my-python-app`, created during Experiment 1, is reused without rebuilding the application. The local Docker CLI is authenticated with Docker Hub, the existing image is assigned a Docker Hub-compatible repository name and version tag, and the tagged image is pushed to the remote registry.

The complete workflow is:

```text
Existing Docker Image
        ↓
   docker login
        ↓
Docker Hub Authentication
        ↓
     docker tag
        ↓
USERNAME/my-python-app:v1
        ↓
    docker push
        ↓
     Docker Hub
        ↓
Image Stored Online
```

---

# 🎯 Objectives

The primary objectives of this experiment are:

1. To use an existing Docker image.
2. To create or use a Docker Hub account.
3. To authenticate Docker from PowerShell.
4. To understand Docker Hub repository naming.
5. To tag a local Docker image using the Docker Hub repository format.
6. To push the tagged Docker image to Docker Hub.
7. To verify the uploaded repository and image tag.
8. To understand how Docker images can be shared through a remote registry.
9. To understand the difference between building, tagging, and pushing a Docker image.

---

# 🧠 Learning Outcomes

After completing this experiment, the following concepts are demonstrated:

| Concept | Description |
|---|---|
| 🐳 Docker Image | Existing application image used as the source |
| ☁️ Docker Hub | Online registry for storing and sharing Docker images |
| 🔐 Docker Authentication | Login process used to authenticate the Docker CLI |
| 🏷️ Image Tagging | Assigning a Docker Hub-compatible name and version |
| 📤 Docker Push | Uploading an image to Docker Hub |
| 🔎 Repository Verification | Confirming the uploaded image and tag online |
| 🔄 Image Distribution | Making a Docker image available for use on another machine |

---

# 🏗️ System Architecture

```text
┌───────────────────────────┐
│     Student Computer      │
│                           │
│  Docker Image             │
│  my-python-app:latest     │
└─────────────┬─────────────┘
              │
              │ docker login
              ▼
┌───────────────────────────┐
│     Docker Hub            │
│   Authentication          │
└─────────────┬─────────────┘
              │
              │ docker tag
              ▼
┌───────────────────────────┐
│ USERNAME/my-python-app:v1 │
└─────────────┬─────────────┘
              │
              │ docker push
              ▼
┌───────────────────────────┐
│       Docker Hub          │
│                           │
│ USERNAME/my-python-app:v1 │
│                           │
└───────────────────────────┘
```

---

# 🔄 Complete Experiment Flow

```text
Existing Docker Image
        │
        ▼
my-python-app:latest
        │
        │ docker login
        ▼
Docker Hub Authentication
        │
        │ docker tag
        ▼
USERNAME/my-python-app:v1
        │
        │ docker push
        ▼
Docker Hub Repository
        │
        ▼
Image Stored Online
```

---

# 🛠️ Technologies and Tools

| Technology / Tool | Purpose |
|---|---|
| 🐳 Docker Desktop | Local Docker environment |
| ☁️ Docker Hub | Remote Docker image registry |
| 💻 PowerShell | Execute Docker commands |
| 🪟 Windows | Host operating system |
| 🌐 Web Browser | Access and verify Docker Hub |

---

# 📋 Prerequisites

The following are required:

- Windows 10 or Windows 11
- Docker Desktop installed and running
- PowerShell
- Docker image `my-python-app` created during Experiment 1
- Docker Hub account
- Internet connection

### Important

The Python application is **not rebuilt in this experiment**.

The existing image:

```text
my-python-app
```

created during Experiment 1 is used directly.

The purpose of this experiment is to publish the existing image to Docker Hub.

---

# 📁 Project Structure

```text
exp3-docker/
│
├── README.md
│
└── screenshots/
    ├── docker login.png
    └── img on docker-hub.png
```

> Screenshots captured during the practical implementation are stored separately in the repository and are intentionally not embedded in this README.

---

# 🚀 Experiment Procedure

# PART 1 — Start Docker

## Step 1: Open Docker Desktop

Open the Windows Start Menu and launch Docker Desktop.

Wait until Docker Desktop has finished starting.

Docker Desktop provides the local Docker environment required to execute Docker commands.

---

## Verify Docker from PowerShell

Open PowerShell and run:

```powershell
docker --version
```

Example:

```text
Docker version 29.x.x
```

The exact version may vary depending on the installed Docker version.

A valid version confirms that the Docker CLI is available.

---

# 📦 PART 2 — Check the Existing Docker Image

## Step 2: Display Docker Images

The image `my-python-app` was created during Experiment 1.

Check whether it is available locally:

```powershell
docker images
```

Expected image:

```text
REPOSITORY      TAG
my-python-app   latest
```

The image must exist locally before it can be tagged and pushed.

### Important

Do **not** run:

```powershell
docker build
```

in this experiment.

The image already exists from Experiment 1.

---

# ☁️ PART 3 — Create or Use a Docker Hub Account

## Step 3: Open Docker Hub

Open a web browser and access Docker Hub.

Docker Hub is an online registry used to store and share Docker images.

A Docker Hub account is required to upload the image.

---

## Step 4: Sign Up or Sign In

If you do not already have a Docker Hub account, create one.

If you already have an account, sign in.

Your Docker Hub username will be used as part of the image name.

For example:

```text
USERNAME/my-python-app
```

Replace `USERNAME` with your actual Docker Hub username.

---

# 🔐 PART 4 — Login from PowerShell

## Step 5: Log in to Docker Hub

Return to PowerShell and run:

```powershell
docker login
```

Expected result:

```text
Login Succeeded
```

Docker authenticates the local Docker CLI with Docker Hub.

If Docker is already authenticated, a message similar to:

```text
Authenticating with existing credentials...
```

may appear before successful authentication.

---

# 🏷️ PART 5 — Understand the Docker Hub Image Name

## Step 6: Build the Docker Hub Image Name

Docker Hub images use the following naming format:

```text
USERNAME/my-python-app:v1
```

Where:

| Component | Meaning |
|---|---|
| `USERNAME` | Your Docker Hub username |
| `my-python-app` | Docker Hub repository name |
| `v1` | Image version tag |

### Example

```text
dheerajj1/my-python-app:v1
```

> Use your own Docker Hub username instead of the example username.

---

# 🏷️ PART 6 — Tag the Existing Docker Image

## Step 7: Tag the Local Image

Replace `USERNAME` with your Docker Hub username:

```powershell
docker tag my-python-app USERNAME/my-python-app:v1
```

### Important

`docker tag`:

- Does not rebuild the application.
- Does not create a separate image build.
- Gives the existing image another name.
- Adds a version tag.
- Connects the local image to the Docker Hub repository name.

---

# 🔎 Step 8: Verify the Image Tags

Run:

```powershell
docker images
```

Expected result:

```text
REPOSITORY                 TAG
my-python-app              latest
USERNAME/my-python-app     v1
```

Both names can refer to the same underlying Docker image.

The Image ID should be the same for both references.

---

# 🧩 Understanding Docker Image Tags

```text
                 Same Docker Image
                        │
              ┌─────────┴─────────┐
              │                   │
              ▼                   ▼
    my-python-app:latest    USERNAME/my-python-app:v1
```

Tagging creates another reference to the same underlying image.

It does not rebuild the application.

---

# 📤 PART 7 — Push the Image to Docker Hub

## Step 9: Push the Tagged Image

Replace `USERNAME` with your Docker Hub username:

```powershell
docker push USERNAME/my-python-app:v1
```

During the upload, Docker may display several image layers.

Example:

```text
The push refers to repository [docker.io/USERNAME/my-python-app]

...
v1: digest: sha256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
size: xxx
```

A successful push means that the image has been stored in Docker Hub.

---

# ☁️ Docker Push Process

```text
Local Computer
      │
      │
      ▼
my-python-app:latest
      │
      │ docker tag
      ▼
USERNAME/my-python-app:v1
      │
      │ docker push
      ▼
Docker Hub
      │
      ▼
USERNAME/my-python-app:v1
```

---

# 🔎 PART 8 — Verify the Image on Docker Hub

## Step 10: Open the Docker Hub Repository

Open Docker Hub in a web browser.

Sign in to your Docker Hub account.

Open the repository:

```text
my-python-app
```

The repository should belong to your Docker Hub account.

The uploaded tag should be visible:

```text
v1
```

---

# 🗂️ Repository Structure on Docker Hub

```text
Docker Hub
    │
    ▼
USERNAME
    │
    ▼
my-python-app
    │
    ▼
v1
```

The presence of the `v1` tag confirms that the image was successfully uploaded to the remote registry.

---

# 💻 Local Image vs Remote Image

After the push, the image exists in two locations:

```text
LOCAL COMPUTER
      │
      └── my-python-app:latest


DOCKER HUB
      │
      └── USERNAME/my-python-app:v1
```

### Local Image

The local image remains available on the student's computer.

### Remote Image

The Docker Hub copy is stored in the online registry and can later be downloaded by another Docker-enabled machine.

---

# 🔬 Build vs Tag vs Push

Understanding the difference between these commands is an important part of this experiment.

## `docker build`

```powershell
docker build -t my-python-app .
```

### Purpose

Creates a Docker image from the Dockerfile and project files.

```text
Dockerfile
    │
    ▼
docker build
    │
    ▼
CREATE IMAGE
```

---

## `docker tag`

```powershell
docker tag my-python-app USERNAME/my-python-app:v1
```

### Purpose

Gives the existing image another name and tag suitable for a Docker Hub repository.

```text
Existing Image
    │
    ▼
docker tag
    │
    ▼
REGISTRY IMAGE NAME
```

---

## `docker push`

```powershell
docker push USERNAME/my-python-app:v1
```

### Purpose

Uploads the tagged Docker image to Docker Hub.

```text
Tagged Image
    │
    ▼
docker push
    │
    ▼
DOCKER HUB
```

---

# 🧠 Key Difference

```text
docker build
      ↓
CREATE IMAGE
      ↓
docker tag
      ↓
GIVE IMAGE A REGISTRY NAME
      ↓
docker push
      ↓
UPLOAD IMAGE
```

Therefore:

| Command | Main Function |
|---|---|
| `docker build` | Creates the image |
| `docker tag` | Gives the image a registry-compatible name |
| `docker push` | Uploads the image to Docker Hub |

---

# 📦 Image Distribution Concept

The main purpose of pushing an image to Docker Hub is to make it available for use on another Docker-enabled machine.

```text
Computer A
    │
    │ docker push
    ▼
Docker Hub
    │
    │ docker pull
    ▼
Computer B
```

This creates a bridge between local containerization and deployment on another system.

---

# 🔄 Complete Experiment 3 Workflow

```text
┌──────────────────────────┐
│    Existing Docker      │
│         Image            │
│    my-python-app:latest  │
└─────────────┬────────────┘
              │
              ▼
        docker login
              │
              ▼
┌──────────────────────────┐
│   Docker Hub             │
│   Authentication         │
└─────────────┬────────────┘
              │
              ▼
         docker tag
              │
              ▼
┌──────────────────────────┐
│ USERNAME/my-python-app:v1│
└─────────────┬────────────┘
              │
              ▼
         docker push
              │
              ▼
┌──────────────────────────┐
│       Docker Hub         │
│                          │
│ USERNAME/my-python-app   │
│          :v1             │
└──────────────────────────┘
              │
              ▼
       Image Available
          Online
```

---

# 📊 Experiment Summary

| Parameter | Value |
|---|---|
| **Experiment Number** | 3 |
| **Experiment Title** | Push a Docker Image to Docker Hub |
| **Existing Docker Image** | `my-python-app` |
| **Local Tag** | `my-python-app:latest` |
| **Remote Repository Format** | `USERNAME/my-python-app` |
| **Image Version** | `v1` |
| **Remote Image Format** | `USERNAME/my-python-app:v1` |
| **Registry** | Docker Hub |
| **Authentication** | `docker login` |
| **Tagging Command** | `docker tag` |
| **Upload Command** | `docker push` |

---

# 🧪 Key Commands Used

| Command | Purpose |
|---|---|
| `docker --version` | Check Docker installation |
| `docker images` | Display existing Docker images |
| `docker login` | Authenticate with Docker Hub |
| `docker tag my-python-app USERNAME/my-python-app:v1` | Tag the existing image |
| `docker images` | Verify the new image tag |
| `docker push USERNAME/my-python-app:v1` | Push the image to Docker Hub |

---

# 💡 Important Concepts Demonstrated

## 1. Image Reusability

The experiment starts with the existing image:

```text
my-python-app
```

The image created in Experiment 1 is reused instead of being rebuilt.

---

## 2. Docker Hub

Docker Hub acts as a remote registry for Docker images.

It allows images to be:

- Stored online
- Shared
- Versioned using tags
- Retrieved by other Docker-enabled machines

---

## 3. Authentication

Before pushing an image, Docker must be authenticated with Docker Hub:

```powershell
docker login
```

Successful authentication produces:

```text
Login Succeeded
```

---

## 4. Image Tagging

The command:

```powershell
docker tag my-python-app USERNAME/my-python-app:v1
```

creates a Docker Hub-compatible reference for the existing image.

---

## 5. Image ID Consistency

After tagging:

```text
my-python-app:latest
```

and:

```text
USERNAME/my-python-app:v1
```

can refer to the same underlying Docker image.

The Image ID remains the same.

---

## 6. Image Upload

The command:

```powershell
docker push USERNAME/my-python-app:v1
```

uploads the image layers to Docker Hub.

---

## 7. Local and Remote Copies

After a successful push:

```text
LOCAL
my-python-app:latest

        +

REMOTE
USERNAME/my-python-app:v1
```

The local image remains on the computer while the tagged version is available remotely on Docker Hub.

---

# 🌐 Image Sharing and Deployment Concept

The Docker Hub repository can later be used by another Docker-enabled machine.

For example:

```text
Machine A
    │
    │ docker push
    ▼
Docker Hub
    │
    │ docker pull
    ▼
Machine B
```

Machine B can obtain the image using:

```powershell
docker pull USERNAME/my-python-app:v1
```

and then create a container from it.

---

# 📈 Experiment Progression

The three experiments demonstrate a progressive Docker workflow:

```text
EXPERIMENT 1
     │
     ▼
Create & Containerize
Python Flask Application
     │
     ▼
my-python-app
     │
     │
     ▼
EXPERIMENT 2
     │
     ▼
Run, Test & Manage
Docker Container
     │
     ▼
test-python-container
     │
     │
     ▼
EXPERIMENT 3
     │
     ▼
Tag & Push Image
     │
     ▼
Docker Hub
     │
     ▼
USERNAME/my-python-app:v1
```

---

# ✅ Result

The existing Docker image:

```text
my-python-app
```

was successfully authenticated, tagged using the Docker Hub repository naming format, and pushed to Docker Hub.

The image was tagged as:

```text
USERNAME/my-python-app:v1
```

The uploaded repository and `v1` tag were verified on Docker Hub.

The experiment successfully demonstrated the complete process:

```text
Local Image
    ↓
Docker Login
    ↓
Image Tagging
    ↓
Docker Push
    ↓
Docker Hub
    ↓
Online Image
```

---

# 🎓 Conclusion

This experiment provided practical understanding of how a locally created Docker image can be distributed through **Docker Hub**.

The existing `my-python-app` image from Experiment 1 was reused without rebuilding the application. Docker authentication was performed using `docker login`, after which the image was given a Docker Hub-compatible repository name and version tag using `docker tag`.

The tagged image was then uploaded to Docker Hub using `docker push` and verified through the Docker Hub web interface.

The experiment demonstrates the transition from **local containerization to image distribution**, allowing the same Docker image to be obtained and used on another Docker-enabled machine.

The complete concept can be summarized as:

```text
Create Image
     ↓
Login
     ↓
Tag
     ↓
Push
     ↓
Docker Hub
     ↓
Share / Pull
```

---

# 📚 Repository Contents

```text
.
├── README.md
│
└── screenshots/
    ├── docker login.png
    └── img on docker-hub.png
```

---

<p align="center">

<b>🐳 Docker · ☁️ Docker Hub · 📦 Container Images</b>

</p>

<p align="center">
Cloud Computing Laboratory — Experiment 3
</p>

<p align="center">
<i>Push a Docker Image to Docker Hub</i>
</p>
