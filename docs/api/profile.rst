.. currentmodule:: discord

.. _discord_api_models_profile:

Profile
---------

.. class:: Profile

    A namedtuple representing a user's Discord public profile.

    .. attribute:: user

        The :class:`User` the profile belongs to.
    .. attribute:: premium

        A boolean indicating if the user has premium (i.e. Discord Nitro).
    .. attribute:: nitro

        An alias for :attr:`premium`.
    .. attribute:: premium_since

        A naive UTC datetime indicating how long the user has been premium since.
        This could be ``None`` if not applicable.
    .. attribute:: staff

        A boolean indicating if the user is Discord Staff.
    .. attribute:: partner

        A boolean indicating if the user is a Discord Partner.
    .. attribute:: bug_hunter

        A boolean indicating if the user is a Bug Hunter.
    .. attribute:: early_supporter

        A boolean indicating if the user has had premium before 10 October, 2018.
    .. attribute:: hypesquad

        A boolean indicating if the user is in Discord HypeSquad.
    .. attribute:: hypesquad_houses

        A list of :class:`HypeSquadHouse` that the user is in.
    .. attribute:: mutual_guilds

        A list of :class:`Guild` that the :class:`ClientUser` shares with this
        user.
    .. attribute:: connected_accounts

        A list of dict objects indicating the accounts the user has connected.

        An example entry can be seen below: ::

            {type: "twitch", id: "92473777", name: "discordapp"}
