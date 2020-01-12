.. currentmodule:: discord

.. _discord_api_events:

Event Reference
---------------

This page outlines the different types of events listened by :class:`Client`.

There are two ways to register an event, the first way is through the use of
:meth:`Client.event`. The second way is through subclassing :class:`Client` and
overriding the specific events. For example: ::

    import discord

    class MyClient(discord.Client):
        async def on_message(self, message):
            if message.author == self.user:
                return

            if message.content.startswith('$hello'):
                await message.channel.send('Hello World!')


If an event handler raises an exception, :func:`on_error` will be called
to handle it, which defaults to print a traceback and ignoring the exception.

.. warning::

    All the events must be a |coroutine_link|_. If they aren't, then you might get unexpected
    errors. In order to turn a function into a coroutine they must be ``async def``
    functions.

.. function:: on_connect()

    Called when the client has successfully connected to Discord. This is not
    the same as the client being fully prepared, see :func:`on_ready` for that.

    The warnings on :func:`on_ready` also apply.

.. function:: on_disconnect()

    Called when the client has disconnected from Discord. This could happen either through
    the internet being disconnected, explicit calls to logout, or Discord terminating the connection
    one way or the other.

    This function can be called many times.

.. function:: on_ready()

    Called when the client is done preparing the data received from Discord. Usually after login is successful
    and the :attr:`Client.guilds` and co. are filled up.

    .. warning::

        This function is not guaranteed to be the first event called.
        Likewise, this function is **not** guaranteed to only be called
        once. This library implements reconnection logic and thus will
        end up calling this event whenever a RESUME request fails.

.. function:: on_shard_ready(shard_id)

    Similar to :func:`on_ready` except used by :class:`AutoShardedClient`
    to denote when a particular shard ID has become ready.

    :param shard_id: The shard ID that is ready.
    :type shard_id: :class:`int`

.. function:: on_resumed()

    Called when the client has resumed a session.

.. function:: on_error(event, \*args, \*\*kwargs)

    Usually when an event raises an uncaught exception, a traceback is
    printed to stderr and the exception is ignored. If you want to
    change this behaviour and handle the exception for whatever reason
    yourself, this event can be overridden. Which, when done, will
    suppress the default action of printing the traceback.

    The information of the exception raised and the exception itself can
    be retrieved with a standard call to :func:`sys.exc_info`.

    If you want exception to propagate out of the :class:`Client` class
    you can define an ``on_error`` handler consisting of a single empty
    :ref:`py:raise`.  Exceptions raised by ``on_error`` will not be
    handled in any way by :class:`Client`.

    :param event: The name of the event that raised the exception.
    :type event: :class:`str`

    :param args: The positional arguments for the event that raised the
        exception.
    :param kwargs: The keyword arguments for the event that raised the
        exception.

.. function:: on_socket_raw_receive(msg)

    Called whenever a message is received from the WebSocket, before
    it's processed. This event is always dispatched when a message is
    received and the passed data is not processed in any way.

    This is only really useful for grabbing the WebSocket stream and
    debugging purposes.

    .. note::

        This is only for the messages received from the client
        WebSocket. The voice WebSocket will not trigger this event.

    :param msg: The message passed in from the WebSocket library.
                Could be :class:`bytes` for a binary message or :class:`str`
                for a regular message.
    :type msg: Union[:class:`bytes`, :class:`str`]

.. function:: on_socket_raw_send(payload)

    Called whenever a send operation is done on the WebSocket before the
    message is sent. The passed parameter is the message that is being
    sent to the WebSocket.

    This is only really useful for grabbing the WebSocket stream and
    debugging purposes.

    .. note::

        This is only for the messages received from the client
        WebSocket. The voice WebSocket will not trigger this event.

    :param payload: The message that is about to be passed on to the
                    WebSocket library. It can be :class:`bytes` to denote a binary
                    message or :class:`str` to denote a regular text message.

.. function:: on_typing(channel, user, when)

    Called when someone begins typing a message.

    The ``channel`` parameter can be a :class:`abc.Messageable` instance.
    Which could either be :class:`TextChannel`, :class:`GroupChannel`, or
    :class:`DMChannel`.

    If the ``channel`` is a :class:`TextChannel` then the ``user`` parameter
    is a :class:`Member`, otherwise it is a :class:`User`.

    :param channel: The location where the typing originated from.
    :type channel: :class:`abc.Messageable`
    :param user: The user that started typing.
    :type user: Union[:class:`User`, :class:`Member`]
    :param when: When the typing started as a naive datetime in UTC.
    :type when: :class:`datetime.datetime`

