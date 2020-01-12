.. currentmodule:: discord

.. _discord_api_audit:

Audit Log Data
----------------

Working with :meth:`Guild.audit_logs` is a complicated process with a lot of machinery
involved. The library attempts to make it easy to use and friendly. In order to accomplish
this goal, it must make use of a couple of data classes that aid in this goal.

.. autoclass:: AuditLogEntry
    :members:

.. class:: AuditLogChanges

    An audit log change set.

    .. attribute:: before

        The old value. The attribute has the type of :class:`AuditLogDiff`.

        Depending on the :class:`AuditLogActionCategory` retrieved by
        :attr:`~AuditLogEntry.category`\, the data retrieved by this
        attribute differs:

        +----------------------------------------+---------------------------------------------------+
        |                Category                |                    Description                    |
        +----------------------------------------+---------------------------------------------------+
        | :attr:`~AuditLogActionCategory.create` | All attributes are set to ``None``.               |
        +----------------------------------------+---------------------------------------------------+
        | :attr:`~AuditLogActionCategory.delete` | All attributes are set the value before deletion. |
        +----------------------------------------+---------------------------------------------------+
        | :attr:`~AuditLogActionCategory.update` | All attributes are set the value before updating. |
        +----------------------------------------+---------------------------------------------------+
        | ``None``                               | No attributes are set.                            |
        +----------------------------------------+---------------------------------------------------+

    .. attribute:: after

        The new value. The attribute has the type of :class:`AuditLogDiff`.

        Depending on the :class:`AuditLogActionCategory` retrieved by
        :attr:`~AuditLogEntry.category`\, the data retrieved by this
        attribute differs:

        +----------------------------------------+--------------------------------------------------+
        |                Category                |                   Description                    |
        +----------------------------------------+--------------------------------------------------+
        | :attr:`~AuditLogActionCategory.create` | All attributes are set to the created value      |
        +----------------------------------------+--------------------------------------------------+
        | :attr:`~AuditLogActionCategory.delete` | All attributes are set to ``None``               |
        +----------------------------------------+--------------------------------------------------+
        | :attr:`~AuditLogActionCategory.update` | All attributes are set the value after updating. |
        +----------------------------------------+--------------------------------------------------+
        | ``None``                               | No attributes are set.                           |
        +----------------------------------------+--------------------------------------------------+

