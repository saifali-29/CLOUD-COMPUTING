# 🐳 Run, Test and Manage a Docker Container

<p align="center">

<img src="https://img.shields.io/badge/Docker-Container%20Management-2496ED?style=for-the-badge&logo=docker&logoColor=white" />
<img src="https://img.shields.io/badge/Cloud%20Computing-Laboratory-6C63FF?style=for-the-badge" />
<img src="https://img.shields.io/badge/Platform-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white" />
<img src="https://img.shields.io/badge/PowerShell-Command%20Line-5391FE?style=for-the-badge&logo=powershell&logoColor=white" />

</p>

<p align="center">
  <b>Cloud Computing Laboratory — Experiment 2</b>
</p>

<p align="center">
  <i>Run, Test and Manage a Docker Container</i>
</p>

---

## 📌 Experiment Overview

This experiment focuses on the practical management of a Docker container using an **existing Docker image**.

The Docker image `my-python-app`, created during Experiment 1, is reused without rebuilding it. A new container named `test-python-container` is created from the existing image.

The experiment demonstrates the complete Docker container lifecycle, including:

- Checking Docker availability
- Checking an existing Docker image
- Creating and running a container
- Publishing and mapping ports
- Checking the running state of a container
- Testing the application through a browser
- Testing the application using PowerShell
- Viewing container logs
- Inspecting container configuration
- Entering a running container
- Exploring files and directories inside the container
- Exiting the container shell
- Stopping the container
- Viewing stopped containers
- Starting the same container again
- Comparing container identity
- Removing the container
- Confirming that the Docker image remains available

---

# 🎯 Objectives

The primary objectives of this experiment are:

1. To use an existing Docker image to create a container.
2. To check whether a Docker container is running.
3. To test the application running inside the container.
4. To understand Docker port mapping.
5. To view container logs.
6. To inspect container information and configuration.
7. To enter and explore a running container.
8. To stop and restart an existing container.
9. To understand the difference between stopping and removing a container.
10. To remove a container while retaining the Docker image.
11. To understand the basic Docker container lifecycle.

---

# 🧠 Learning Outcomes

After completing this experiment, the following concepts are demonstrated:

| Concept | Description |
|---|---|
| 🐳 Docker Image | Reusable template from which containers are created |
| 📦 Docker Container | Instance created from a Docker image |
| ▶️ `docker run` | Creates and starts a new container |
| 🔍 `docker ps` | Displays currently running containers |
| 🌐 Port Mapping | Connects a host port to a container port |
| 🧪 Application Testing | Verifies that the application responds correctly |
| 📜 Docker Logs | Displays application output and requests |
| 🔎 Docker Inspect | Displays detailed container information |
| 💻 Docker Exec | Executes commands inside a running container |
| ⏹️ Docker Stop | Stops a running container |
| ▶️ Docker Start | Starts an existing stopped container |
| 🗑️ Docker Remove | Removes a container |
| 🔄 Container Lifecycle | Run → Test → Inspect → Enter → Stop → Start → Remove |

---

# 🏗️ Experiment Architecture

```text
                 Existing Docker Image
                       │
                       ▼
                 my-python-app
                       │
                       │ docker run
                       ▼
              test-python-container
                       │
                       │
            ┌──────────┼───────────┐
            │          │           │
            ▼          ▼           ▼
        docker ps   docker logs  docker inspect
            │
            ▼
      Application Testing
            │
            ▼
     http://localhost:5001
            │
            ▼
      Host Port 5001
            │
            ▼
   Container Port 5000
            │
            ▼
     Flask Application
```

---

# 🔄 Complete Experiment Workflow

```text
Existing Docker Image
        │
        ▼
  my-python-app
        │
        ▼
    docker run
        │
        ▼
test-python-container
        │
        ▼
    docker ps
        │
        ▼
 Test Application
        │
        ▼
 localhost:5001
        │
        ▼
    docker logs
        │
        ▼
   docker inspect
        │
        ▼
     docker exec
        │
        ▼
 Enter Container
        │
        ▼
    docker stop
        │
        ▼
 Stopped Container
        │
        ▼
    docker start
        │
        ▼
 Running Container
        │
        ▼
     docker rm
        │
        ▼
 Container Removed
```

