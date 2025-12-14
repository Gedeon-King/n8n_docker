# n8n – Docker Compose Setup

This repository provides a simple and production-ready **Docker Compose** configuration to run **n8n**, an open-source workflow automation tool.

---

## 📦 What is n8n?

**n8n** is a workflow automation platform that allows you to connect APIs, services, and applications with little to no code. It is widely used for:

* Automation & orchestration
* ETL / data pipelines
* Security & DevOps workflows
* No-code / low-code integrations

Official website: [https://n8n.io](https://n8n.io)

---

## 📁 Project Structure

```
.
├── docker-compose.yml
├── .env
└── n8n_data/
```

* **docker-compose.yml** → Service definition
* **.env** → Environment variables (recommended)
* **n8n_data/** → Persistent data (credentials, workflows, settings)

---

## 🐳 Docker Compose Configuration

```yaml
services:
  n8n:
    image: n8nio/n8n:latest
    container_name: n8n
    ports:
      - 5678:5678
    environment:
      - GENERIC_TIMEZONE=${GENERIC_TIMEZONE}
      - N8N_SECURE_COOKIE=${N8N_SECURE_COOKIE}
    volumes:
      - ./n8n_data:/home/node/.n8n
```

### 🔍 Explanation

* **image**: Official n8n Docker image
* **container_name**: Explicit container name for clarity
* **ports**: Exposes n8n on port `5678`
* **environment**: Runtime configuration via environment variables
* **volumes**: Persists workflows and credentials

---

## ⚙️ Environment Variables (.env)

Create a `.env` file in the same directory:

```env
GENERIC_TIMEZONE=Europe/Paris
N8N_SECURE_COOKIE=true
```

### Variable Details

| Variable            | Description                                    |
| ------------------- | ---------------------------------------------- |
| `GENERIC_TIMEZONE`  | Sets the timezone for workflows                |
| `N8N_SECURE_COOKIE` | Enables secure cookies (required behind HTTPS) |

> ⚠️ In production, `N8N_SECURE_COOKIE=true` **requires HTTPS** (reverse proxy).

---

## ▶️ How to Run

### Start n8n

```bash
docker compose up -d
```

### Stop n8n

```bash
docker compose down
```

### View Logs

```bash
docker logs -f n8n
```

---

## 🌐 Access n8n

Once running, access n8n via your browser:

```
http://localhost:5678
```

---

## 🔐 Data Persistence

All important data is stored in:

```
./n8n_data
```

This includes:

* Credentials
* Workflows
* Encryption keys
* User settings

👉 **Never delete this folder** unless you want a full reset.

---

## 🚀 Production Recommendations

For a production deployment, consider:

* ✅ Reverse proxy (Nginx / Traefik / Caddy)
* ✅ HTTPS (Let’s Encrypt)
* ✅ `N8N_BASIC_AUTH_ACTIVE=true`
* ✅ PostgreSQL instead of SQLite
* ✅ Regular backups of `n8n_data`

Example security variables:

```env
N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=admin
N8N_BASIC_AUTH_PASSWORD=strongpassword
```

---

## 🧪 Tested Environments

* Docker Desktop (Windows / macOS)
* Docker Engine (Linux)
* WSL2 (Ubuntu)

---

## 📚 Useful Links

* Documentation: [https://docs.n8n.io](https://docs.n8n.io)
* Docker Image: [https://hub.docker.com/r/n8nio/n8n](https://hub.docker.com/r/n8nio/n8n)
* GitHub: [https://github.com/n8n-io/n8n](https://github.com/n8n-io/n8n)

---

## 👨‍💻 Maintainer Notes

This setup is intentionally minimal, secure by default, and easy to extend.

Feel free to adapt it for:

* SOC automation
* DevSecOps pipelines
* Incident response workflows

---

✅ **You are now ready to automate with n8n.**
