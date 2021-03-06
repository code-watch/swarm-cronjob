# Renovate

```yaml
version: "3.8"

services:
  renovate:
    image: "renovate/renovate:slim"
    configs:
      - source: config-js-prod-v1
        target: /usr/src/app/config.js
    secrets:
      - api-token-v1
    healthcheck:
      disable: true
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
    deploy:
      mode: replicated
      replicas: 0
      labels:
        - "swarm.cronjob.enable=true"
        - "swarm.cronjob.schedule=*/30 * * * *"
      restart_policy:
        condition: none

configs:
  config-js-prod-v1:
    file: configs/prod/config.js.tmpl
    template_driver: golang

secrets:
  api-token-v1:
    external: true
```
