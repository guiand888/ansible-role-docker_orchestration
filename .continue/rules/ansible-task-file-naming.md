---
globs:
  - tasks/**/*.yml
description: Ensure all new Ansible task implementations are created in separate
  '.ansible.yml' files within the tasks folder and then referenced in
  'main.yml'.
---

Create individual Ansible task files in the tasks folder with filenames ending in '.ansible.yml', and call these tasks into the 'main.yml'.