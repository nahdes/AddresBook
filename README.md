# 🔄 Jenkins CI/CD Pipeline — Automated Address Book Deployment

## 🎯 Overview
**Address Book CI/CD Pipeline** is a declarative Groovy-based Jenkins workflow that automates the full lifecycle of a Vaadin-powered contact management app—from Git checkout to Dockerized deployment. This pipeline ensures reliable builds, secure image pushes to Docker Hub, and instant runtime spins on port 4000, streamlining DevOps for Java-based web apps.
---
## 🧭 Pipeline Objectives
- ✅ **Automate SCM Integration** for seamless main-branch pulls from GitHub
- ✅ **Optimize Builds** with Maven packaging (tests skipped for CI velocity) and artifact management
- ✅ **Secure Containerization** via tagged Docker builds and credential-protected Hub pushes
- ✅ **Enable Zero-Downtime Runs** by force-removing old containers and launching fresh ones detached
- ✅ **Enhance Monitoring** through conditional post-actions for success/failure logging and build retention
---
## 📊 Pipeline Features
- 📂 **Agent & Tools Setup**: Runs on any agent with Maven tool ('Maven') pre-configured for reproducible builds
- 🗑️ **Build Cleanup**: Rotates logs after 30 days, keeping only the latest 1 for efficiency
- 🔐 **Credential Handling**: Loads Docker Hub creds (ID '1') as env vars for stdin login without exposure
- 🔄 **Multi-Stage Orchestration**: Checkout → Build → Docker Build → Push → Run, with shell steps for cross-platform compatibility
- 📝 **Post-Execution Hooks**: Always echoes completion; celebrates success or flags failures for quick triage
- 🎨 Built with **Groovy + Jenkins Declarative Syntax** for readable, maintainable pipelines—trigger-ready for webhooks or polls
---