.. function:: on_message(message)

    Called when a :class:`Message` is created and sent.

    .. warning::

        Your bot's own messages and private messages are sent through this
        event. This can lead cases of 'recursion' depending on how your bot was
        programmed. If you want the bot to not reply to itself, consider
        checking the user IDs. Note that :class:`~ext.commands.Bot` does not
        have this problem.

    :param message: The current message.
    :type message: :class:`Message`

.. function:: on_message_delete(message)

    Called when a message is deleted. If the message is not found in the
    internal message cache, then this event will not be called.
    Messages might not be in cache if the message is too old
    or the client is participating in high traffic guilds.

    If this occurs increase the :attr:`Client.max_messages` attribute.

    :param message: The deleted message.
    :type message: :class:`Message`

.. function:: on_bulk_message_delete(messages)

    Called when messages are bulk deleted. If none of the messages deleted
    are found in the internal message cache, then this event will not be called.
    If individual messages were not found in the internal message cache,
    this event will still be called, but the messages not found will not be included in
    the messages list. Messages might not be in cache if the message is too old
    or the client is participating in high traffic guilds.

    If this occurs increase the :attr:`Client.max_messages` attribute.

    :param messages: The messages that have been deleted.
    :type messages: List[:class:`Message`]

.. function:: on_raw_message_delete(payload)

    Called when a message is deleted. Unlike :func:`on_message_delete`, this is
    called regardless of the message being in the internal message cache or not.

    If the message is found in the message cache,
    it can be accessed via :attr:`RawMessageDeleteEvent.cached_message`

    :param payload: The raw event payload data.
    :type payload: :class:`RawMessageDeleteEvent`

.. function:: on_raw_bulk_message_delete(payload)

    Called when a bulk delete is triggered. Unlike :func:`on_bulk_message_delete`, this is
    called regardless of the messages being in the internal message cache or not.

    If the messages are found in the message cache,
    they can be accessed via :attr:`RawBulkMessageDeleteEvent.cached_messages`

    :param payload: The raw event payload data.
    :type payload: :class:`RawBulkMessageDeleteEvent`

.. function:: on_message_edit(before, after)

    Called when a :class:`Message` receives an update event. If the message is not found
    in the internal message cache, then these events will not be called.
    Messages might not be in cache if the message is too old
    or the client is participating in high traffic guilds.

    If this occurs increase the :attr:`Client.max_messages` attribute.

    The following non-exhaustive cases trigger this event:

    - A message has been pinned or unpinned.
    - The message content has been changed.
    - The message has received an embed.

        - For performance reasons, the embed server does not do this in a "consistent" manner.

    - A call message has received an update to its participants or ending time.

    :param before: The previous version of the message.
    :type before: :class:`Message`
    :param after: The current version of the message.
    :type after: :class:`Message`

.. function:: on_raw_message_edit(payload)

    Called when a message is edited. Unlike :func:`on_message_edit`, this is called
    regardless of the state of the internal message cache.

    If the message is found in the message cache,
    it can be accessed via :attr:`RawMessageUpdateEvent.cached_message`

    Due to the inherently raw nature of this event, the data parameter coincides with
    the raw data given by the `gateway <https://discordapp.com/developers/docs/topics/gateway#message-update>`_.

    Since the data payload can be partial, care must be taken when accessing stuff in the dictionary.
    One example of a common case of partial data is when the ``'content'`` key is inaccessible. This
    denotes an "embed" only edit, which is an edit in which only the embeds are updated by the Discord
    embed server.

    :param payload: The raw event payload data.
    :type payload: :class:`RawMessageUpdateEvent`

.. function:: on_reaction_add(reaction, user)

    Called when a message has a reaction added to it. Similar to :func:`on_message_edit`,
    if the message is not found in the internal message cache, then this
    event will not be called.

    .. note::

        To get the :class:`Message` being reacted, access it via :attr:`Reaction.message`.

    :param reaction: The current state of the reaction.
    :type reaction: :class:`Reaction`
    :param user: The user who added the reaction.
    :type user: Union[:class:`Member`, :class:`User`]

.. function:: on_raw_reaction_add(payload)

    Called when a message has a reaction added. Unlike :func:`on_reaction_add`, this is
    called regardless of the state of the internal message cache.

    :param payload: The raw event payload data.
    :type payload: :class:`RawReactionActionEvent`

