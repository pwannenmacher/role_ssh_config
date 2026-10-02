# Configure SSH

Configures the ssh daemon, fail2ban and ufw for ssh access.

## Requirements

none

## Role Variables

| Variable                              | Required | Default                 | Choices     | Comments                                     |
|---------------------------------------|----------|-------------------------|-------------|----------------------------------------------|
| ssh_permit_root_login                 | true      | "no"                    | "no", "true" |                                              |
| ssh_client_alive_interval             | true      | 300                     |             |                                              |
| ssh_client_alive_count_max            | true      | 5                       |             |                                              |
| ssh_port                              | true      | 22                      |             |                                              |
| ssh_password_authentication           | true      | "no"                    | "no", "true" |                                              |
| ssh_x11_forwarding                    | true      | "no"                    | "no", "true" |                                              |
| ssh_max_auth_tries                    | true      | 10                      |             |                                              |
| ssh_allow_tcp_forwarding              | true      | "no"                    | "no", "true" |                                              |
| ssh_allow_agent_forwarding            | true      | "no"                    | "no", "true" |                                              |
| ssh_authorized_keys_file              | true      | .ssh/authorized_keys    |             |                                              |
| ssh_pubkey_authentication             | true      | "true"                   | "no", "true" |                                              |
| ssh_challenge_response_authentication | true      | "no"                    | "no", "true" |                                              |
| ufw_enabled                           | true      | false                   | true, false |                                              |
| fail2ban_enabled                      | true      | false                   | true, false | install and configure fail2ban on the system |
| ssh_fail2ban_enabled                  | true      | false                   | true, false | enable fail2ban for ssh logins               |
| ssh_match_blocks                      | no       | []                      |             | Match blocks appended to sshd_config         |

### Match blocks

`ssh_match_blocks` is written as a managed block at the end of `/etc/ssh/sshd_config` and validated with `sshd -t` before sshd is restarted. An empty list removes the block.

```yaml
ssh_match_blocks:
  - criteria: User deploy
    options:
      AuthenticationMethods: publickey
      ForceCommand: sudo -n /opt/apps/ci/deploy.sh
      PermitTTY: "no"
      AllowTcpForwarding: "no"
      AllowAgentForwarding: "no"
      X11Forwarding: "no"
```

Boolean values are written as `yes`/`no`.

## Dependencies

`community.general.ufw` is used which should come with ansible by default

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - role: role_ssh_config
```

## License

MIT

## Author Information

Paul Wannenmacher
