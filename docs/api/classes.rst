.. currentmodule:: discord

.. _classes:

.. _discord_api_data:

Data Classes
--------------

Some classes are just there to be data containers, this lists them.

Unlike :ref:`models <discord_api_models>` you are allowed to create
these yourself, even if they can also be used to hold attributes.

Nearly all classes here have :ref:`py:slots` defined which means that it is
impossible to have dynamic attributes to the data classes.

The only exception to this rule is :class:`abc.Snowflake`, which is made with
dynamic attributes in mind.


Object
~~~~~~~

.. autoclass:: Object
    :members:

Embed
~~~~~~

.. autoclass:: Embed
    :members:

File
~~~~~

.. autoclass:: File
    :members:

Colour
~~~~~~

.. autoclass:: Colour
    :members:

Activity
~~~~~~~~~

.. autoclass:: Activity
    :members:

Game
~~~~~

.. autoclass:: Game
    :members:

Streaming
~~~~~~~~~~~

.. autoclass:: Streaming
    :members:

Permissions
~~~~~~~~~~~~

.. autoclass:: Permissions
    :members:

PermissionOverwrite
~~~~~~~~~~~~~~~~~~~~

.. autoclass:: PermissionOverwrite
    :members:

SystemChannelFlags
~~~~~~~~~~~~~~~~~~~~

.. autoclass:: SystemChannelFlags
    :members:
