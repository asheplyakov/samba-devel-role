=======================================================
ansible_ roles for Samba developement environment setup
=======================================================

Synopsis
========

* Purpose: quickly setup environment for hacking Samba_
* Inputs:

  - (virtual) machine(s) running Fedora
  - (local) username, ssh public key

* Result: (virtual) machine(s) ready to compile Samba_ code

.. _Samba: https://www.samba.org
.. _ansible: https://www.ansible.com

Prerequisites
=============

* (virtual) machines running supported Linux distro (Fedora)
* ssh root access to these machines
* control machine
  
  - running Linux 
  - with ansible installed


Usage
=====

#. Clone this repository::

     git clone git://github.com/asheplyakov/samba-devel-role
     cd samba-devel-role

#. Enumerate machines in the ``hosts`` file::

     cp hosts.sample hosts
     vi hosts

#. Check if the machine are reachable via ssh::

     ansible -i hosts -m ping all

#. Run the playbook::

     ansible-playbook -i hosts setup.yml

   This installs the required packages, creates a user account
   named after a local one. The newly created user is allowed to
   run ``sudo`` without a password.

Next steps
==========

#. Login to machine using your local username::

     ssh -Y -o ForwardAgent=yes development.host.ip

#. Clone Samba_ repository (or your own fork)::

     git clone https://github.com/samba-team/samba.git

#. Compile it::

     cd samba
     ./configure.developer
     ./buildtools/bin/waf

Happy hacking!
