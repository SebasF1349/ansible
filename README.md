# ANSIBLE

## Prequesites

- Update dependencies (at least the linux kernel or some cmds will fail)

- Install git, gh, ansible and ssh

- Create ssh key

```sh
ssh-keygen -t ed25519 -C "sebas@gmail.com"
```

- Connect the gh account

```sh
gh auth login
```

(Web code can be entered manually from another device in
[https://github.com/login/device](https://github.com/login/device))

- Start ssh-agent for git

```sh
eval "$(ssh-agent -s)" && ssh-add ~/.ssh/id_ed25519
```

## Complete VARS

- Set `target_distribution` in `./group_vars/all/vars.yml` (`arch` or `debian`).

- edit use_wayland as desired

- Set `use_disk_encryption` to `true` or `false` as desired.

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

Update partition label variables in `./group_vars/all/vars.yml` if needed (used for encrypted Btrfs/Timeshift setup on both `arch` and `debian`).

Flathub and Timeshift tasks run on both `arch` and `debian`.

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
