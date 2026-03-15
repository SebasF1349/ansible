# ANSIBLE

## Prequesites

- Update dependencies (at least the linux kernel or some cmds will fail)

- Start ssh-agent for git

```sh
eval "$(ssh-agent -s)" && ssh-add ~/.ssh/id_ed25519
```

## Complete VARS

- edit use_wayland as desired

- Get partition labels with

```sh
lsblk -f
```

If any partition miss the labels add them with (edit partition and/or label as needed)

```sh
sudo btrfs filesystem label / ARCH_ROOT # BTRFS

sudo fatlabel /dev/sda1 BOOT # FAT32

sudo cryptsetup config /dev/sda2 --label LUKS_ROOT # LUKS

sudo e2label /dev/sda3 STORAGE # ext4
```

Update the appropriated variables in `./group_vars/all/vars.yml` if needed.

## Run

First install collections

```sh
ansible-galaxy collection install -r requirements.yml
```

Then run ansible

```sh
ansible-playbook run.yml -K
```

Note: `-K` makes ansible run with sudo when needed