---

# 🛠️ Technologies and Tools

| Technology / Tool | Purpose |
|---|---|
| 🐳 Docker Desktop | Provides the Docker environment |
| 💻 PowerShell | Used to execute Docker commands |
| 🐍 Python / Flask | Application running inside the container |
| 📦 Docker Image | Source template for creating the container |
| 🌐 Web Browser | Used to test the application |
| 🪟 Windows | Host operating system |

---

# 📋 Prerequisites

The following are required:

- Docker Desktop installed and running
- Windows PowerShell
- Docker image `my-python-app` created during Experiment 1
- A web browser

### Important

The Docker image is **not rebuilt in this experiment**.

The existing image:

```text
my-python-app
```

created during Experiment 1 is reused to create a new container.

An internet connection is not required when the image already exists locally.

---

# 📁 Project Structure

```text
exp2-docker/
│
├── README.md
│
└── screenshots/
    ├── intro.png
    ├── name image.png
    ├── run.png
    ├── inspect.png
    ├── Ports and networks.png
    ├── container logs.png
    ├── explore container.png
    ├── stopped container.png
    ├── last.png
    └── ...
```

> Screenshots captured during the practical implementation are stored separately in the repository and are not embedded in this README.

---

# 🚀 Experiment Procedure

## PART 1 — Start Docker

### Step 1: Open Docker Desktop

Open the Windows Start Menu and launch Docker Desktop.

Wait until Docker Desktop has finished starting.

Docker Desktop provides the Docker environment required for creating and managing containers.

---

### Verify Docker from PowerShell

Open PowerShell and run:

```powershell
docker --version
```

Example:

```text
Docker version 29.x.x
```

The exact version may differ depending on the installed Docker version.

---

# 📦 PART 2 — Check the Existing Docker Image

## Step 2: Display Docker Images

The image `my-python-app` was created during Experiment 1.

Check whether it is still available locally:

```powershell
docker images
```

Expected image:

```text
REPOSITORY
my-python-app
```

The important point is that the image is **reused** rather than rebuilt.

### Image Concept

```text
Docker Image
my-python-app
       │
       ├──────────► Container 1
       │
       ├──────────► Container 2
       │
       └──────────► Container 3
```

A Docker image acts as a reusable template from which multiple containers can be created.

---

# 🚀 PART 3 — Create and Run a New Container

## Step 3: Create and Run the Container

Run:

```powershell
docker run -d -p 5001:5000 --name test-python-container my-python-app
```

### Command Breakdown

| Option | Purpose |
|---|---|
| `docker run` | Creates and starts a new container |
| `-d` | Runs the container in the background |
| `-p 5001:5000` | Maps host port 5001 to container port 5000 |
| `--name test-python-container` | Assigns the container name |
| `my-python-app` | Existing Docker image used to create the container |

The new container is named:

```text
test-python-container
```

---

# 🔌 Port Mapping

This experiment uses host port `5001` instead of port `5000` used in Experiment 1.

```text
Windows Host
Port 5001
     │
     ▼
Docker Container
Port 5000
     │
     ▼
Flask Application
```

The mapping is:

```text
5001 : 5000
```

Therefore, the application can be accessed through:

```text
http://localhost:5001
```

---

# 🔍 PART 4 — Check the Running Container

## Step 4: Use `docker ps`

Display currently running containers:

```powershell
docker ps
```

Expected information includes:

```text
CONTAINER ID
IMAGE
STATUS
PORTS
```

Example:

```text
CONTAINER ID   IMAGE          STATUS       PORTS
xxxxxxxx       my-python-app  Up ...       0.0.0.0:5001->5000/tcp
```

### Important Points

- `docker ps` displays only running containers.
- `my-python-app` is the image used by the container.
- `test-python-container` is the container created in this experiment.
- `Up` indicates that the container is currently running.

---

# 🌐 PART 5 — Test the Application

## Step 5: Open the Application in a Browser

Open Google Chrome, Microsoft Edge, or another web browser.

Enter:

```text
http://localhost:5001
```

Expected response:

```text
Hello! My first Docker application is running.
```

### Request Flow

