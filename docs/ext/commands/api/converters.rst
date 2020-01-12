.. currentmodule:: discord

.. _ext_commands_api_converters:

Converters
------------

.. autoclass:: discord.ext.commands.Converter
    :members:

.. autoclass:: discord.ext.commands.MemberConverter
    :members:

.. autoclass:: discord.ext.commands.UserConverter
    :members:

.. autoclass:: discord.ext.commands.MessageConverter
    :members:

.. autoclass:: discord.ext.commands.TextChannelConverter
    :members:

.. autoclass:: discord.ext.commands.VoiceChannelConverter
    :members:

.. autoclass:: discord.ext.commands.CategoryChannelConverter
    :members:

.. autoclass:: discord.ext.commands.InviteConverter
    :members:

.. autoclass:: discord.ext.commands.RoleConverter
    :members:

.. autoclass:: discord.ext.commands.GameConverter
    :members:

.. autoclass:: discord.ext.commands.ColourConverter
    :members:

.. autoclass:: discord.ext.commands.EmojiConverter
    :members:

.. autoclass:: discord.ext.commands.PartialEmojiConverter
    :members:

.. autoclass:: discord.ext.commands.clean_content
    :members:

.. data:: ext.commands.Greedy

    A special converter that greedily consumes arguments until it can't.
    As a consequence of this behaviour, most input errors are silently discarded,
    since it is used as an indicator of when to stop parsing.

    When a parser error is met the greedy converter stops converting, undoes the
    internal string parsing routine, and continues parsing regularly.

    For example, in the following code:

    .. code-block:: python3

        @commands.command()
        async def test(ctx, numbers: Greedy[int], reason: str):
            await ctx.send("numbers: {}, reason: {}".format(numbers, reason))

    An invocation of ``[p]test 1 2 3 4 5 6 hello`` would pass ``numbers`` with
    ``[1, 2, 3, 4, 5, 6]`` and ``reason`` with ``hello``\.

    For more information, check :ref:`ext_commands_special_converters`.
