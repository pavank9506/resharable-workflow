# Reusable Build and Deploy Workflow

A flexible, multi-language GitHub Actions workflow that supports both **Python** and **Node.js** applications. This workflow automates testing, Docker image building, security scanning, and image signing.

## Features

✅ **Multi-Language Support** - Python and Node.js  
✅ **Automated Testing** - Unit and integration tests with coverage reporting  
✅ **Docker Build & Push** - Automated Docker image creation and registry push  
✅ **Security Scanning** - Trivy vulnerability scanning and SBOM generation  
✅ **Image Signing** - Cosign-based image signing for supply chain security  
✅ **Reusable Workflow** - Call from multiple repositories with different configurations  
✅ **Coverage Reports** - HTML and XML coverage reports (Python only)  

## Prerequisites

- GitHub repository with source code
- Dockerfile in the repository root
- `requirements.txt` (Python) or `package.json` (Node.js)
- Docker Hub account (for pushing images)
- GitHub secrets configured (see below)

## GitHub Secrets Required

Add these secrets to your repository (Settings → Secrets and variables → Actions):

| Secret | Description |
|--------|-------------|
| `DOCKER_USERNAME` | Docker Hub username |
| `DOCKER_PASSWORD` | Docker Hub access token or password |

## Usage

### 1. For Python Projects

Create `.github/workflows/python-build.yml`:

````yaml
name: Python Build and Deploy

on:
  push:
    branches:
      - main

permissions:
  contents: read
  id-token: write
  security-events: write

jobs:
  build:
    uses: pavank9506/resharable-workflow/.github/workflows/test-buld.yaml@main
    with:
      app_language: 'python'
      docker_image_name: 'your-username/your-python-app'
      docker_image_tag: '1.0.0'
    secrets:
      DOCKER_USERNAME: ${{ secrets.DOCKER_USERNAME }}
      DOCKER_PASSWORD: ${{ secrets.DOCKER_PASSWORD }}
````