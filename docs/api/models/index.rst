.. currentmodule:: discord

.. _discord_api_models:

Discord Models
---------------

Models are classes that are received from Discord and are not meant to be created by
the user of the library.

.. danger::

    The classes listed below are **not intended to be created by users** and are also
    **read-only**.

    For example, this means that you should not make your own :class:`User` instances
    nor should you modify the :class:`User` instance yourself.

    If you want to get one of these model classes instances they'd have to be through
    the cache, and a common way of doing so is through the :func:`utils.find` function
    or attributes of model classes that you receive from the events specified in the
    :ref:`discord_api_events`.

.. note::

    Nearly all classes here have :ref:`py:slots` defined which means that it is
    impossible to have dynamic attributes to the data classes.

    
.. toctree::
    :maxdepth: 2

    clientuser
    relationship
    user
    attachment
    asset
    message
    reaction
    callmessage
    groupcall
    guild
    member
    spotify
    voicestate
    emoji
    partialemoji
    role
    textchannel
    voicechannel
    categorychannel
    dmchannel
    groupchannel
    partialinviteguild
    partialinvitechannel
    invite
    widgetchannel
    widgetmember
    widget
    rawmessagedeleteevent
    rawbulkmessagedeleteevent
    rawmessageupdateevent
    rawreactionactionevent
    rawreactionclearevent
