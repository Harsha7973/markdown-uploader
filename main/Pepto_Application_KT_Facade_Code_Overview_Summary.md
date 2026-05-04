Source tag : 
      
Note : This extracted file is generated from SharePoint or Wiki content. If the source document contains images, charts, or graphical elements, they may not be fully converted into Markdown format. For complete clarity, please refer to the original source using the source tag provided above.

# Pepto Application KT Facade Code Overview Summary

## Overview
This KT provides a high-level walkthrough of the Facade application codebase, explaining folder structure, request handling, configuration, and deployment integration.

## Purpose of Facade
- Handles legacy devices sending non-JSON payloads (TXT/XML).
- Converts incoming data to JSON format.
- Forwards normalized requests to PDS.

## Technology Stack
- Language: Node.js (Node 20.x)
- Framework: Express
- Logging: OpenSearch
- Platform: Kubernetes

## Code Structure
- **package.json**:
  - Manages dependencies and Node version.
- **app.js**:
  - Application entry point.
  - Initializes routes and middleware.
- **routes/**:
  - Defines endpoint-specific request handling.
  - Converts payloads into JSON.
- **helper functions**:
  - Common validation, transformation, and routing logic.

## Request Flow
1. Request reaches Facade endpoint.
2. Payload is validated and transformed.
3. Logging is pushed to OpenSearch.
4. Request is forwarded to PDS.

## Local Code Understanding
- Recommended to clone repos locally.
- Use VS Code + Copilot for faster code comprehension.
- Copilot helps explain endpoint logic without manual deep dives.

## Docker Integration
- Facade code repo is imported into Facade KS Docker repo.
- Dockerfile defines base image, copy steps, and run commands.
- Correct commit ID must be used to avoid code-image mismatch.

## Configuration Overview
- Default configs exist in Docker repo.
- Environment-specific configs are managed in KS Config repo.
- Key configs include:
  - Log level
  - OpenSearch group and stack
  - Resource limits (CPU, memory)
  - Autoscaling thresholds

## Kubernetes Deployment
- Separate stacks: Dev, ITG, Prod (plus Pi and Stage for Facade).
- Minimum and maximum replica counts enforced.
- Autoscaling based on CPU and memory utilization.

## Ownership Model
- Platform-owned repos: Kubernetes infra and cluster configs.
- Pepto-owned repos: application, Docker, and app-level configs.
- Platform approval required for infra changes.

## Outcome
This KT gives engineers a clear architectural and code-level understanding of the Facade application, enabling efficient debugging, configuration updates, and safe deployments.