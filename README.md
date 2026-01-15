# 🏠 Legacy Hardware Home Lab & AI Server

> **Project Goal:** Resurrection of an old AMD E2-9000 PC into a fully functional Home Lab, Media Server, and Local AI Host.

<img width="3456" height="1992" alt="image" src="https://github.com/user-attachments/assets/61f4b262-5f59-4ccc-8fc5-97051399f86d" />



## 🛠️ The Hardware Challenge
This project runs entirely on recycled hardware. The goal was to build a modern microservices architecture without buying new gear.
* **CPU:** AMD E2-9000 Radeon R2 (Dual Core, non-AVX)
* **RAM:** 8GB DDR4 (approx. 4.5GB available for containers)
* **OS:** Ubuntu Server 24.04 (Headless)
* **Constraint:** The CPU struggles with AI models >1 Billion parameters, requiring extreme optimization and model selection.

## 🏗️ Architecture & Services
The server uses **Docker Compose** to orchestrate a suite of 15+ microservices. All services are secured behind **Nginx Proxy Manager** with Cloudflare DNS and strict firewall rules.

### 🧠 The AI Stack (Local LLMs)
| Service | Domain | Port | Description |
| :--- | :--- | :--- | :--- |
| **Ollama** | `localhost` | `11434` | The inference engine hosting the models. |
| **Open WebUI** | `llm-hs` | `3005` | ChatGPT-like UI for the local models. |

### 🛡️ Privacy & Infrastructure
| Service | Domain | Port | Description |
| :--- | :--- | :--- | :--- |
| **Nginx Proxy Manager** | `npm-hs` | `81` | SSL termination & reverse proxy. |
| **Pi-hole** | `pi-hole-hs` | `8082` | Network-wide ad blocker & DNS. |
| **Portainer** | `portainer-hs` | `9443` | Container management GUI. |
| **Uptime Kuma** | `system-health-hs` | `3001` | Service health monitoring & alerting. |

### 💻 Development & Productivity
| Service | Domain | Port | Description |
| :--- | :--- | :--- | :--- |
| **VS Code Server** | `vsc-hs` | `8888` | Remote development environment. |
| **Stirling PDF** | `pdf-hs` | `8089` | Local PDF manipulation tools. |
| **Reactive Resume**| `reactive-resume-hs` | `3002` | Open-source resume builder. |
| **Excalidraw** | `whiteboard-hs` | `6001` | Virtual whiteboard. |
| **Draw.io** | `drawio-hs` | `6025` | Professional diagramming tool. |
| **FreshRSS** | `news-hs` | `6003` | Self-hosted RSS aggregator. |

### 🍿 Media & Lifestyle
| Service | Domain | Port | Description |
| :--- | :--- | :--- | :--- |
| **Navidrome** | `music-hs` | `4533` | Self-hosted Spotify alternative. |
| **Mealie** | `mealie-hs` | `9925` | Recipe manager and scraper. |
| **FileBrowser** | `files-hs` | `6030` | Web-based file manager. |

---

## 🧪 The "AI Arena" Benchmarks
I tested multiple Large Language Models (LLMs) to find the absolute limit of the AMD E2 processor.

| Model | Parameters | Verdict |
| :--- | :--- | :--- |
| **Qwen 2.5 Coder** | 0.5B | **Daily Driver (Coding)** |
| **Llama 3.2** | 1B | Usable, but heavy |
| **Gemma 2** | 2B | Usable, but too slow |

---

## 🔧 Security & Access
* **HTTPS Everywhere:** All services are served over HTTPS using Let's Encrypt Wildcard Certificates via Cloudflare DNS Challenge.
* **Firewall (UFW):** All ports (except 80/443/SSH) are blocked from the local network. Access is only possible via the Reverse Proxy URLs.
* **Remote Access:** Tailscale Mesh VPN.

## 🚀 Roadmap
- [ ] **Automation:** Connect AI to iOS Shortcuts via **n8n**.
- [ ] **Backups:** Automate volume backups to external storage.
