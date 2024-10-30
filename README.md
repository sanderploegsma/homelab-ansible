# Homelab automation with Ansible

## Requirements

- Ansible 10.5.0

Install Ansible collections using:

```sh
ansible-galaxy install -r requirements.yml
```

## Troubleshooting

### A worker was found in a dead state

When running into an error like the following when running Ansible playbooks from macOS:

> +[__NSCFConstantString initialize] may have been in progress in another thread when fork() was called. We cannot safely call it or ignore it in the fork() child process. Crashing instead. Set a breakpoint on objc_initializeAfterForkError to debug. ERROR! A worker was found in a dead state

Make sure to set the following environment variable in your shell:

```sh
export OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES
```

See the [Ansible FAQ](https://docs.ansible.com/ansible/latest/reference_appendices/faq.html#running-on-macos-as-a-target).

### GNU tar required

In case a playbook tries to unarchive a tarball on the Ansible controller when running macOS, it may complain about GNU tar missing:

> Command "/usr/bin/tar" detected as tar type bsd. GNU tar required.

```sh
brew install gnu-tar
```

```sh
echo 'export PATH="/opt/homebrew/opt/gnu-tar/libexec/gnubin:$PATH"' >> ~/.zshrc
```
