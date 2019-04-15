# Hashi

A role to install the Hashicorp tools.

## Requirements

- curl
- wget
- gpg


## Role Variables

The versions for the tools can override those set in defaults:

- `terraform.version`
- `packer.version`
- `vault.version`

## Dependencies

None.


## Example Playbook

    - hosts: servers
      roles:
         - { role: brucellino.hashi, become: true }

## License

MIT

## Author Information


Bruce Becker | brucellino@gmail.com