Ansible Docker Container
========================

An Ansible roles that creates a docker container with a data volume. This role uses the docker module to create the container.


Role Variables
--------------

Create the following structure to hold the variables that the role needs:


    # Our list of containers. An object using the name of the container as the index.
    containers:
      "test":
        # The docker image to be used.
        container_image: batandwa/baseimage
        # The command to be run when the container is started.
        container_command: /sbin/my_init --enable-insecure-key
        # The domain to be used assigned to the container
        container_domain: "dev5.batandwa.me"
        # The ports that will be exposed by the container
        container_ports: 
          - "2201:22"
          - 3306
          - 80
          - 1080
        # The container volumes with their corresponding host destinations with the host destination specfied first.
        container_volumes: 
          - "{{ lookup('env', 'PWD') }}/data/home:/home"
          - "{{ lookup('env', 'PWD') }}/data/tmp:/tmp"
        # Whether the container should expose all it's open ports.
        container_all_ports: no
        # The interface IP to use for the DNS. Set no to ignore.
        container_dns_interface: no
        # The socket or URL location for the docker host.
        container_docker_url: unix://var/run/docker.sock
        # Create a data-only container for this container.
        container_data_container: yes

    # A list of containers that should be removed.
    remove_cotainers:
      - dev
      - db1
      - load_balancer

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
