.. _block_storage:

=============
Block Storage
=============

This section lists the commands for interacting with Cloud Block Storage.

Commands
--------

All ``block-storage`` commands are based on this syntax::

   rack block-storage <subservice> <action> [command flags]

*Command flags* allow you to customize certain attributes of the command,
such as ``--name`` to name a volume. Type ``rack block-storage <subservice> <action> --help``
to bring up a list of *command flags* specific to the command.

**Volume**
~~~~~~~~~~

Volume commands use this syntax::

    rack block-storage volume <action> [optional flags]

``list``
^^^^^^^^
Retrieves a list of volumes::

    rack block-storage volume list [optional flags]

**Response**

.. code::

    $ rack block-storage volume list
    ID					                          Name	 Size	 Status		    Description	VolumeType	SnapshotID
    81c7a7e5-01a5-44bb-9b43-0cc9f7c4e423		     75	   available		            SATA
    a7c97db7-a0d3-495b-9ba3-1cb9dd9cf12c	Store1	 75	   in-use			            	SATA
    ca50fdfd-21f2-47e9-8ede-1518cb7467af	Store2  150	 in-use				            SSD

``create``
^^^^^^^^^^
Creates a volume::

    rack block-storage volume create --size <volumeSize> [optional flags]

**Response**

.. code::

    $ rack block-storage volume create --size 75 --name Response
    ID		66dcbe53-1b62-4a15-adc2-e46e78b95f8b
    Name		Response
    Description
    Size		75
    VolumeType	SATA
    SnapshotID
    Attachments	[]
    CreatedAt	2015-08-05T19:48:28.000000

``get``
^^^^^^^
Retrieves details on a specified volume::

    rack block-storage volume get --id <volumeID> [optional flags]
    rack block-storage volume get --name <volumeName> [optional flags]
    (echo volumeID1 && echo volumeID2) | rack block-storage volume get --stdin id [optional flags]

**Response**

.. code::

    $ rack block-storage volume get --name Response
    ID		66dcbe53-1b62-4a15-adc2-e46e78b95f8b
    Name		Response
    Description
    Size		75
    VolumeType	SATA
    SnapshotID
    Attachments	[]
    CreatedAt	2015-08-05T19:48:28.000000


``update``
^^^^^^^^^^
Updates the name and description of a volume::

    rack block-storage volume update --id <volumeID> [optional flags]
    rack block-storage volume update --name <volumeName> [optional flags]


``delete``
^^^^^^^^^^
Permanently deletes a volume::

    rack block-storage volume delete --id <volumeID> [optional flags]
    rack block-storage volume delete --name <volumeName> [optional flags]
    (echo volumeID1 && echo volumeID2) | rack block-storage volume delete --stdin id [optional flags]

**Response**

.. code::

    $ rack block-storage volume delete --name Response
    Deleting volume [66dcbe53-1b62-4a15-adc2-e46e78b95f8b]

**Snapshot**
~~~~~~~~~~~~

Snapshot commands use this syntax::

    rack block-storage snapshot <actions> [optional flags]

``list``
^^^^^^^^
Retrieves a list of snapshots::

    rack block-storage snapshot list [optional flags]

**Response**

.. code::

    $ rack block-storage snapshot list
    ID				                          	Name	Size	Status		VolumeID				                      VolumeType	SnapshotID	Bootable
    180a6c5c-ad6d-4cb6-846f-d500d67e59a5		    75	  available	81c7a7e5-01a5-44bb-9b43-0cc9f7c4e423

``create``
^^^^^^^^^^
Creates a snapshot based on a specified volume id::

    rack block-storage snapshot create --volume-id <volumeID> [optional flags]

**Response**

.. code::

    $ rack block-storage snapshot create --volume-id 66dcbe53-1b62-4a15-adc2-e46e78b95f8b --name Snapshot1
    ID		4aa6ae9b-9b1d-4870-9192-8da72df7473e
    Name		Snapshot1
    Description
    Size		75
    VolumeType
    SnapshotID
    Attachments
    CreatedAt	2015-08-05T20:57:56.604914

``get``
^^^^^^^
Retrieves details on a specified snapshot::

    rack block-storage snapshot get --id <snapshotID> [optional flags]
    rack block-storage snapshot get --name <snapshotName>] [optional flags]
    (echo snapshotID1 && echo snapshotID2) | rack block-storage snapshot get --stdin id [optional flags]

**Response**

.. code::

    $ rack block-storage snapshot get --name Snapshot1
    ID		4aa6ae9b-9b1d-4870-9192-8da72df7473e
    Name		Snapshot1
    Size		75
    Status		creating
    VolumeID	66dcbe53-1b62-4a15-adc2-e46e78b95f8b
    VolumeType
    SnapshotID
    Bootable
    Attachments


``delete``
^^^^^^^^^^
Permanently deletes a snapshot::

    rack block-storage snapshot delete --id <snapshotID> [optional flags]
    rack block-storage snapshot delete --name <snapshotName> [optional flags]
    (echo snapshotID1 && echo snapshotID2) | rack block-storage snapshot delete --stdin id [optional flags]

**Response**

.. code::

    $ rack block-storage snapshot delete --name Snapshot1
    Deleting snapshot [4aa6ae9b-9b1d-4870-9192-8da72df7473e]
