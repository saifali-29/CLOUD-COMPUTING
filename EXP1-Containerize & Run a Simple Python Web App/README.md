# 🐳 Containerize and Run a Simple Python Web Application

<p align="center">

![Docker](https://img.shields.io/badge/Docker-Containerization-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-Web%20Application-000000?style=for-the-badge&logo=flask&logoColor=white)
![Windows](https://img.shields.io/badge/Platform-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)

</p>

<p align="center">
  <b>Cloud Computing Laboratory — Experiment 1</b>
</p>

<p align="center">
  Containerizing and running a simple Python Flask web application using Docker.
</p>

---

## 📌 Experiment Overview

This experiment demonstrates the fundamental process of **containerizing a Python Flask web application using Docker**.

A simple Flask application is created and its required dependency is defined using `requirements.txt`. A `Dockerfile` is then used to create a Docker image containing the application and its runtime environment.

The Docker image is used to create and run a container. The application is exposed through **port 5000** and accessed from a web browser using:

```text
http://localhost:5000
