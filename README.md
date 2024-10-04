# NEAR Sandbox

NEAR Sandbox is an experimental tool designed for the NEAR ecosystem, inspired by [Anthropic's Claude Artifacts](https://www.anthropic.com/news/claude-3-5-sonnet), Vercel [v0](https://v0.dev), and [GPT Engineer](https://gptengineer.app). It aims to provide developers with an AI-powered environment for building and testing applications on the NEAR blockchain.

Powered by [E2B Sandbox SDK](https://github.com/e2b-dev/e2b) and [Code Interpreter SDK](https://github.com/e2b-dev/code-interpreter).

![Preview](preview.png)

[→ Try NEAR Sandbox](https://sandbox-near.vercel.app/)

## About NEAR Sandbox

NEAR Sandbox is an experimental tool that combines AI-assisted code generation with a secure execution environment, tailored specifically for the NEAR ecosystem. It's designed to help developers rapidly prototype, test, and build applications on the NEAR blockchain.

Key features include:

- AI-powered code generation for NEAR-specific smart contracts and applications
- Secure code execution environment
- Real-time UI updates and streaming
- Support for multiple programming languages and frameworks

## Related NEAR Ecosystem Tools

While experimenting with NEAR Sandbox, you might also find these tools helpful:

1. [NEAR Fine-Tuned Model](https://github.com/jbarnes850/near-fine-tuning-job): A GPT-4o model fine-tuned on the NEAR ecosystem, designed to assist developers with NEAR-specific tasks and queries.

2. [NEAR Founder Copilot](https://github.com/jbarnes850/near-copilot): An AI-powered chatbot tailored for NEAR ecosystem builders, offering guidance and assistance throughout the development process.

3. [NEAR AI Cookbook](https://github.com/jbarnes850/near-ai-cookbook): A comprehensive guide and collection of examples for integrating AI capabilities with NEAR, perfect for developers looking to combine AI and onchain apps.

## Features

- Built on Next.js 14 (App Router, Server Actions), shadcn/ui, TailwindCSS, and Vercel AI SDK.
- Utilizes [Code Interpreter SDK](https://github.com/e2b-dev/code-interpreter) from [E2B](https://e2b.dev) for secure execution of AI-generated code.
- Supports real-time UI streaming for immediate feedback.
- Capable of installing and using any package from npm or pip.
- Supported development stacks:
  - 🔸 Python interpreter
  - 🔸 Next.js
  - 🔸 Vue.js
  - 🔸 Streamlit
  - 🔸 Gradio
- Integrated with multiple LLM providers:
  - 🔸 OpenAI
  - 🔸 Anthropic
  - 🔸 Google
  - 🔸 Mistral
  - 🔸 Groq
  - 🔸 Fireworks
  - 🔸 Together AI
  - 🔸 Ollama

## Getting Started

### Prerequisites

- [git](https://git-scm.com)
- Recent version of [Node.js](https://nodejs.org) and npm package manager
- [E2B API Key](https://e2b.dev)
- LLM Provider API Key

### Quick Start

1. Clone the repository:

   ```bash
   git clone https://github.com/jbarnes850/ai-artifacts
   cd ai-artifacts
   ```

2. Install dependencies:

   ```bash
   npm i
   ```

3. Set the environment variables

Create a `.env.local` file and set the following:

```sh
# Get your API key here - https://e2b.dev/
E2B_API_KEY="your-e2b-api-key"

# OpenAI API Key
OPENAI_API_KEY=

# Other providers
ANTHROPIC_API_KEY=
GROQ_API_KEY=
FIREWORKS_API_KEY=
TOGETHER_AI_API_KEY=
GOOGLE_AI_API_KEY=
MISTRAL_API_KEY=
```

4. Start the development server

```bash
npm run dev
```

5. Build the web app

```bash
npm run build
```

For detailed setup instructions and customization options, please refer to the [full documentation](https://github.com/jbarnes850/ai-artifacts).

## Customization

NEAR Sandbox is highly customizable. You can add new personas, LLM models, and providers to tailor the tool to your specific needs. For detailed instructions on customization, please see the [customization guide](https://github.com/jbarnes850/ai-artifacts/README.md).

Here's an example streamlit template:

```Dockerfile
# You can use most Debian-based base images
FROM python:3.19-slim

    RUN pip3 install --no-cache-dir streamlit pandas numpy matplotlib requests seaborn plotly

    # Copy the code to the container
    WORKDIR /home/user
    COPY . /home/user
    ```

5. Specify a custom start command in `e2b.toml`:

    ```toml
    start_cmd = "cd /home/user && streamlit run app.py"
    ```

6. Deploy the template with the E2B CLI

    ```
    e2b template build --name <template-name>
    ```

    After the build has finished, you should get the following message:

    ```
    ✅ Building sandbox template <template-id> <template-name> finished.
    ```

7. Open [lib/templates.json](lib/templates.json) in your code editor.

    Add your new template to the list. Here's an example for Streamlit:

    ```json
    "streamlit-developer": {
      "name": "Streamlit developer",
      "lib": [
        "streamlit",
        "pandas",
        "numpy",
        "matplotlib",
        "request",
        "seaborn",
        "plotly"
      ],
      "file": "app.py",
      "instructions": "A streamlit app that reloads automatically.",
      "port": 8501 // can be null
    },
    ```

    Provide a template id (as key), name, list of dependencies, entrypoint and a port (optional). You can also add additional instructions that will be given to the LLM.

4. Optionally, add a new logo under [public/thirdparty/templates](public/thirdparty/templates)

### Adding custom LLM models

1. Open [lib/models.json](lib/models.ts) in your code editor.

2. Add a new entry to the models list:

    ```json
    {
      "id": "mistral-large",
      "name": "Mistral Large",
      "provider": "Ollama",
      "providerId": "ollama"
    }
    ```

    Where id is the model id, name is the model name (visible in the UI), provider is the provider name and providerId is the provider tag (see [adding providers](#adding-custom-llm-providers) below).

### Adding custom LLM providers

1. Open [lib/models.ts](lib/models.ts) in your code editor.

2. Add a new entry to the `providerConfigs` list:

    Example for fireworks:

    ```ts
    fireworks: () => createOpenAI({ apiKey: apiKey || process.env.FIREWORKS_API_KEY, baseURL: baseURL || 'https://api.fireworks.ai/inference/v1' })(modelNameString),
    ```

3. Optionally, adjust the default structured output mode in the `getDefaultMode` function:

    ```ts
    if (providerId === 'fireworks') {
      return 'json'
    }
    ```

4. Optionally, add a new logo under [public/thirdparty/logos](public/thirdparty/logos)

## Contributing

As an open-source project, we welcome contributions from the community. If you are experiencing any bugs or want to add some improvements, please feel free to open an issue or pull request.

## License

This project is open-source and available under the MIT License. See the [LICENSE](LICENSE) file for details.
