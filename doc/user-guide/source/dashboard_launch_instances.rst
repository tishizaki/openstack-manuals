===========================
Launch and manage instances
===========================
Instances are virtual machines that run inside the cloud. You can launch
an instance from the following sources:

-  Images uploaded to the OpenStack Image service.

-  Image that you have copied to a persistent volume. The instance
   launches from the volume, which is provided by the ``cinder-volume``
   API through iSCSI.

Launch an instance
~~~~~~~~~~~~~~~~~~

When you launch an instance from a volume, note the following steps:

-  To select the volume from which to launch, launch an instance from
   an arbitrary image on the volume. The arbitrary image that you select
   does not boot. Instead, it is replaced by the image on the volume that
   you choose in the next steps.

   To boot a Xen image from a volume, the image you launch in must be
   the same type, fully virtualized or paravirtualized, as the one on
   the volume.

-  Select the volume or volume snapshot from which to boot. Enter a
   device name. Enter ``vda`` for KVM images or ``xvda`` for Xen images.

When you launch an instance from an image, OpenStack creates a local
copy of the image on the compute node where the instance starts.

#. Log in to the dashboard, choose a project, and click :guilabel:`Images`.

   The dashboard shows the images that have been uploaded to OpenStack
   Image service and are available for this project.

   For details on creating images, see `Creating images
   manually <http://docs.openstack.org/image-guide/content/ch_creating_images_manually.html>`__
   in the *OpenStack Virtual Machine Image Guide*.

#. Select an image and click :guilabel:`Launch`.

#. In the :guilabel:`Launch Instance` dialog box, specify the following values:

   :guilabel:`Details` tab

   Availability Zone
      By default, this value is set to the availability zone given by the
      cloud provider (for example, ``us-west`` or ``apac-south``). For some
      cases, it could be ``nova``.

   Instance Name
      Assign a name to the virtual machine.

      .. note:: The name you assign here becomes the initial host name
         of the server.

         After the server is built, if you change the server name in the API
         or change the host name directly, the names are not updated in the
         dashboard.

         Server names are not guaranteed to be unique when created so you
         could have two instances with the same host name.

   Flavor
      Specify the size of the instance to launch.

      .. note:: The flavor is selected based on the size of the image selected
         for launching an instance. For example, while creating an image, if
         you have entered the value in the :guilabel:`Minimum RAM (MB)` field
         as 2048, then on selecting the image, the default flavor is
         ``m1.small``.

   Instance Count
      To launch multiple instances, enter a value greater than ``1``. The
      default is ``1``.

   Instance Boot Source
      Your options are:

      Boot from image
          If you choose this option, a new field for :guilabel:`Image Name`
          displays. You can select the image from the list.

      Boot from snapshot
          If you choose this option, a new field for :guilabel:`Instance
          Snapshot` displays. You can select the snapshot from the list.

      Boot from volume
          If you choose this option, a new field for :guilabel:`Volume`
          displays. You can select the volume from the list.

      Boot from image (creates a new volume)
          With this option, you can boot from an image and create a volume
          by entering the :guilabel:`Device Size` and :guilabel:`Device
          Name` for your volume. Click the :guilabel:`Delete on Terminate`
          option to delete the volume on terminating the instance.

      Boot from volume snapshot (creates a new volume)
          Using this option, you can boot from a volume snapshot and create
          a new volume by choosing :guilabel:`Volume Snapshot` from a list
          and adding a :guilabel:`Device Name` for your volume. Click the
          :guilabel:`Delete on Terminate` option to delete the volume on
          terminating the instance.

      Since you are launching an instance from an image, :guilabel:`Boot
      from image` is chosen by default.

   Image Name
      This field changes based on your previous selection. Since you have
      chosen to launch an instance using an image, the :guilabel:`Image Name`
      field displays. Select the image name from the dropdown list.

   :guilabel:`Access & Security` tab

   Keypair
      Specify a key pair.

      If the image uses a static root password or a static key set
      (neither is recommended), you do not need to provide a key pair
      to launch the instance.

   Security Groups
      Activate the security groups that you want to assign to the instance.

      Security groups are a kind of cloud firewall that define which
      incoming network traffic is forwarded to instances.

      If you have not created any security groups, you can assign
      only the default security group to the instance.

   :guilabel:`Networking` tab

   Selected Networks
      To add a network to the instance, click the :guilabel:`+` in the
      :guilabel:`Available Networks` field.

   :guilabel:`Post-Creation` tab

   Customization Script
      Specify a customization script that runs after your instance
      launches.

   :guilabel:`Advanced Options` tab

   Disk Partition
      Select the type of disk partition from the dropdown list:

      Automatic
          Entire disk is single partition and automatically resizes.

      Manual
          Faster build times but requires manual partitioning.

#. Click :guilabel:`Launch`.

   The instance starts on a compute node in the cloud.

The :guilabel:`Instances` tab shows the instance's name, its private
and public IP addresses, size, status, task, and power state.

If you did not provide a key pair, security groups, or rules, users can
access the instance only from inside the cloud through VNC. Even pinging
the instance is not possible without an ICMP rule configured.

Connect to your instance by using SSH
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To use SSH to connect to your instance, you use the downloaded keypair
file.

.. note:: The user name is ``ubuntu`` for the Ubuntu cloud images on TryStack.

#. Copy the IP address for your instance.

#. Use the :command:`ssh` command to make a secure connection to the instance.
   For example::

    $ ssh -i MyKey.pem ubuntu@10.0.0.2

#. At the prompt, type ``yes``.

Track usage for instances
~~~~~~~~~~~~~~~~~~~~~~~~~

You can track usage for instances for each project. You can track costs
per month by showing meters like number of vCPUs, disks, RAM, and
uptime for all your instances.

#. Log in to the dashboard, choose a project, and click :guilabel:`Overview`.

#. To query the instance usage for a month, select a month and click
   :guilabel:`Submit`.

#. To download a summary, click :guilabel:`Download CSV Summary`.

Create an instance snapshot
~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the dashboard, choose a project, and click :guilabel:`Instances`.

#. Select the instance from which to create a snapshot.

#. In the :guilabel:`Actions` column, click :guilabel:`Create Snapshot`.

#. In the :guilabel:`Create Snapshot` dialog box, enter a name for the
   snapshot, and click :guilabel:`Create Snapshot`.

   The Images category shows the instance snapshot.

To launch an instance from the snapshot, select the snapshot and click
:guilabel:`Launch`. Proceed with launching an instance.

Manage an instance
~~~~~~~~~~~~~~~~~~

#. Log in to the dashboard, choose a project, and click :guilabel:`Instances`.

#. Select an instance.

#. In the :guilabel:`More` list in the :guilabel:`Actions` column, select the
   state.

   You can resize or rebuild an instance. You can also choose to view
   the instance console log, edit instance or the security groups.
   Depending on the current state of the instance, you can pause,
   resume, suspend, soft or hard reboot, or terminate it.
