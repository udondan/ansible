.. _developing_modules:

Developing Modules
==================

.. contents:: Topics

.. _module_dev_welcome:

Welcome
```````
This section discusses how to develop, debug, review, and test modules.


Ansible modules are reusable, standalone scripts that can be used by the Ansible API,
or by the :command:`ansible` or :command:`ansible-playbook` programs.  They
return information to ansible by printing a JSON string to stdout before
exiting.  They take arguments in one of several ways which we'll go into
as we work through this tutorial.

See :ref:`all_modules` for a list of existing modules.

Modules can be written in any language and are found in the path specified
by :envvar:`ANSIBLE_LIBRARY` or the ``--module-path`` command line option or
in the :envvar:`library section of the Ansible configuration file <ANSIBLE_LIBRARY>`.

.. _module_dev_should_you:

Should You Develop A Module?
````````````````````````````
Before diving into the work of creating a new module, you should think about whether you actually *should*
develop a module. Ask the following questions:

1. Does a similar module already exist?

There are a lot of existing modules available, you should check out the list of existing modules at :ref:`modules`

2. Has someone already worked on a similar Pull Request?

It's possible that someone has already started developing a similar PR. There are a few ways to find open module Pull Requests:

* `GitHub new module PRs <https://github.com/ansible/ansible/labels/new_module>`_
* `All updates to modules <https://github.com/ansible/ansible/labels/module>`_
* `New module PRs listed by directory <https://ansible.sivel.net/pr/byfile.html>`_ search for `lib/ansible/modules/`

If you find an existing PR that looks like it addresses the issue you are trying to solve, please provide feedback on the PR -  this will speed up getting the PR merged.

3. Should you use or develop an action plugin instead?

Action plugins get run on the master instead of on the target. For modules like file/copy/template, some of the work needs to be done on the master before the module executes on the target. Action plugins execute first on the master and can then execute the normal module on the target if necessary.

For more information about action plugins, read the :ref:`action plugins documentation <developing_plugins>`.

4. Should you use a role instead?

Check out the :ref:`roles documentation<playbooks_reuse_roles>`.

5. Should you write multiple modules instead of one module?

The following guidelines will help you determine if your module attempts to do too much, and should likely be broken into several smaller modules.

* Modules should have a concise and well defined functionality. Basically, follow the UNIX philosophy of doing one thing well.

* Modules should not require that a user know all the underlying options of an api/tool to be used. For instance, if the legal values for a required module parameter cannot be documented, that's a sign that the module would be rejected.

* Modules should typically encompass much of the logic for interacting with a resource. A lightweight wrapper around an API that does not contain much logic would likely cause users to offload too much logic into a playbook, and for this reason the module would be rejected. Instead try creating multiple modules for interacting with smaller individual pieces of the API.


.. _developing_modules_all:

How To Develop A Module
```````````````````````

The following topics will discuss how to develop and work with modules:

:doc:`developing_program_flow_modules`
    A description of Ansible's module architecture.
:doc:`developing_modules_general`
    A general overview of how to develop, debug, and test modules.
:doc:`developing_modules_general_windows`
    A general overview of how to develop, debug and test Windows modules.
:doc:`developing_modules_documenting`
    How to include in-line documentation in your module.
:doc:`developing_modules_best_practices`
    Best practices, recommendations, and things to avoid.
:doc:`developing_modules_checklist`
     Checklist for contributing your module to Ansible.
:doc:`testing`
    Developing unit and integration tests.
:doc:`developing_python3`
    Adding Python 3 support to modules (all new modules must be Python-2.6 and Python-3.5 compatible).
:doc:`developing_modules_in_groups`
    A guide for partners wanting to submit multiple modules.


.. seealso::

   :ref:`all_modules`
       Learn about available modules
   :doc:`developing_plugins`
       Learn about developing plugins
   :doc:`developing_api`
       Learn about the Python API for playbook and task execution
   `GitHub modules directory <https://github.com/ansible/ansible/tree/devel/lib/ansible/modules>`_
       Browse module source code
   `Mailing List <http://groups.google.com/group/ansible-devel>`_
       Development mailing list
   `irc.freenode.net <http://irc.freenode.net>`_
       #ansible IRC chat channel

