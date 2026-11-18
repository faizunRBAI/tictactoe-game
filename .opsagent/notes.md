# tic-tac-toe — Working Notes

## Status
- [x] Project meta approved (aws / us-east-1 / ec2)
- [x] Architecture written (EC2 + Nginx + Node.js)
- [x] Pipeline written (lint → test → provision → configure → verify)
- [x] Design approved
- [x] Plan approved
- [x] Scaffold generated (node/express)
- [x] Game UI written (public/index.html — full Tic Tac Toe with AI)
- [x] Terraform IaC written (infra/)
- [x] Ansible playbook written (ansible/site.yml)
- [x] README written
- [ ] validate_project
- [ ] create_repo_and_push
- [ ] deploy

## Key Decisions
- Node.js 20 on Ubuntu 22.04 — installed via NodeSource (not apt default which ships older version)
- App binds 127.0.0.1:3000; Nginx proxies :80 → :3000
- EIP used so the IP survives instance stop/start; verify stage reads it from terraform output directly (self-sufficient job rule)
- No database needed — game state is client-side only
- Minimax AI implemented in vanilla JS (no backend needed for AI)
- Each CI stage (configure, verify) re-runs terraform init + output to get the IP independently (platform pitfall #3)

## Gotchas
- Ubuntu 22.04 apt ships Node.js 12 — MUST use NodeSource setup script for Node 20
- ansible.builtin.copy used for src/ and public/ directories (not community.general.synchronize) to avoid collection install
- No cache_valid_time on apt update (platform pitfall #1c — fresh VM cache)
- Scores tracked in browser memory only (page refresh resets score — by design for Tier 1)
