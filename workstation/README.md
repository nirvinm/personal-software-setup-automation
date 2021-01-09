# fedora-postinstall-automation
Personal scripts and Ansible playbooks for configuring a fresh Fedora Silverblue/Workstation installation

## Step 1 - Update operating system:

**Silverblue**
    
    $ rpm-ostree upgrade

**Workstation**
    
    $ sudo dnf upgrade

and reboot.

## Step 2 - Install Ansible and RPMFusion:

**Silverblue**

    $ rpm-ostree install ansible https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm


and reboot to use the layered Ansible package

**Workstation**

    $ sudo dnf install ansible

(No reboot required)

## Step 3 - Install Ansible Collections:

Navigate to the directory where you've cloned this repository and execute following command to install Ansible Collections from `requirements.yml`.

    $ ansible-galaxy collection install -r requirements.yml

## Step 4 - Install system packages:

Execute the `system-*.yml` playbook to install core system tools like drivers, shells, virt-manager etc.

**Silverblue**

    $ ansible-playbook --ask-become-pass system-ostree.yml

**Workstation**

    $ ansible-playbook --ask-become-pass system-workstation.yml

and reboot.

## Step 5 - Configure system and services:

> Note: Before running this playbook you should have rebooted the system to ensure all installed services and users are available.

This playbook applies custom configurations, enables systemd services and other customizations.

    $ ansible-playbook --ask-become-pass config.yml


## Step 6 - Install userland apps

Execute `user.yml` playbook to install userland applications like Firefox, LibreOffice, VLC etc. from Flathub primarily. 

    $ ansible-playbook user.yml


Now enjoy Fedora!
