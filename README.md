Ansible Docker Container
========================

An Ansible roles that creates a docker container with a data volume. This role uses the docker module to create the container.


Role Variables
--------------

Create the following structure to hold the variables that the role needs:

    container:
      # The docker image to be used.
      container_image: ubuntu 
      # The container will be given this name and the data volume will use the same name suffixed with *_data*.
      container_name: sample_container 
      # The command to be run when the container is started.
      container_command: /bin/bash
      # The domain to be used assigned to the container
      container_domain: example.com
      # The ports that will be exposed by the container
      container_ports: 80,22
      # The container volumes with their corresponding host destinations with the host destination specfied first.
      container_volumes: 
        - "{{ cwd_path }}/data/home:/home"
        - "{{ cwd_path }}/data/tmp:/tmp"
      # Whether the container should expose all it's open ports.
      container_all_ports: no
      # Whether the container should be destroyed and recreated whenever this roles is executed. This excludes the data container.
      container_kill_existing: no


Example Playbook
-------------------------

Create a *variables.yml* file with the variables as above and add the following to your playbook.

    - hosts: local
      remote_user: root
      vars_files:
        - variables.yml
      roles:
        - ansible-docker-container


License
-------

GPL v2