.. function:: on_reaction_remove(reaction, user)

    Called when a message has a reaction removed from it. Similar to on_message_edit,
    if the message is not found in the internal message cache, then this event
    will not be called.

    .. note::

        To get the message being reacted, access it via :attr:`Reaction.message`.

    :param reaction: The current state of the reaction.
    :type reaction: :class:`Reaction`
    :param user: The user who added the reaction.
    :type user: Union[:class:`Member`, :class:`User`]

.. function:: on_raw_reaction_remove(payload)

    Called when a message has a reaction removed. Unlike :func:`on_reaction_remove`, this is
    called regardless of the state of the internal message cache.

    :param payload: The raw event payload data.
    :type payload: :class:`RawReactionActionEvent`

.. function:: on_reaction_clear(message, reactions)

    Called when a message has all its reactions removed from it. Similar to :func:`on_message_edit`,
    if the message is not found in the internal message cache, then this event
    will not be called.

    :param message: The message that had its reactions cleared.
    :type message: :class:`Message`
    :param reactions: The reactions that were removed.
    :type reactions: List[:class:`Reaction`]

.. function:: on_raw_reaction_clear(payload)

    Called when a message has all its reactions removed. Unlike :func:`on_reaction_clear`,
    this is called regardless of the state of the internal message cache.

    :param payload: The raw event payload data.
    :type payload: :class:`RawReactionClearEvent`

.. function:: on_private_channel_delete(channel)
              on_private_channel_create(channel)

    Called whenever a private channel is deleted or created.

    :param channel: The private channel that got created or deleted.
    :type channel: :class:`abc.PrivateChannel`

.. function:: on_private_channel_update(before, after)

    Called whenever a private group DM is updated. e.g. changed name or topic.

    :param before: The updated group channel's old info.
    :type before: :class:`GroupChannel`
    :param after: The updated group channel's new info.
    :type after: :class:`GroupChannel`

.. function:: on_private_channel_pins_update(channel, last_pin)

    Called whenever a message is pinned or unpinned from a private channel.

    :param channel: The private channel that had its pins updated.
    :type channel: :class:`abc.PrivateChannel`
    :param last_pin: The latest message that was pinned as a naive datetime in UTC. Could be ``None``.
    :type last_pin: Optional[:class:`datetime.datetime`]

.. function:: on_guild_channel_delete(channel)
              on_guild_channel_create(channel)

    Called whenever a guild channel is deleted or created.

    Note that you can get the guild from :attr:`~abc.GuildChannel.guild`.

    :param channel: The guild channel that got created or deleted.
    :type channel: :class:`abc.GuildChannel`

.. function:: on_guild_channel_update(before, after)

    Called whenever a guild channel is updated. e.g. changed name, topic, permissions.

    :param before: The updated guild channel's old info.
    :type before: :class:`abc.GuildChannel`
    :param after: The updated guild channel's new info.
    :type after: :class:`abc.GuildChannel`

.. function:: on_guild_channel_pins_update(channel, last_pin)

    Called whenever a message is pinned or unpinned from a guild channel.

    :param channel: The guild channel that had its pins updated.
    :type channel: :class:`abc.GuildChannel`
    :param last_pin: The latest message that was pinned as a naive datetime in UTC. Could be ``None``.
    :type last_pin: Optional[:class:`datetime.datetime`]

.. function:: on_guild_integrations_update(guild)

    Called whenever an integration is created, modified, or removed from a guild.

    :param guild: The guild that had its integrations updated.
    :type guild: :class:`Guild`

.. function:: on_webhooks_update(channel)

    Called whenever a webhook is created, modified, or removed from a guild channel.

    :param channel: The channel that had its webhooks updated.
    :type channel: :class:`abc.GuildChannel`

.. function:: on_member_join(member)
              on_member_remove(member)

    Called when a :class:`Member` leaves or joins a :class:`Guild`.

    :param member: The member who joined or left.
    :type member: :class:`Member`

.. function:: on_member_update(before, after)

    Called when a :class:`Member` updates their profile.

    This is called when one or more of the following things change:

    - status
    - game playing
    - nickname
    - roles

    :param before: The updated member's old info.
    :type before: :class:`Member`
    :param after: The updated member's updated info.
    :type after: :class:`Member`

.. function:: on_user_update(before, after)

    Called when a :class:`User` updates their profile.

    This is called when one or more of the following things change:

    - avatar
    - username
    - discriminator

    :param before: The updated user's old info.
    :type before: :class:`User`
    :param after: The updated user's updated info.
    :type after: :class:`User`

