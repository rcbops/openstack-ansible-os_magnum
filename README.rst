OpenStack-Ansible Magnum
########################

Ansible role that installs and configures OpenStack Magnum. Magnum is
installed behind the Apache webserver listening on port 9511 by default.

.. literalinclude:: ../../defaults/main.yml
   :language: yaml
   :start-after: under the License.

Required Variables
==================

This list is not exhaustive at present. See role internals for further
details.

.. code-block:: yaml

    # Magnum TCP listening port
    magnum_service_port: 9511

    # Magnum service protocol http or https
    magnum_service_proto: http

    # Magnum Galera address of internal load balancer
    magnum_galera_address: "{{ internal_lb_vip_address }}"

    # Magnum Galera database name
    magnum_galera_database_name: magnum_service

    # Magnum Galera username
    magnum_galera_user: magnum

    # Magnum rabbit userid
    magnum_rabbitmq_userid: magnum

    # Magnum rabbit vhost
    magnum_rabbitmq_vhost: /magnum

Example Playbook
================

.. code-block:: yaml

   - name: Install magnum server
     hosts: magnum_all
     user: root
     roles:
        - { role: "os_magnum", tags: [ "os-magnum" ] }
     vars:
       magnum_galera_address: "{{ internal_lb_vip_address }}"
       magnum_galera_database_name: magnum_service
       magnum_galera_user: magnum
       magnum_rabbitmq_userid: magnum
       magnum_rabbitmq_vhost: /magnum
       ansible_hostname: "{{ container_name }}"
       is_metal: "{{ properties.is_metal|default(false) }}"

Tags
====

This role supports two tags: ``magnum-install`` and ``magnum-config``.

The ``magnum-install`` tag can be used to install and upgrade.

The ``magnum-config`` tag can be used to maintain configuration of the
service.
