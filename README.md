<!--
  ~ Copyright (c) 2023-2024 Datalayer, Inc.
  ~
  ~ BSD 3-Clause License
-->

[![Datalayer](https://assets.datalayer.tech/datalayer-25.svg)](https://datalayer.io)

[![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=1ABC9C)](https://github.com/sponsors/datalayer)

# 🪐 ✨ Jupyter AI Agent

[![Github Actions Status](https://github.com/datalayer/jupyter-ai-agents/workflows/Build/badge.svg)](https://github.com/datalayer/jupyter-ai-agents/actions/workflows/build.yml)
[![PyPI - Version](https://img.shields.io/pypi/v/jupyter-ai-agents)](https://pypi.org/project/jupyter-ai-agents)

*Use Jupyter AI Agent, an AI Agent equipped with tools like 'execute', 'insert_cell', and more, to transform your Jupyter Notebooks into an intelligent, interactive workspace!*

![Jupyter AI Agent](https://assets.datalayer.tech/jupyter-ai-agents/ai-agents-prompt-demo-terminal.gif)

```
Jupyter AI Agent <-----------> JupyterLab
    |
    |   (RTC Real Time Collaboration)
    |
JNC + JKC

- JNC https://github.com/datalayer/jupyter-nbmodel-client
- JKC https://github.com/datalayer/jupyter-kernel-client
```

Jupyter AI Agent empowers **AI** models to **interact** with and **modify Jupyter Notebooks**. The agent is equipped with tools such as adding code cells, inserting markdown cells, executing code, enabling it to modify the notebook comprehensively based on user instructions or by reacting to notebook and kernel events.

This agent is **innovative** as it is designed to **operate on the entire notebook**, not just at the cell level, enabling more comprehensive and seamless modifications.

This powerful functionality is made possible through [jupyter-nbmodel-client](https://github.com/datalayer/jupyter-nbmodel-client) and [jupyter-kernel-client](https://github.com/datalayer/jupyter-kernel-client), enabling interaction with Jupyter Notebooks and Kernels.

[LangChain Agent Framework](https://python.langchain.com/v0.1/docs/modules/agents/how_to/custom_agent/) is used to manage the interactions between the AI model and the tools.

> [!WARNING] 
>
> jupyter-nbmodel-client and jupyter-kernel-client are experimental and under active development.
> Unexpected behavior may occur, due to potential issue generated by 3rd party projects.

## Usage

This library is documented on https://jupyter-ai-agents.datalayer.tech.

We put here a quick example for a Out-Kernel Stateless Agent helping your JupyterLab session.

To install Jupyter AI Agent, run the following command.

```bash
pip install jupyter_ai_agents
```

Or clone this repository and install it from source.

```bash
git clone https://github.com/datalayer/jupyter-ai-agents
cd jupyter-ai-agents
pip install -e .
```

The Jupyter AI Agent can directly interact with JupyterLab and the modifications made by the Jupyter AI Agent can be seen in real-time thanks to [Jupyter Real Time Collaboration](https://jupyterlab.readthedocs.io/en/stable/user/rtc.html). Make sure you have JupyterLab installed with the Collaboration extension.

```bash
pip install jupyterlab jupyter-collaboration ipykernel
```

Start JupyterLab, setting a `port` and a `token` to be reused by the agent, and create a notebook `test.ipynb`.

```bash
jupyter lab --port 8888 --IdentityProvider.token MY_TOKEN
```

Read the [Azure Documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai) to get the needed credentials and make sure you define them in the following `.env` file.

```bash
cat << EOF >>.env
OPENAI_API_VERSION="..."
AZURE_OPENAI_ENDPOINT="..."
AZURE_OPENAI_API_KEY="..."
EOF
```

To use the Jupyter AI Agent, an easy way is to launch a CLI (update the Azure deployment name based on your setup).

```bash
# Prompt agent example.
jupyter-ai-agents prompt \
  --url http://localhost:8888 \
  --token MY_TOKEN \
  --azure-ai-deployment-name gpt-40-mini \
  --path test.ipynb \
  --input "Create a matplotlib example"
```

![Jupyter AI Agent](https://assets.datalayer.tech/jupyter-ai-agents/ai-agents-prompt-demo-terminal.gif)

```bash
# Explain Error agent example.
jupyter-ai-agents explain-error \
  --url http://localhost:8888 \
  --token MY_TOKEN \
  --azure-ai-deployment-name gpt-40-mini \
  --path test.ipynb
```

![Jupyter AI Agent](https://assets.datalayer.tech/jupyter-ai-agents/ai-agents-explainerror-demo-terminal.gif)

## Uninstall

To uninstall the agent, execute.

```bash
pip uninstall jupyter_ai_agents
```

## Contributing

### Development install

```bash
# Clone the repo to your local environment
# Change directory to the jupyter_ai_agents directory
# Install package in development mode - will automatically enable
# The server extension.
pip install -e ".[test,lint,typing]"
```

### Running Tests

Install dependencies:

```bash
pip install -e ".[test]"
```

To run the python tests, use:

```bash
pytest
```

### Development uninstall

```bash
pip uninstall jupyter_ai_agents
```

### Packaging the library

See [RELEASE](RELEASE.md)