.. function:: on_guild_join(guild)

    Called when a :class:`Guild` is either created by the :class:`Client` or when the
    :class:`Client` joins a guild.

    :param guild: The guild that was joined.
    :type guild: :class:`Guild`

.. function:: on_guild_remove(guild)

    Called when a :class:`Guild` is removed from the :class:`Client`.

    This happens through, but not limited to, these circumstances:

    - The client got banned.
    - The client got kicked.
    - The client left the guild.
    - The client or the guild owner deleted the guild.

    In order for this event to be invoked then the :class:`Client` must have
    been part of the guild to begin with. (i.e. it is part of :attr:`Client.guilds`)

    :param guild: The guild that got removed.
    :type guild: :class:`Guild`

.. function:: on_guild_update(before, after)

    Called when a :class:`Guild` updates, for example:

    - Changed name
    - Changed AFK channel
    - Changed AFK timeout
    - etc

    :param before: The guild prior to being updated.
    :type before: :class:`Guild`
    :param after: The guild after being updated.
    :type after: :class:`Guild`

.. function:: on_guild_role_create(role)
              on_guild_role_delete(role)

    Called when a :class:`Guild` creates or deletes a new :class:`Role`.

    To get the guild it belongs to, use :attr:`Role.guild`.

    :param role: The role that was created or deleted.
    :type role: :class:`Role`

.. function:: on_guild_role_update(before, after)

    Called when a :class:`Role` is changed guild-wide.

    :param before: The updated role's old info.
    :type before: :class:`Role`
    :param after: The updated role's updated info.
    :type after: :class:`Role`

.. function:: on_guild_emojis_update(guild, before, after)

    Called when a :class:`Guild` adds or removes :class:`Emoji`.

    :param guild: The guild who got their emojis updated.
    :type guild: :class:`Guild`
    :param before: A list of emojis before the update.
    :type before: List[:class:`Emoji`]
    :param after: A list of emojis after the update.
    :type after: List[:class:`Emoji`]

.. function:: on_guild_available(guild)
              on_guild_unavailable(guild)

    Called when a guild becomes available or unavailable. The guild must have
    existed in the :attr:`Client.guilds` cache.

    :param guild: The :class:`Guild` that has changed availability.

.. function:: on_voice_state_update(member, before, after)

    Called when a :class:`Member` changes their :class:`VoiceState`.

    The following, but not limited to, examples illustrate when this event is called:

    - A member joins a voice channel.
    - A member leaves a voice channel.
    - A member is muted or deafened by their own accord.
    - A member is muted or deafened by a guild administrator.

    :param member: The member whose voice states changed.
    :type member: :class:`Member`
    :param before: The voice state prior to the changes.
    :type before: :class:`VoiceState`
    :param after: The voice state after to the changes.
    :type after: :class:`VoiceState`

.. function:: on_member_ban(guild, user)

    Called when user gets banned from a :class:`Guild`.

    :param guild: The guild the user got banned from.
    :type guild: :class:`Guild`
    :param user: The user that got banned.
                 Can be either :class:`User` or :class:`Member` depending if
                 the user was in the guild or not at the time of removal.
    :type user: Union[:class:`User`, :class:`Member`]

.. function:: on_member_unban(guild, user)

    Called when a :class:`User` gets unbanned from a :class:`Guild`.

    :param guild: The guild the user got unbanned from.
    :type guild: :class:`Guild`
    :param user: The user that got unbanned.
    :type user: :class:`User`

.. function:: on_group_join(channel, user)
              on_group_remove(channel, user)

    Called when someone joins or leaves a :class:`GroupChannel`.

    :param channel: The group that the user joined or left.
    :type channel: :class:`GroupChannel`
    :param user: The user that joined or left.
    :type user: :class:`User`

.. function:: on_relationship_add(relationship)
              on_relationship_remove(relationship)

    Called when a :class:`Relationship` is added or removed from the
    :class:`ClientUser`.

    :param relationship: The relationship that was added or removed.
    :type relationship: :class:`Relationship`

.. function:: on_relationship_update(before, after)

    Called when a :class:`Relationship` is updated, e.g. when you
    block a friend or a friendship is accepted.

    :param before: The previous relationship status.
    :type before: :class:`Relationship`
    :param after: The updated relationship status.
    :type after: :class:`Relationship`
