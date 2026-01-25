# ANSIBLE

## Prequesites

Start ssh-agent for git

```sh
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

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
