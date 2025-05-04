# Configure SSH

Configures the ssh daemon, fail2ban and ufw for ssh access.

## Requirements

none

## Role Variables

| Variable                              | Required | Default                 | Choices     | Comments                                     |
|---------------------------------------|----------|-------------------------|-------------|----------------------------------------------|
| ssh_permit_root_login                 | yes      | "no"                    | "no", "yes" |                                              |
| ssh_client_alive_interval             | yes      | 300                     |             |                                              |
| ssh_client_alive_count_max            | yes      | 5                       |             |                                              |
| ssh_port                              | yes      | 22                      |             |                                              |
| ssh_password_authentication           | yes      | "no"                    | "no", "yes" |                                              |
| ssh_x11_forwarding                    | yes      | "no"                    | "no", "yes" |                                              |
| ssh_max_auth_tries                    | yes      | 10                      |             |                                              |
| ssh_allow_tcp_forwarding              | yes      | "no"                    | "no", "yes" |                                              |
| ssh_allow_agent_forwarding            | yes      | "no"                    | "no", "yes" |                                              |
| ssh_authorized_keys_file              | yes      | ~/.ssh/authorized_keys" |             |                                              |
| ssh_pubkey_authentication             | yes      | "yes"                   | "no", "yes" |                                              |
| ssh_challenge_response_authentication | yes      | "no"                    | "no", "yes" |                                              |
| ufw_enabled                           | yes      | false                   | true, false |                                              |
| fail2ban_enabled                      | yes      | false                   | true, false | install and configure fail2ban on the system |
| ssh_fail2ban_enabled                  | yes      | false                   | true, false | enable fail2ban for ssh logins               |

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
