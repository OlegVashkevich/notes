[<< На главную](../README.md)

# Пример docker compose команд для taskfile
```yaml
version: '3'
env:
  DCO_BIN: docker-compose 
tasks:
  up:
    desc: Start the Docker containers
    cmds:
      - ${DCO_BIN} up -d
  stop:
    desc: Stop the Docker containers
    cmds:
      - ${DCO_BIN} stop
  down:
    desc: Drop the Docker containers to wipe all data
    cmds:
      - ${DCO_BIN} down
  reset:
    desc: Rebuild Docker containers to wipe all data
    cmds:
      - ${DCO_BIN} down
      - task: up
```