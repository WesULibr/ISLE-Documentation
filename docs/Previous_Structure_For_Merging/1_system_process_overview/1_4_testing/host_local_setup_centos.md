### Host Local Setup Guide - CentOS

```
TO DO

Modify for Host Local Virtualbox settings Please

```


* This alpha build uses `isle.localdomain` as the test domain along with the Docker Compose service names e.g. `mysql, fedora, apache` etc.
     * If your institution's server uses real DNS, then skip the next step. If not, please proceed with the following:
     * To ensure this domain resolves properly, one will need to edit the servers and/or their own local `/etc/hosts` file.
         * Open up a terminal and enter: `sudo vi /etc/hosts`
              * Add one or more of the following: (**Examples ONLY**)

              * Ubuntu 16.04 LTS Host Server (or VM)  
              ```
             127.0.0.1       localhost isle.localdomain fedora apache fedora.isle.localdomain apache.isle.localdomain
             ```

             * Enduser local laptop
             ```
             127.0.0.1 localhost   
             192.156.123.26       isle.localdomain fedora apache fedora.isle.localdomain apache.isle.localdomain
             ```

#### Install / run on CentOS 7 server  
* Virtualbox Virtual Machine (VM)  
* a Vagrant image (recommend using [bento/centos-7.2](https://app.vagrantup.com/bento/boxes/centos-7.2))  
* Cloud based server e.g. Digital Ocean or Amazon Web Services  
* Post-installation, add the appropriate ssh keys to the root user's `.ssh/authorized_keys` file.  

#### Docker setup for CentOS 7

* Open a terminal, ssh to the CentOS server as root and install the following:  
     * `yum install openssl git htop ntp wget curl`

#### Install Docker on CentOS 7 (as root user)

* Add the RHEL/CENTOS epel-release package repository first

    * `sudo yum install epel-release`

    * `sudo yum install -y yum-utils device-mapper-persistent-data lvm2`

    * `sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo`

    * `sudo yum install docker-ce`

#### Create islandora user (as root)  
* `adduser islandora`

* `passwd islandora`

* `isle2017`

* `echo "islandora ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/islandora`

* Create Docker group `groupadd docker`  

* Add islandora user to docker group `usermod -aG docker islandora`  

* Add islandora user to wheel group `sudo usermod -aG wheel islandora`

* Create a ssh key for the islandora user
   * `mkdir /home/islandora/.ssh`  

   * `chmod -Rv 700 /home/islandora/.ssh`  

   * `cd /home/islandora/.ssh`  

   * `ssh-keygen`  
      * Follow the prompts to save these files to `/home/islandora/.ssh`

* Create an `authorized_keys` file in `/home/islandora/.ssh`using one of the following tools: `nano`, `pico`, `vi` or `emacs`

   * Example:
     ```
     vi /home/islandora/.ssh/authorized_keys
    ```

* Copy in the existing ssh key from the enduser's laptop /workstation. This will allow key based ssh access for the enduser.

      * `cat /Users/endusername/.ssh/id_rsa.pub`

      * Copy and paste this value exactly into the `/home/islandora/.ssh/authorized_keys` file.

* Exit out of the ssh session from the host server as the root user `exit`

* ssh back in as `islandora`

* Enable the Docker service to start on host server boot
    * `sudo systemctl enable docker.service`

* Start the Docker service
    * `sudo systemctl start docker`


#### Install Docker-Compose as islandora-user on CentOS 7
* Open a terminal and ssh back into the CentOS Host Server/VM as the `islandora` user and perform the following:

    * `sudo curl -L https://github.com/docker/compose/releases/download/1.19.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose`

    * `sudo chmod +x /usr/local/bin/docker-compose`

* Test the Installation
    * `docker-compose --version`

**Example output:**
```
  docker-compose version 1.19.0, build 1719ceb
```

#### Alternative install method for Docker-compose

In case the commands in the steps above fail, please use this alternative install.

* Install Python Pip (package manager for Python Scripting Language)

    * `sudo yum install -y python-pip`

* Upgrade Python to latest version

    * `sudo yum upgrade python*`

* Upgrade Python Pip

    * `sudo pip install --upgrade pip`

* Install Docker compose

    * `sudo pip install docker-compose`


#### Clone ISLE repository
* Please note in some Linux Distributions, one might need to create the `/opt` directory (optional)  

    * One can `ls -lha /` to see if an `/opt` directory exists  

        * If missing, `sudo mkdir /opt`  

        * If not missing, proceed to next step.  

* `cd /opt`

* `sudo git clone https://github.com/Islandora-Collaboration-Group/ISLE.git`

   * This process will take 1 - 3 minutes depending on internet bandwidth

* `sudo chown -Rv islandora:islandora ISLE`

* `cd /opt/ISLE`



#### Next steps
Once this process has finished one chose to do one of the following:

* Continue next steps with the [Test Site Guide - isle.localdomain](testsite_guide.md)

* Continue next steps with [Migration Guide](migration_guide.md)
---