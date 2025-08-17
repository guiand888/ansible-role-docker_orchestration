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

# Project discovery mode: 'auto' or 'manual' (default: auto)
docker_projects_mode: auto

# Project exclusion list - projects to skip
docker_projects_exclude: []

# Project configurations (manual mode only)
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

## Project Discovery Modes

### Auto Mode (Default)

Automatically discovers Docker projects by scanning subdirectories in `docker_project_root`:

```bash
/home/user/docker/
├── nextcloud/          # Auto-discovered as 'nextcloud'
├── wordpress/          # Auto-discovered as 'wordpress'
└── monitoring/         # Auto-discovered as 'monitoring'
```

Each discovered project gets default settings:
- `state: started`
- `pull: true` (based on `docker_build_default`)
- `build: false`
- `start: true`
- `restart: false` (based on `docker_restart_default`)
- `recreate: false`

### Manual Mode

Explicitly define projects in variables:

```yaml
docker_projects_mode: manual
docker_projects:
  - name: webapp
    state: started
    pull: true
    recreate: true
```

## Example Usage

See `playbooks/docker-maintenance-compose.ansible.yml` for ready-to-use playbook.

### Excluding Projects

To exclude specific projects from orchestration, define `docker_projects_exclude` in host_vars:

```yaml
# host_vars/server1.yml
docker_projects_exclude:
  - nextcloud
  - maintenance-project
```

Excluded projects will be skipped during all operations (pull, build, start, restart).

## Author

Guillaume Andre (@guinad888)
- [mail@guillaumea.fr](mailto:mail@guillaumea.fr)
- [blog.guillaumea.fr](https://blog.guillaumea.fr)
