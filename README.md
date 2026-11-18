# Tic Tac Toe 🎮

A classic Tic Tac Toe game built with Node.js/Express, deployed on AWS EC2.

## Features

- 🎯 Two-player mode (local)
- 🤖 Single-player vs Computer (Minimax AI — unbeatable!)
- 📊 Score tracking across rounds
- 🏆 Win highlighting animation
- 📱 Responsive design

## Tech Stack

| Layer       | Technology              |
|-------------|-------------------------|
| Frontend    | HTML5 / CSS3 / Vanilla JS |
| Backend     | Node.js 20 + Express 5  |
| Web Server  | Nginx (reverse proxy)   |
| Cloud       | AWS EC2 (t3.micro)      |
| IaC         | Terraform               |
| Config Mgmt | Ansible                 |
| CI/CD       | GitHub Actions          |

## Local Development

```bash
npm install
npm run dev
# Open http://localhost:3000
```

## Deployment

Deployment is fully automated via GitHub Actions on push to `main`:

1. **Lint** — ESLint check
2. **Test** — Unit tests
3. **Provision** — Terraform creates EC2 + EIP + SG
4. **Configure** — Ansible installs Node.js, deploys app, configures Nginx
5. **Verify** — Health check against the public IP

## Architecture

```
User → Nginx (port 80) → Node.js App (port 3000) on EC2 t3.micro
```

## Project Structure

```
├── public/          # Static frontend (Tic Tac Toe game UI)
├── src/             # Express routes and middleware
├── server.js        # App entry point
├── infra/           # Terraform IaC
├── ansible/         # Ansible playbook
└── .opsagent/       # Architecture + pipeline spec
```
