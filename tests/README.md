# Test harness

This role uses the joe-speedboat OS-independent task dispatcher. Run tests from a separate harness with symlinks instead of `role: ../../`, so `tasks/main.yml` resolves `role_path|basename` correctly.

```bash
mkdir -p /tmp/log-forwarder-harness/roles
ln -sfn "$PWD" /tmp/log-forwarder-harness/roles/joe-speedboat.log_forwarder
ln -sfn "$PWD" /tmp/log-forwarder-harness/roles/ansible.log_forwarder
ANSIBLE_ROLES_PATH=/tmp/log-forwarder-harness/roles \
  ansible-playbook -i tests/inventory tests/deploy.yml --syntax-check
```

The second symlink covers runs where Ansible resolves `role_path|basename` to the repository name (`ansible.log_forwarder`).
