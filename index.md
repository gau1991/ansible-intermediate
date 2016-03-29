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

    #Inventory2 p {
        margin:0 0 15px;
        line-height:25px;
        }
    #Inventory2 code {
        margin:0 0 0;
        line-height:25px;
        }


---

# Ansible for Intermediates {#Cover}

*Brought you by [Gaurav Ashtikar](http://gau1991.me/)*

![](pictures/cover.jpg)
<!-- photo by WikiPedia, https://en.wikipedia.org/wiki/Server_%28computing%29#/media/File:Wikimedia_Foundation_Servers-8055_35.jpg CC BY-SA 3.0 -->


## Contents

  1. More about Inventory
  2. Become
  3. Vault
  4. More into Playbook
  5. Complex Playbook Example - WordPress & Nginx on CentOS-7 system

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

## More about Inventory {#Inventory2}
<b>Splitting Out Host and Group Specific Data</b>

    /etc/ansible/group_vars/raleigh
    /etc/ansible/group_vars/webservers
    /etc/ansible/host_vars/foosball

OR

    /etc/ansible/group_vars/raleigh/db_settings
    /etc/ansible/group_vars/raleigh/cluster_settings


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

## Vault
  - Creating Encrypted Files
    - `$ansible-vault create foo.yml`
  - Editing Encrypted Files
    - `$ansible-vault edit foo.yml`
  - Rekeying Encrypted Files
    - `$ansible-vault rekey foo.yml`

## Vault

  - Encrypting Unencrypted Files
    - `$ansible-vault encrypt foo.yml`
  - Decrypting Encrypted Files
    - `$ansible-vault decrypt foo.yml`
  - Viewing Encrypted Files
    - `ansible-vault view foo.yml`

## Running a Playbook With Vault
  - `$ansible-playbook site.yml --ask-vault-pass`
  - `$ansible-playbook site.yml --vault-password-file ~/.vault_pass.txt`
  -  Setting ENV Variable `ANSIBLE_VAULT_PASSWORD_FILE`

## More into Playbook

 - Vars
 - Tasks
 - Handlers
 - Roles
 - Files
 - Meta
 - Templates

## Complex Playbook Example - WordPress & Nginx on CentOS-7 system

[Demo Time](https://github.com/ansible/ansible-examples/tree/master/wordpress-nginx_rhel7)

## References

1. http://docs.ansible.com/ansible
2. https://serversforhackers.com/an-ansible-tutorial
3. http://wiki.glitchdata.com/index.php?title=Ansible_Training

## **Thanks**
