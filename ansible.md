# Ansible

## Ansible Commands

| Command | Action |
| ------- | ------ |
| `ansible [pattern] -m [module] -a "[module options]"` | Ad hoc command structure |
| `ansible <host-or-group> -m ping` | Ansible-ping host or group |
| `ansible <host-or-group> -a "sudo /sbin/reboot"` | Reboot a host or group |
| `ansible <host-or-group> -a setup \| less` | Check host facts |
| `ansible <host-or-group> -a "uptime"` | Run a command |

## Ansible Playbook Commands

| Command | Action |
| ------- | ------ |
| `ansible-playbook playbook.yml --syntax-check` | Check playbook for syntax errors |
| `ansible-playbook playbook.yml --list-hosts` | List hosts that will be affected |
| `ansible-playbook playbook.yml --check` | Dry-run a playbook |
| `ansible-playbook playbook.yml` | Execute a playbook |
| `ansible-playbook playbook.yml --ask-pass` | Prompt for SSH (or windows) password |
| `ansible-playbook playbook.yml --syntax-check` | Execute a playbook step by step |
| `ansible-playbook playbook.yml --v` | Verbose output (increase up to `--vvvvvv`) |

## Ansible Inventory Commands

| Command | Action |
| ------- | ------ |
| `ansible-inventory --list` | Print inventory in JSON |
| `ansible-inventory --list -y` | Print inventory in YAML |
| `ansible-inventory --graph` | Print inventory in Tree Structure |
| `ansible-inventory --host <hostname>` | Print info about a specific host |

## References

* [Ansble Cheatsheet | Software Engineer World 🌐](https://sweworld.net/cheatsheets/ansible/)
* [Ansible Cheat Sheet: CLI Commands and Basics | spacelift.io 🌐](https://spacelift.io/blog/ansible-cheat-sheet)
* [Introduction to ad hoc commands | Ansible Docs 🌐](https://docs.ansible.com/ansible/latest/command_guide/intro_adhoc.html)
* [omerbsezer/Fast-Ansible | Github 🌐](https://github.com/omerbsezer/Fast-Ansible) - tons of ansible examples, tutorials, labs, etc.