```text
Browser
   │
   ▼
localhost:5001
   │
   ▼
Windows Host
   │
   ▼
Docker Port Mapping
   │
   ▼
Container Port 5000
   │
   ▼
Flask Application
   │
   ▼
Response
   │
   ▼
Browser
```

The browser sends a request to host port `5001`, and Docker forwards the request to port `5000` inside the container.

---

# 💻 PART 6 — Test the Container Using PowerShell

## Step 6: Test Without Opening a Browser

PowerShell can send an HTTP request directly to the application.

Run:

```powershell
Invoke-WebRequest http://localhost:5001
```

To display only the returned content:

```powershell
(Invoke-WebRequest http://localhost:5001).Content
```

Expected result:

```text
Hello! My first Docker application is running.
```

This confirms that the application responds to an HTTP request without requiring a browser.

---

# 📜 PART 7 — View Container Logs

## Step 7: Display Logs

View messages generated by the application:

```powershell
docker logs test-python-container
```

Typical Flask output may include:

```text
Running on all addresses (0.0.0.0)
Running on http://127.0.0.1:5000
Running on http://172.x.x.x:5000
GET / HTTP/1.1
```

### Why Logs Matter

Container logs can show:

- Whether the Flask application started correctly
- Requests received by the application
- Application startup information
- Runtime problems

Logs are particularly useful when a container starts but the application does not behave as expected.

---

# 🔎 PART 8 — Inspect the Container

## Step 8: Display Container Information

Run:

```powershell
docker inspect test-python-container
```

The command provides detailed information about the container.

Important sections include:

```text
Name
Image
State
Ports
Network
```

### Why Use `docker inspect`?

`docker inspect` is useful for troubleshooting because it provides detailed metadata and configuration information about the container.

You do not need to understand every field returned by the command.

---

# 💻 PART 9 — Enter the Running Container

## Step 9: Open a Shell Inside the Container

Run:

```powershell
docker exec -it test-python-container /bin/sh
```

Expected prompt:

```text
/app #
```

### Command Breakdown

| Option | Purpose |
|---|---|
| `docker exec` | Executes a command inside a running container |
| `-i` | Keeps the input stream open |
| `-t` | Allocates an interactive terminal |
| `/bin/sh` | Opens a shell inside the container |

The prompt changes because the terminal session is now running inside the Docker container.

---

# 📂 PART 10 — Explore the Container

## Step 10: List Files Inside the Container

While inside the container, run:

```sh
ls
```

Expected files:

```text
app.py
requirements.txt
```

These files exist inside the container because they were copied into the Docker image during the image build process.

---

## Step 11: Check the Current Working Directory

Run:

```sh
pwd
```

Expected result:

```text
/app
```

The working directory is `/app` because the Dockerfile contains:

```dockerfile
WORKDIR /app
```

Therefore, Docker starts commands from this directory.

---

# 🚪 PART 11 — Exit the Container Shell

## Step 12: Exit the Shell

Run:

```sh
exit
```

This returns to PowerShell on the Windows host.

Example:

```text
PS C:\Users\Admin>
```

### Important

The `exit` command:

- Closes the interactive shell
- Does not delete the container
- Does not remove the container
- Does not necessarily stop the container

The container can continue running after the shell session is closed.

Check it using:

```powershell
docker ps
```

The container should still be listed as running.

---

# ⏹️ PART 12 — Stop the Container

## Step 13: Stop the Running Container

Run:

```powershell
docker stop test-python-container
```

Then check running containers:

```powershell
docker ps
```

The container will no longer appear because it is stopped.

### Important Difference

Stopping a container does **not** remove it.

The container still exists and can be started again later.

---

# 📋 PART 13 — Check Stopped Containers

## Step 14: Display All Containers

Use:

```powershell
docker ps -a
```

This displays both running and stopped containers.

Example:

```text
CONTAINER ID   IMAGE          STATUS
xxxxxxxx       my-python-app  Exited ...
```

### Difference Between `docker ps` and `docker ps -a`

| Command | Displays |
|---|---|
| `docker ps` | Running containers only |
| `docker ps -a` | Running and stopped containers |

This allows a stopped container to be found even after it is no longer running.

---

# ▶️ PART 14 — Start the Same Container Again

## Step 15: Start the Existing Container

Start the stopped container:

```powershell
docker start test-python-container
```

