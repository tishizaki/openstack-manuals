=============
Manage quotas
=============

To prevent system capacities from being exhausted without
notification, you can set up quotas. Quotas are operational
limits. For example, the number of gigabytes allowed for each
tenant can be controlled so that cloud resources are optimized.
Quotas can be enforced at both the tenant (or project)
and the tenant-user level.

Using the command-line interface, you can manage quotas for
the OpenStack Compute service, the OpenStack Block Storage service,
and the OpenStack Networking service.

The cloud operator typically changes default values because a
tenant requires more than ten volumes or 1 TB on a compute
node.

.. note::
   To view all tenants (projects), run::

    $ openstack project list
     +----------------------------------+----------+
     | ID                               | Name     |
     +----------------------------------+----------+
     | e66d97ac1b704897853412fc8450f7b9 | admin    |
     | bf4a37b885fe46bd86e999e50adad1d3 | services |
     | 21bd1c7c95234fd28f589b60903606fa | tenant01 |
     | f599c5cd1cba4125ae3d7caed08e288c | tenant02 |
     +----------------------------------+----------+

   To display all current users for a tenant, run::

    $ openstack user list --project PROJECT_NAME
     +----------------------------------+--------+
     | ID                               | Name   |
     +----------------------------------+--------+
     | ea30aa434ab24a139b0e85125ec8a217 | demo00 |
     | 4f8113c1d838467cad0c2f337b3dfded | demo01 |
     +----------------------------------+--------+


.. toctree::
   :maxdepth: 2

   cli_set_compute_quotas.rst
   cli_cinder_quotas.rst
   networking_advanced_quotas.rst
