## Vagrant local tests for ansible playbooks and roles


### Used versions:
* On the host:
  - Vagrant 2.2.13
  - Ansible 2.9.6
* On instances:
  - Application code https://github.com/express42/reddit
  - Ruby 2.3.8 (required by this version of the application)
  - MongoDB 4.4

* Firewall rules to open ports:
  - 22     SSH connection
  - 9292   Application work port
  - 27017  Database connection
  - 80     HTTP port

### Steps:

#### To manage instances:
  ```
  vagrant up        # to create instances
  vagrant provision # to run ansible test
  vagrant halt      # to power off instances
  vagrant destroy   # to remove instances
    ```