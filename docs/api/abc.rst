.. currentmodule:: discord

.. _abc:

Abstract Base Classes
-----------------------

An :term:`py:abstract base class` (also known as an ``abc``) is a class that models can inherit
to get their behaviour. The Python implementation of an :doc:`abc <py:library/abc>` is
slightly different in that you can register them at run-time. **Abstract base classes cannot be instantiated**.
They are mainly there for usage with :func:`py:isinstance` and :func:`py:issubclass`\.

This library has a module related to abstract base classes, some of which are actually from the :doc:`abc <py:library/abc>` standard
module, others which are not.

.. autoclass:: discord.abc.Snowflake
    :members:

.. autoclass:: discord.abc.User
    :members:

.. autoclass:: discord.abc.PrivateChannel
    :members:

.. autoclass:: discord.abc.GuildChannel
    :members:

.. autoclass:: discord.abc.Messageable
    :members:
    :exclude-members: history, typing

    .. autocomethod:: discord.abc.Messageable.history
        :async-for:

    .. autocomethod:: discord.abc.Messageable.typing
        :async-with:

.. autoclass:: discord.abc.Connectable