Check the running container:

```powershell
docker ps
```

Expected status:

```text
Up ...
```

The application becomes available again on:

```text
http://localhost:5001
```

---

## Container Lifecycle

```text
Container
    │
    ▼
  STOP
    │
    ▼
Stopped Container
    │
    ▼
  START
    │
    ▼
Running Container
```

### Important

`docker start` starts the **existing container**.

It does not create a new container.

---

# 🆔 PART 15 — Check the Container ID

## Step 16: Compare the Container ID

Run:

```powershell
docker ps
```

Compare the container ID with the ID observed when the container was first created.

The same container ID remains associated with:

```text
test-python-container
```

This demonstrates that:

```text
docker start
```

does not create a new container.

It starts the existing stopped container.

---

# 🗑️ PART 16 — Remove the Container

## Step 17: Stop and Remove the Container

Before removing the container, stop it if it is running:

```powershell
docker stop test-python-container
```

Then remove it:

```powershell
docker rm test-python-container
```

Verify the removal:

```powershell
docker ps -a
```

The removed container should no longer appear.

---

# 📦 PART 17 — Confirm the Docker Image Still Exists

## Step 18: Check the Docker Image

Run:

```powershell
docker images
```

The image:

```text
my-python-app
```

should still be available.

### Important Concept

Removing a container does **not** remove the image used to create it.

```text
Docker Image
my-python-app
       │
       ├──────► Container
       │
       ├──────► Container
       │
       └──────► Container
```

The same image can be reused to create new containers later.

---

# 🧩 Image vs Container

| Docker Image | Docker Container |
|---|---|
| Reusable template | Instance created from an image |
| Exists independently | Created from an image |
| Used to create containers | Runs the application |
| Can create multiple containers | Represents one container instance |
| Example: `my-python-app` | Example: `test-python-container` |

### Relationship

```text
Docker Image
my-python-app
      │
      │ docker run
      ▼
Docker Container
test-python-container
```

---

# 🔄 Container Lifecycle

The complete lifecycle demonstrated in this experiment is:

```text
                 ┌───────────────┐
                 │ Docker Image  │
                 │ my-python-app │
                 └───────┬───────┘
                         │
                    docker run
                         │
                         ▼
                 ┌───────────────┐
                 │    Running    │
                 │   Container   │
                 └───────┬───────┘
                         │
                    docker stop
                         │
                         ▼
                 ┌───────────────┐
                 │    Stopped    │
                 │   Container   │
                 └───────┬───────┘
                         │
                    docker start
                         │
                         ▼
                 ┌───────────────┐
                 │    Running    │
                 │   Container   │
                 └───────┬───────┘
                         │
                     docker rm
                         │
                         ▼
                 ┌───────────────┐
                 │    Removed    │
                 │   Container   │
                 └───────────────┘

                 Docker Image
                 remains available
```

---

# 📊 Experiment Summary

| Parameter | Value |
|---|---|
| **Experiment Number** | 2 |
| **Experiment Title** | Run, Test and Manage a Docker Container |
| **Existing Image** | `my-python-app` |
| **Container Name** | `test-python-container` |
| **Host Port** | `5001` |
| **Container Port** | `5000` |
| **Port Mapping** | `5001:5000` |
| **Application URL** | `http://localhost:5001` |
| **Container Shell** | `/bin/sh` |
| **Working Directory** | `/app` |
| **Application** | Python Flask Web Application |

---

# 🧪 Key Commands Used

| Command | Purpose |
|---|---|
| `docker --version` | Check Docker availability |
| `docker images` | List Docker images |
| `docker run -d -p 5001:5000 --name test-python-container my-python-app` | Create and run the container |
| `docker ps` | Display running containers |
| `Invoke-WebRequest http://localhost:5001` | Test the application using PowerShell |
| `(Invoke-WebRequest http://localhost:5001).Content` | Display HTTP response content |
| `docker logs test-python-container` | Display container logs |
| `docker inspect test-python-container` | Display detailed container information |
| `docker exec -it test-python-container /bin/sh` | Enter the running container |
| `ls` | List files inside the container |
| `pwd` | Display current working directory |
| `exit` | Exit the container shell |
| `docker stop test-python-container` | Stop the container |
| `docker ps -a` | Display all containers |
| `docker start test-python-container` | Start the existing stopped container |
| `docker rm test-python-container` | Remove the container |
| `docker images` | Confirm the image remains available |

