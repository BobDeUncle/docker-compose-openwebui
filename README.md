# OpenWebUI Docker Setup

This repository contains a Docker Compose configuration for running [OpenWebUI](https://github.com/open-webui/open-webui) - a web-based user interface for Ollama with CUDA support.

## Overview

OpenWebUI provides a user-friendly interface for interacting with Ollama, making it easier to manage and use large language models (LLMs) running locally via Ollama. This configuration includes GPU support via CUDA and automatic updates through Watchtower.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/)
- An existing Ollama instance running on the same Docker network
- NVIDIA GPU with appropriate drivers installed
- Docker configured with NVIDIA Container Toolkit

### Ollama

If you need to set up Ollama itself, check out our companion repository:
- [Docker Compose Ollama](https://github.com/BobDeUncle/docker-compose-ollama) - A complete Docker setup for running Ollama with automatic updates via Watchtower
 
This WebUI container is designed to work seamlessly with the Ollama instance from the above repository. Simply ensure that the `OLLAMA_API_BASE_URL` environment variable points to your running Ollama instance.

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/BobDeUncle/docker-compose-openwebui.git
   cd docker-compose-openwebui
   ```

2. Make sure you have a Docker network named `llm-network-compose` created:
   ```bash
   docker network create llm-network-compose
   ```

3. Start the containers:
   ```bash
   docker compose up -d
   ```

4. Verify installation:
   ```bash
   docker ps
   ```
   You should see the OpenWebUI and Watchtower containers running.

## Usage

### Accessing OpenWebUI

OpenWebUI is accessible via a web browser at:
```
http://localhost:8181
```

The interface allows you to:
- Chat with available models
- Manage and download models
- Customize model parameters
- Create and share prompts
- Review chat history

## Configuration

### Customize the `docker-compose.yml`

- **Port**: The default port is 8181. Change `8181:8080` if you need a different port mapping.
- **Ollama API URL**: The `OLLAMA_API_BASE_URL` environment variable points to your Ollama instance at `http://ollama:11434`. Update this URL to match your Ollama server's address.
- **GPU Support**: The configuration includes NVIDIA GPU support. Remove or modify the device reservations if not using a GPU.
- **Watchtower**: The included Watchtower container will automatically update the OpenWebUI container every 15 minutes.
- **Restart Policy**: By default, the containers will restart automatically unless manually stopped.

## Maintenance

### Updating

The included Watchtower container will automatically check for updates to the OpenWebUI image every 15 minutes and update it if a new version is available.

If you want to manually update:

```bash
docker compose pull
docker compose up -d
```

## Volumes

The configuration creates a persistent volume named `open-webui` to store your application data, including chat history and settings.

## Networks

This setup requires an external Docker network named `llm-network-compose`. Make sure your Ollama instance is also connected to this network for proper communication.

## Troubleshooting

- If you can't connect to OpenWebUI, verify that the Ollama API URL is correct and that your Ollama instance is running
- Check container logs for any errors: `docker logs openwebui`
- Ensure that your network allows connections between the OpenWebUI container and Ollama
- For GPU-related issues, verify your NVIDIA drivers and Docker NVIDIA toolkit configuration

## License

OpenWebUI is an open-source project. For licensing information, visit the [OpenWebUI GitHub repository](https://github.com/open-webui/open-webui).

## Additional Resources

- [OpenWebUI GitHub Repository](https://github.com/open-webui/open-webui)
- [Ollama Documentation](https://github.com/ollama/ollama/tree/main/docs)
- [Ollama Models Library](https://ollama.ai/library)
- [NVIDIA Container Toolkit Documentation](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)
- [Docker Documentation](https://docs.docker.com/)