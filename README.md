# Welcome to my-insecure-repo

This repository contains example projects with intentionally vulnerable dependencies to demonstrate Dependabot security alerts.

## Project Structure

- **nodejs-app/** - Node.js application with vulnerable npm packages
- **python-service/** - Python service with vulnerable pip packages
- **ruby-webapp/** - Ruby web application with vulnerable gems
- **java-api/** - Java API with vulnerable Maven dependencies
- **golang-microservice/** - Go microservice with vulnerable Go modules

## Dependabot Configuration

Dependabot is configured in `.github/dependabot.yml` to automatically check for dependency updates across all ecosystems:

- npm (Monday)
- pip (Tuesday)  
- bundler (Wednesday)
- maven (Thursday)
- gomod (Friday)

Dependabot will automatically open pull requests to update vulnerable dependencies when new versions are available.
