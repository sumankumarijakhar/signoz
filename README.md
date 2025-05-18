# signoz
signoz demo with docker-compose 

```bash
ansible-playbook up.yml
```

This does docker compose up on an "empty" signoz in a codespace. Use this as a starting point for instrumenting your app.

```bash
ansible-playbook down.yml
```

This does docker compose down on the clickhouse-setup/docker-compose-minimal.yaml (the same docker-compose file from up.yml)

## -------------------------------------------------------------------------------
Hypothesis 1: Missing Docker Monitoring Setup

Problem:
No Docker container metrics were shown. The otel-collector was not set up to collect Docker/container data.

What I did:
- Added `docker_stats` and `hostmetrics` to otel-collector config.
- Mounted `/var/run/docker.sock` in docker-compose.

Result:  
Docker container metrics started showing in the SigNoz UI.

## -------------------------------------------------------------------------------

## -------------------------------------------------------------------------------
Hypothesis 2: Outdated Image Versions

Problem:
Some Docker images were old. That might cause services to not work correctly together.

What I did:
- Updated images like `query-service`, `frontend`, and `otel-collector` to latest stable versions.

Result:  
Everything worked after update. UI was working and metrics loaded.
## -------------------------------------------------------------------------------