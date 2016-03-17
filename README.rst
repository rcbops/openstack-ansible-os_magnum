OpenStack-Ansible Magnum
#######################
:tags: openstack, magnum, cloud, ansible
:category: \*nix

This Ansible role installs and configures OpenStack Magnum.

Default Variables
=================

.. literalinclude:: ../../defaults/main.yml
   :language: yaml
   :start-after: under the License.

Required Variables
==================

magnum_service_password
magnum_galera_password
magnum_rabbitmq_password

Example Playbook
================

.. code-block:: yaml

   - name: Install magnum server
     hosts: magnum_all
     user: root
     roles:
       - role: "os_magnum"
     vars:
       external_lb_vip_address: 172.16.24.1
       internal_lb_vip_address: 192.168.0.1
       magnum_galera_address: "{{ internal_lb_vip_address }}"