.. class:: AuditLogDiff

    Represents an audit log "change" object. A change object has dynamic
    attributes that depend on the type of action being done. Certain actions
    map to certain attributes being set.

    Note that accessing an attribute that does not match the specified action
    will lead to an attribute error.

    To get a list of attributes that have been set, you can iterate over
    them. To see a list of all possible attributes that could be set based
    on the action being done, check the documentation for :class:`AuditLogAction`,
    otherwise check the documentation below for all attributes that are possible.

    .. describe:: iter(diff)

        Returns an iterator over (attribute, value) tuple of this diff.

    .. attribute:: name

        :class:`str` – A name of something.

    .. attribute:: icon

        :class:`str` – A guild's icon hash. See also :attr:`Guild.icon`.

    .. attribute:: splash

        :class:`str` – The guild's invite splash hash. See also :attr:`Guild.splash`.

    .. attribute:: owner

        Union[:class:`Member`, :class:`User`] – The guild's owner. See also :attr:`Guild.owner`

    .. attribute:: region

        :class:`VoiceRegion` – The guild's voice region. See also :attr:`Guild.region`.

    .. attribute:: afk_channel

        Union[:class:`VoiceChannel`, :class:`Object`] – The guild's AFK channel.

        If this could not be found, then it falls back to a :class:`Object`
        with the ID being set.

        See :attr:`Guild.afk_channel`.

    .. attribute:: system_channel

        Union[:class:`TextChannel`, :class:`Object`] – The guild's system channel.

        If this could not be found, then it falls back to a :class:`Object`
        with the ID being set.

        See :attr:`Guild.system_channel`.

    .. attribute:: afk_timeout

        :class:`int` – The guild's AFK timeout. See :attr:`Guild.afk_timeout`.

    .. attribute:: mfa_level

        :class:`int` - The guild's MFA level. See :attr:`Guild.mfa_level`.

    .. attribute:: widget_enabled

        :class:`bool` – The guild's widget has been enabled or disabled.

    .. attribute:: widget_channel

        Union[:class:`TextChannel`, :class:`Object`] – The widget's channel.

        If this could not be found then it falls back to a :class:`Object`
        with the ID being set.

    .. attribute:: verification_level

        :class:`VerificationLevel` – The guild's verification level.

        See also :attr:`Guild.verification_level`.

    .. attribute:: default_notifications

        :class:`NotificationLevel` – The guild's default notification level.

        See also :attr:`Guild.default_notifications`.

    .. attribute:: explicit_content_filter

        :class:`ContentFilter` – The guild's content filter.

        See also :attr:`Guild.explicit_content_filter`.

    .. attribute:: default_message_notifications

        :class:`int` – The guild's default message notification setting.

    .. attribute:: vanity_url_code

        :class:`str` – The guild's vanity URL.

        See also :meth:`Guild.vanity_invite` and :meth:`Guild.edit`.

    .. attribute:: position

        :class:`int` – The position of a :class:`Role` or :class:`abc.GuildChannel`.

    .. attribute:: type

        Union[:class:`int`, :class:`str`] – The type of channel or channel permission overwrite.

        If the type is an :class:`int`, then it is a type of channel which can be either
        ``0`` to indicate a text channel or ``1`` to indicate a voice channel.

        If the type is a :class:`str`, then it is a type of permission overwrite which
        can be either ``'role'`` or ``'member'``.

    .. attribute:: topic

        :class:`str` – The topic of a :class:`TextChannel`.

        See also :attr:`TextChannel.topic`.

    .. attribute:: bitrate

        :class:`int` – The bitrate of a :class:`VoiceChannel`.

        See also :attr:`VoiceChannel.bitrate`.

    .. attribute:: overwrites

        List[Tuple[target, :class:`PermissionOverwrite`]] – A list of
        permission overwrite tuples that represents a target and a
        :class:`PermissionOverwrite` for said target.

        The first element is the object being targeted, which can either
        be a :class:`Member` or :class:`User` or :class:`Role`. If this object
        is not found then it is a :class:`Object` with an ID being filled and
        a ``type`` attribute set to either ``'role'`` or ``'member'`` to help
        decide what type of ID it is.

    .. attribute:: roles

        List[Union[:class:`Role`, :class:`Object`]] – A list of roles being added or removed
        from a member.

        If a role is not found then it is a :class:`Object` with the ID and name being
        filled in.

    .. attribute:: nick

        Optional[:class:`str`] – The nickname of a member.

        See also :attr:`Member.nick`

    .. attribute:: deaf

        :class:`bool` – Whether the member is being server deafened.

        See also :attr:`VoiceState.deaf`.

    .. attribute:: mute

        :class:`bool` – Whether the member is being server muted.

        See also :attr:`VoiceState.mute`.

    .. attribute:: permissions

        :class:`Permissions` – The permissions of a role.

        See also :attr:`Role.permissions`.

    .. attribute:: colour
                   color

        :class:`Colour` – The colour of a role.

        See also :attr:`Role.colour`

    .. attribute:: hoist

        :class:`bool` – Whether the role is being hoisted or not.

        See also :attr:`Role.hoist`

    .. attribute:: mentionable

        :class:`bool` – Whether the role is mentionable or not.

        See also :attr:`Role.mentionable`

    .. attribute:: code

        :class:`str` – The invite's code.

        See also :attr:`Invite.code`

    .. attribute:: channel

        Union[:class:`abc.GuildChannel`, :class:`Object`] – A guild channel.

        If the channel is not found then it is a :class:`Object` with the ID
        being set. In some cases the channel name is also set.

    .. attribute:: inviter

        :class:`User` – The user who created the invite.

        See also :attr:`Invite.inviter`.

    .. attribute:: max_uses

        :class:`int` – The invite's max uses.

        See also :attr:`Invite.max_uses`.

    .. attribute:: uses

        :class:`int` – The invite's current uses.

        See also :attr:`Invite.uses`.

    .. attribute:: max_age

        :class:`int` – The invite's max age in seconds.

        See also :attr:`Invite.max_age`.

    .. attribute:: temporary

        :class:`bool` – If the invite is a temporary invite.

        See also :attr:`Invite.temporary`.

    .. attribute:: allow
                   deny

        :class:`Permissions` – The permissions being allowed or denied.

    .. attribute:: id

        :class:`int` – The ID of the object being changed.

    .. attribute:: avatar

        :class:`str` – The avatar hash of a member.

        See also :attr:`User.avatar`.

    .. attribute:: slowmode_delay

        :class:`int` – The number of seconds members have to wait before
        sending another message in the channel.

        See also :attr:`TextChannel.slowmode_delay`.

.. this is currently missing the following keys: reason and application_id
   I'm not sure how to about porting these
