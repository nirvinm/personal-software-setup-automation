# Personal workstation setup - Fedora
Personal scripts and Ansible playbooks for configuring a fresh Fedora Silverblue/Workstation installation

## Step 1 - Update operating system:

**Silverblue**
    
    $ rpm-ostree upgrade

**Workstation**
    
    $ sudo dnf upgrade

and reboot.

## Step 2 - Install Ansible:

    $ pip install --user ansible

## Step 3 - Add RPMFusion repository:

**Silverblue**

    $ rpm-ostree install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm


and reboot to use the layered packages.

**Workstation**

    $ sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

(No reboot required)

## Step 4 - Install Ansible Collections:

Navigate to the directory where you've cloned this repository and execute following command to install Ansible Collections from `requirements.yml`.

    $ ansible-galaxy collection install -r requirements.yml

## Step 5 - Install system packages:

Execute the `system-*.yml` playbook to install core system tools like drivers, shells, virt-manager etc.

**Silverblue**

    $ ansible-playbook --ask-become-pass system-ostree.yml

**Workstation**

    $ ansible-playbook --ask-become-pass system-workstation.yml

and reboot.

## Step 6 - Configure system and services:

> Note: Before running this playbook you should have rebooted the system to ensure all installed services and users are available.

This playbook applies custom configurations, enables systemd services and other customizations.

    $ ansible-playbook --ask-become-pass config.yml


## Step 7 - Install userland apps

Execute `user.yml` playbook to install userland applications like Firefox, LibreOffice, VLC etc. from Flathub primarily. 

    $ ansible-playbook user.yml


Now enjoy Fedora!
