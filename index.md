---

layout: ribbon

style: |

    #Cover h2 {
        margin:30px 0 0;
        color:#FFF;
        text-align:center;
        font-size:70px;
        }
    #Cover p {
        margin:10px 0 0;
        text-align:center;
        color:#FFF;
        font-style:italic;
        font-size:20px;
        }
        #Cover p a {
            color:#FFF;
            }
    #Picture h2 {
        color:#FFF;
        }
    #SeeMore h2 {
        font-size:100px
        }
    #SeeMore img {
        width:0.72em;
        height:0.72em;
        }
    #Inventory p {
        margin:0 0 15px;
        line-height:25px;
        }
    #Inventory code {
        margin:0 0 0;
        line-height:25px;
        }

    #Inventory1 p {
        margin:0 0 15px;
        line-height:25px;
        }
    #Inventory1 code {
        margin:0 0 0;
        line-height:25px;
        }


---

# Ansible for Intermediates {#Cover}

*Brought you by [Gaurav Ashtikar](http://gau1991.me/)*

![](pictures/cover.jpg)
<!-- photo by WikiPedia, https://en.wikipedia.org/wiki/Server_%28computing%29#/media/File:Wikimedia_Foundation_Servers-8055_35.jpg CC BY-SA 3.0 -->


## Contents

  1. Become
  2. More about Inventory
  3. Check Mode
  4. Playbooks Variables and Jinja2 filters
  5. Playbooks Conditionals, Loops and Blocks
  6. Playbook Example - WordPress & Nginx on RHEL system
  7. Vaults

## Become

  - Directive
    - become
    - become_user
    - become_method
  - Connection variables
    - ansible_become
    - ansible_become_method
    - ansible_become_user
    - ansible_become_pass

## Become

 - Command Line Options
   - `--ask-become-pass, -K`
   - `--become, -b`
   - `--become-method=BECOME_METHOD`
   - `--become-user=BECOME_USER`


## More about Inventory

<b>Host Variables</b>

    [atlanta]
    host1 http_port=80 maxRequestsPerChild=808
    host2 http_port=303 maxRequestsPerChild=909


## More about Inventory {#Inventory1}

<b>Group Variables</b>

    [atlanta]
    host1
    host2

    [atlanta:vars]
    ntp_server=ntp.atlanta.example.com
    proxy=proxy.atlanta.example.com

## More about Inventory {#Inventory}

<b>Groups of Groups, and Group Variables</b>

    [atlanta]
    host1

    [raleigh]
    host2

    [southeast:children]
    atlanta
    raleigh

    [southeast:vars]
    some_server=foo.southeast.example.com

    [usa:children]
    southeast

## Check Mode

1. Using Check Mode
  - `$ansible-playbook foo.yml --check`
2. Running a task in check mode
  - `always_run: yes`
3. Showing Differences
  - `ansible-playbook foo.yml --check --diff --limit foo.example.com`


## Test your setup

1. `$ansible all -m ping`
3. `$ansible all -m ping -u root -k`
4. `$ansible all -m ping -K`
5. `$ansible all -m ping -f 10`

## Modules

1. Libraries that can be executed directly on remote hosts or through Playbooks.
2. User can also write their own modules
3. Two types of modules:
  - [Core Modules](https://github.com/ansible/ansible-modules-core)
  - [Extras Modules](https://github.com/ansible/ansible-modules-extras)

## Command Modules
  - `$ansible all -m command -a "ls"`
  - `$ansible all -m command -a "df -h"`
  - `$ansible all -m shell -a "ls"`
  - `$ansible all -m shell -a "ls | grep txt"`
  - `$ansible all -m shell -a "apt-get update"`

## System Modules:
  - `$ansible all -m ping`
  - `$ansible all -m setup`
  - `$ansible all -m hostname -a "name=web01"`
  - `$ansible all -m service -a "name=nginx state=started"`
  - `$ansible all -m user -a "name=jsmith generate_ssh_key=yes ssh_key_bits=2048 ssh_key_file=.ssh/id_rsa"`


## File Modules:
  - `$ansible all -m copy -a "src=/srv/myfiles/foo.conf dest=/etc/foo.conf"`
  - `$ansible all -m find -a "paths=/tmp patterns=*.old"`
  - `$ansible all -m stat -a "path=/path/to/something checksum_algorithm=sha256"`


## Source Control Modules:
  - `$ansible all -m git -a "repo=git://git@github.com/mylogin/hello.git dest=/home/mylogin/hello"`
  - `$ansible all -m git -a "repo=git://foosball.example.org/path/to/repo.git dest=/srv/checkout clone=no update=no"`


## Packaging Modules:
  - `$ansible all -m apt -a "name=htop update_cache=yes"`
  - `$ansible all -m apt -a "name=htop state=latest"`
  - `$ansible all -m apt -a "name=htop state=absent"`
  - `$ansible all -m apt -a "upgrade=dist"`

## Playbooks

Basic Playbook `nginx.yml` example:

    ---
    - hosts: local
    tasks:
      - name: Install Nginx
        apt: pkg=nginx state=installed update_cache=true

To run Playbook : `$ansible-playbook -b nginx.yml`

## Handlers {#Handlers}
{: .slide .w }

    ---
    - hosts: local
    tasks:
      - name: Install Nginx
        apt: pkg=nginx state=installed update_cache=true
        notify:
          - Start Nginx
    handlers:
      - name: Start Nginx
        service: name=nginx state=started

## Playbook More YAML

 - Vars
 - Tasks
 - Handlers
 - Roles
 - Files
 - Meta
 - Templates

## Playbook Directories

 - Group/Host Vars
 - Roles
 - Inventory Files
 - Libraries
 - Plugins
 - Playbook Files


## References

1. http://docs.ansible.com/ansible
2. https://serversforhackers.com/an-ansible-tutorial
3. http://wiki.glitchdata.com/index.php?title=Ansible_Training

## **Thanks**
