# 🏠 Legacy Hardware Home Lab & AI Server

> **Project Goal:** Resurrection of an older AMD E2-9000 PC into a comprehensive Home Lab, Media Server, and Local AI Host.

<img width="3456" height="1994" alt="image" src="https://github.com/user-attachments/assets/ad01ab0d-31d2-459f-9779-a391d811c052" />

## 🛠️ The Hardware Challenge
This project runs entirely on recycled hardware. The goal was to build a modern microservices architecture without buying new gear.
* **CPU:** AMD E2-9000 Radeon R2 (Dual Core, non-AVX)
* **RAM:** 8GB DDR4 (approx. 4.5GB available for containers)
* **OS:** Ubuntu Server 24.04 (Headless)
* **Constraint:** The CPU struggles with AI models >1 Billion parameters, requiring extreme optimization and model selection.

---

## 🏗️ Architecture & Services
The server uses **Docker Compose** to orchestrate a suite of 10+ microservices, categorized by function.

### 🧠 The AI Stack (Local LLMs)
| Service | Type | Port | Description |
| :--- | :--- | :--- | :--- |
| **Ollama** | Backend | `11434` | The inference engine hosting the models. |
| **Open WebUI** | Interface | `3005` | ChatGPT-like UI for the local models. |

### 🛡️ Privacy & Infrastructure
| Service | Type | Port | Description |
| :--- | :--- | :--- | :--- |
| **Pi-hole** | Network | `8082` | Network-wide ad blocker and DNS sinkhole. |
| **Portainer** | Mgmt | `9443` | Container management GUI (HTTPS). |
| **Uptime Kuma** | Status | `3001` | Service health monitoring. |

### 💻 Development & Productivity
| Service | Type | Port | Description |
| :--- | :--- | :--- | :--- |
| **VS Code Server** | IDE | `8888` | Remote development environment in the browser. |
| **Stirling PDF** | Tools | `8089` | Local PDF manipulation tools (merge, split, edit). |
| **Reactive Resume**| Builder | `3000` | Open-source resume builder. |

### 🍿 Media & Lifestyle
| Service | Type | Port | Description |
| :--- | :--- | :--- | :--- |
| **Navidrome** | Music | `4533` | Self-hosted Spotify alternative. |
| **Mealie** | Food | `9925` | Recipe manager and scraper. |

---

## 🧪 The "AI Arena" Benchmarks
I tested multiple Large Language Models (LLMs) to find the absolute limit of the AMD E2 processor.

| Model | Parameters | Performance | Verdict |
| :--- | :--- | :--- | :--- |
| **Qwen 2.5** | 0.5B | ⚡️ Fast | **Winner (Daily Driver)** |
| **Qwen 2.5 Coder** | 0.5B | ⚡️ Fast | **Winner (Coding)** |
| **Llama 3.2** | 1B | 🐢 Slow | Usable, but lags |
| **Gemma 2** | 2B | 🐢 Slow | Too heavy for CPU |

### 🤣 "Hallucination of the Year"
*Model: Qwen 2.5 Coder (0.5B)*
Due to its heavy training on code repositories, the 0.5B model lacks "common sense" world knowledge.
> **Prompt:** "Why is the sky blue?"
> **AI Answer:** "It is possible that the blue sky is due to **cloud computing** or other factors such as human activities."
*(See `screenshots/ai-chat.png` for the proof)*

---

## 🔧 Deployment
The entire stack is defined in `docker-compose.yml` and managed via a single command.

```bash
# Clone the repository
git clone [https://github.com/YOUR_USERNAME/home-server-ai.git](https://github.com/YOUR_USERNAME/home-server-ai.git)

# Start the stack
docker compose up -d
```
#### Key Configurations
* Port Mapping: Custom ports (3005, 9925) were used to avoid conflicts with reserved services.

* Volume Management: Persistent data stored in ./volumes/ to survive reboots.

* Resource Limits: Heavy containers (Mealie, VS Code) are capped at 1GB RAM to prevent OOM kills.

## 🚀 Roadmap
- [ ] Automation: Connect AI to iOS Shortcuts via n8n.

- [ ] Remote Access: Configure Cloudflare Tunnel for secure external access.

- [ ] Backups: Automate Restic backups to cloud storage.


