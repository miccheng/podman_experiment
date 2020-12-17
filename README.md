# Podman Experiment

## Installation

1. Install [VirtualBox](https://www.virtualbox.org/)
2. Install [Vagrant](https://www.vagrantup.com/)
3. Start Vagrant box in this repo:

    ```bash
    vagrant up
    ```
    
    The Vagrant provisioning script should install the Podman binary.
    
    *Reference: <https://podman.io/getting-started/installation>*

4. Configure Podman remote:

    ```bash
    systemctl --user enable --now podman.socket
    sudo loginctl enable-linger $USER
    ```
    
    *Reference: <https://github.com/containers/podman/blob/master/docs/tutorials/mac_win_client.md>*

5. Generate a dev SSH key:

    ```bash
    ssh-keygen -t rsa -C "podman-test"
    ```
    
    Add the new public key to the Vagrant instance: `~/.ssh/authorized_keys`
    
    You might want to try and SSH into the Vagrant instance first.
    
    ```bash
    ssh vagrant@127.0.0.1 -p 2222 -i ~/.ssh/podman_dev_rsa
    ```

6. Install Podman client:

    ```
    brew install podman
    ```
    
7. Setup your Podman to connect to the Vagrant box:
    
    ```
    podman system connection add podmanexp --identity ~/.ssh/podman_dev_rsa ssh://vagrant@127.0.0.1:2222/run/user/1000/podman/podman.sock
    
    podman system connection list
    podman info
    ```

## Getting Started

Reference: <https://podman.io/getting-started/>