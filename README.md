# guiand888.docker_orchestration

Ansible role for Docker Compose orchestration - build, pull, start, stop, and restart services.

## Requirements

- Docker and Docker Compose installed on target hosts
- Ansible 2.9+

## Role Variables

```yaml
# Root directory containing Docker projects
docker_project_root: "/home/{{ ansible_user }}/docker"

# Default behaviors
docker_build_default: true
docker_restart_default: false

# Project configurations
docker_projects:
  - name: project_name
    state: started        # started|stopped|restarted
    pull: true           # Pull images before operations
    build: false         # Build images
    start: true          # Start services
    restart: false       # Restart services
    recreate: false      # Recreate containers
```

## Example Playbook

```yaml
- hosts: docker_hosts
  roles:
    - guiand888.docker_orchestration
  vars:
    docker_projects:
      - name: webapp
        state: started
        pull: true
        recreate: true
```

## Example Usage

See `playbooks/docker-maintenance-compose.ansible.yml` for ready-to-use playbook.

## Author

Guillaume Andre (@guinad888)
- [mail@guillaumea.fr](mailto:mail@guillaumea.fr)
- [blog.guillaumea.fr](https://blog.guillaumea.fr)
