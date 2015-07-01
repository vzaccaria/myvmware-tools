Instructions for setting up a working development VM Fusion image
=================================================================

Here I'll find some of the steps I did when setting up VMware fusion for
development. They've been collected using an Ubuntu 14.04; hopefully
they'll be useful for other versions as well.

Authentication
--------------

Set up ssh on the target image

    sudo apt-get install openssh-server
    scp zaccaria@macbook.local:/Users/zaccaria/.ssh/id_rsa.pub /home/zaccaria/.ssh/authorized_keys
    sudo restart ssh

test it with:

    ssh zaccaria@172.16.189.143

Folder sharing
--------------

VMWare tools suck. To set up folder sharing, I've used sshfs in this
way:

On the Mac:

``` shell
sudo mkdir /Volumes/Ubuntu                                   # Create shared folder
sshfs zaccaria@172.16.189.143:/home/zaccaria /Volumes/Ubuntu # Dont use sudo!
```

Environment setup
-----------------

To setup the env, we'll use ansible with the playbook in the `ansible`
directory:

    cd ansible
    ansible-playbook deploy.yml -i host-list.ini -K

where:

-   `-K` asks for the sudo password.
-   `-i` specifies the target host(s)
-   `deploy.yml` is the top level deployment file

