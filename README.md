# Ollama Web UI: A User-Friendly Web Interface for Chat Interactions 👋

![GitHub repo size](https://img.shields.io/github/repo-size/ollama-webui/ollama-webui)
![GitHub last commit](https://img.shields.io/github/last-commit/ollama-webui/ollama-webui?color=red)

ChatGPT-Style Web Interface for Ollama 🦙

![Ollama Web UI Demo](./demo.gif)

## How to Install 🚀

### Installing Both Ollama and Ollama Web UI Using Docker Compose

If you don't have Ollama installed yet, you can use the provided Docker Compose file for a hassle-free installation. Simply run the following command:

```bash
docker compose up -d --build
```

This command will install both Ollama and Ollama Web UI on your system. Ensure to modify the `compose.yaml` file for GPU support and Exposing Ollama API outside the container stack if needed.


#### Accessing External Ollama on a Different Server

Change `OLLAMA_API_BASE_URL` environment variable to match the external Ollama Server url:

```bash
docker run -d -p 3000:8080 -e OLLAMA_API_BASE_URL=https://example.com/api --name ollama-webui --restart always ghcr.io/ollama-webui/ollama-webui:main
```

Alternatively, if you prefer to build the container yourself, use the following command:

```bash
docker build -t ollama-webui .
docker run -d -p 3000:8080 -e OLLAMA_API_BASE_URL=https://example.com/api --name ollama-webui --restart always ollama-webui
```

### TL;DR 🚀

Run the following commands to install:

```sh
git clone https://github.com/ollama-webui/ollama-webui.git
cd ollama-webui/

# Copying required .env file
cp -RPp example.env .env

# Building Frontend
npm i
npm run build

# Serving Frontend with the Backend
cd ./backend
pip install -r requirements.txt
sh start.sh
```

You should have the Ollama Web UI up and running at http://localhost:8080/. Enjoy! 😄

### Project Components

The Ollama Web UI consists of two primary components: the frontend and the backend (which serves as a reverse proxy, handling static frontend files, and additional features). Both need to be running concurrently for the development environment using `npm run dev`. Alternatively, you can set the `PUBLIC_API_BASE_URL` during the build process to have the frontend connect directly to your Ollama instance or build the frontend as static files and serve them with the backend.

### Prerequisites

1. **Clone and Enter the Project:**

   ```sh
   git clone https://github.com/ollama-webui/ollama-webui.git
   cd ollama-webui/
   ```

2. **Create and Edit `.env`:**

   ```sh
   cp -RPp example.env .env
   ```

### Building Ollama Web UI Frontend

1. **Install Node Dependencies:**

   ```sh
   npm install
   ```

2. **Run in Dev Mode or Build for Deployment:**

   - Dev Mode (requires the backend to be running simultaneously):

     ```sh
     npm run dev
     ```

   - Build for Deployment:

     ```sh
     # `PUBLIC_API_BASE_URL` overwrites the value in `.env`
     PUBLIC_API_BASE_URL='https://example.com/api' npm run build
     ```

3. **Test the Build with `Caddy` (or your preferred server):**

   ```sh
   curl https://webi.sh/caddy | sh

   PUBLIC_API_BASE_URL='https://localhost/api' npm run build
   caddy run --envfile .env --config ./Caddyfile.localhost
   ```

### Running Ollama Web UI Backend

If you wish to run the backend for deployment, ensure that the frontend is built so that the backend can serve the frontend files along with the API route.

#### Setup Instructions

1. **Install Python Requirements:**

   ```sh
   cd ./backend
   pip install -r requirements.txt
   ```

2. **Run Python Backend:**

   - Dev Mode with Hot Reloading:

     ```sh
     sh dev.sh
     ```

   - Deployment:

     ```sh
     sh start.sh
     ```

Now, you should have the Ollama Web UI up and running at [http://localhost:8080/](http://localhost:8080/).