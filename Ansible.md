# ANSIBLE 
1.  Initializing inventory
    * inventory file

        {{{inventory
                192.168.1.20

                [database]
                192.168.1.21
                192.168.1.22

                [network]
                192.168.1.22
        }}}


    * Setting SSH keys
2.  Playbook

        {{{playbook
                #Start a playbook
                ---
                #First play
                - hosts: webservers
                  remote_user: root

                  tasks:
                  - name: ensure apache is at the latest version
                    yum: name=httpd state=latest
                  - name: write the apache config file
                    template: src=/srv/httpd.j2 dest=/etc/httpd.conf

                #Second play
                - hosts: databases  #Hosts to provision
                  remote_user: root #account used to provision

                  tasks:
                  - name: ensure postgresql is at the latest version
                    yum: name=postgresql state=latest
                  - name: ensure that postgresql is started
                    service: name=postgresql state=started
        }}}


3. Handlers