---

# 📈 Overall Experiment Flow

```text
┌─────────────────────────┐
│ Existing Docker Image   │
│     my-python-app       │
└────────────┬────────────┘
             │
             │ docker run
             ▼
┌─────────────────────────┐
│      Container          │
│ test-python-container   │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│     Port Mapping        │
│    5001 : 5000          │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│    Application Test     │
│  localhost:5001         │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│       Inspection        │
│ logs / inspect / exec   │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│    Container Stop       │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│    Container Start      │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│   Container Removal     │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│ Docker Image Remains    │
│     my-python-app       │
└─────────────────────────┘
```

---

# 💡 Important Concepts Demonstrated

## 1. Image Reusability

The experiment begins with the existing image:

```text
my-python-app
```

The image is not rebuilt.

This demonstrates that Docker images are reusable templates.

---

## 2. Container Creation

A new container is created using:

```powershell
docker run -d -p 5001:5000 --name test-python-container my-python-app
```

The container receives its own identity and configuration.

---

## 3. Port Publishing

The application inside the container listens on port `5000`.

Docker publishes it on host port `5001`:

```text
5001 → 5000
```

Therefore:

```text
http://localhost:5001
```

can be used to access the application.

---

## 4. Container Inspection

The command:

```powershell
docker inspect test-python-container
```

provides detailed information about:

- Name
- Image
- State
- Ports
- Network
- Configuration

---

## 5. Entering a Container

The command:

```powershell
docker exec -it test-python-container /bin/sh
```

opens an interactive shell inside the running container.

This demonstrates that the application files and runtime environment are available inside the container.

---

## 6. Stop vs Start

Stopping:

```powershell
docker stop test-python-container
```

changes the container from running to stopped.

Starting:

```powershell
docker start test-python-container
```

starts the **same container again**.

It does not create a new container.

---

## 7. Stop vs Remove

### Stop

```powershell
docker stop test-python-container
```

The container still exists.

### Remove

```powershell
docker rm test-python-container
```

The container is removed.

The Docker image remains available.

---

# ✅ Result

The existing Docker image `my-python-app` was successfully used to create and run a new container named:

```text
test-python-container
```

The application was successfully tested using:

```text
http://localhost:5001
```

and through PowerShell using:

```powershell
Invoke-WebRequest http://localhost:5001
```

The experiment also demonstrated:

- Container status checking
- Application testing
- Port mapping
- Container logs
- Container inspection
- Interactive shell access
- File and directory exploration
- Container stopping
- Container restarting
- Container ID verification
- Container removal
- Docker image reuse

After the container was removed, the Docker image:

```text
my-python-app
```

remained available for creating containers again.

---

# 🎓 Conclusion

This experiment provided practical understanding of the **Docker container lifecycle and container management operations**.

Instead of rebuilding the application image, the existing `my-python-app` image was reused to create a new container. The container was tested through both a web browser and PowerShell, while Docker commands were used to view logs, inspect configuration, and enter the container environment.

The experiment further demonstrated the difference between stopping, starting, and removing a container. The same container could be stopped and restarted while retaining its identity, whereas removing the container deleted the container itself while leaving the original Docker image available for reuse.

The complete concept can be summarized as:

```text
Existing Image
      ↓
Create Container
      ↓
Run
      ↓
Test
      ↓
Inspect
      ↓
Enter
      ↓
Stop
      ↓
Start
      ↓
Remove
      ↓
Image Remains
```

---

# 📚 Repository Contents

```text
.
├── README.md
│
└── screenshots/
    ├── container logs.png
    ├── explore container.png
    ├── inspect.png
    ├── intro.png
    ├── last.png
    ├── name image(1).png
    ├── Ports and networks.png
    └── stopped container.png
```

---

<p align="center">

<b>🐳 Docker · 📦 Containers · 🌐 Flask · ☁️ Cloud Computing</b>

</p>

<p align="center">
Cloud Computing Laboratory — Experiment 2
</p>

<p align="center">
<i>Run, Test and Manage a Docker Container</i>
</p>
