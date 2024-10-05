# DevContainer Configuration for GitHub Codespaces
This repository contains one (hopefully more to come) configuration file to set up a development environment for GitHub Codespaces using devcontainers. Currently, it consists of a base Linux image with Conda installed and the necessary extensions to work with Python, Pylance, and GitHub Copilot. The container also listens on port 8080 for testing purposes.

## Setting Up the DevContainer
To use this configuration in your project, follow these steps:

Create the .devcontainer directory and inside the .devcontainer directory, create a file named devcontainer.json with the following content:

```dir
├── .devcontainer
│   ├── devcontainer.json
├── main.py
├── ...
```


```json
{
    "name": "Conda Environment with Python and GitHub Copilot",
    "image": "mcr.microsoft.com/vscode/devcontainers/base",
    "postCreateCommand": "conda init",
    "customizations": {
      "vscode": {
        "extensions": [
          "ms-python.python",
          "ms-python.vscode-pylance",
          "github.copilot"
        ],
        "settings": {
          "python.defaultInterpreterPath": "/opt/conda/bin/python",
          "python.linting.enabled": true,
          "python.linting.pylintEnabled": true,
          "python.formatting.provider": "black",
          "editor.formatOnSave": true
        }
      }
    },
    "features": {
      "ghcr.io/devcontainers/features/conda:1": {}
    },
    "forwardPorts": [
      8080
    ]
  }
```

Explanation of the devcontainer.json:
- name: The name of the devcontainer environment.
- image: The base image is a Linux environment.
- postCreateCommand: The command __conda init__ will be runned after the container is created, setting up Conda for environment management.
- customizations: This section lists the Visual Studio Code extensions to be installed automatically and some settings:
    - ms-python.python: Python extension.
    - ms-python.vscode-pylance: Pylance for better Python IntelliSense and type checking.
    - GitHub.copilot: GitHub Copilot for AI-assisted coding.
    - python.defaultInterpreterPath: Uses the Conda-installed Python interpreter.
    - python.linting.enabled & python.linting.pylintEnabled: Enables code linting with Pylint.
    - python.formatting.provider: Formats code with Black.
    - editor.formatOnSave: Auto-formats code on save.
- features: Includes Conda installation.
- forwardPorts: Port 8080 is forwarded, which is useful if you are testing applications locally.

## Additional Notes
You can customize this devcontainer.json as needed, such as adding more extensions, changing the base image, or configuring additional ports.
Once you have created the .devcontainer directory and the devcontainer.json file, you can rebuild the Github Codespace. The devcontainer setup will automatically build and configure the development environment for you.

Happy Coding!