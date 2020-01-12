.. currentmodule:: discord

.. _ext_commands_api_errors:

Exceptions
-----------

.. autoexception:: discord.ext.commands.CommandError
    :members:

.. autoexception:: discord.ext.commands.ConversionError
    :members:

.. autoexception:: discord.ext.commands.MissingRequiredArgument
    :members:

.. autoexception:: discord.ext.commands.ArgumentParsingError
    :members:

.. autoexception:: discord.ext.commands.UnexpectedQuoteError
    :members:

.. autoexception:: discord.ext.commands.InvalidEndOfQuotedStringError
    :members:

.. autoexception:: discord.ext.commands.ExpectedClosingQuoteError
    :members:

.. autoexception:: discord.ext.commands.BadArgument
    :members:

.. autoexception:: discord.ext.commands.BadUnionArgument
    :members:

.. autoexception:: discord.ext.commands.PrivateMessageOnly
    :members:

.. autoexception:: discord.ext.commands.NoPrivateMessage
    :members:

.. autoexception:: discord.ext.commands.CheckFailure
    :members:

.. autoexception:: discord.ext.commands.CommandNotFound
    :members:

.. autoexception:: discord.ext.commands.DisabledCommand
    :members:

.. autoexception:: discord.ext.commands.CommandInvokeError
    :members:

.. autoexception:: discord.ext.commands.TooManyArguments
    :members:

.. autoexception:: discord.ext.commands.UserInputError
    :members:

.. autoexception:: discord.ext.commands.CommandOnCooldown
    :members:

.. autoexception:: discord.ext.commands.NotOwner
    :members:

.. autoexception:: discord.ext.commands.MissingPermissions
    :members:

.. autoexception:: discord.ext.commands.BotMissingPermissions
    :members:

.. autoexception:: discord.ext.commands.MissingRole
    :members:

.. autoexception:: discord.ext.commands.BotMissingRole
    :members:

.. autoexception:: discord.ext.commands.MissingAnyRole
    :members:

.. autoexception:: discord.ext.commands.BotMissingAnyRole
    :members:

.. autoexception:: discord.ext.commands.NSFWChannelRequired
    :members:

.. autoexception:: discord.ext.commands.ExtensionError
    :members:

.. autoexception:: discord.ext.commands.ExtensionAlreadyLoaded
    :members:

.. autoexception:: discord.ext.commands.ExtensionNotLoaded
    :members:

.. autoexception:: discord.ext.commands.NoEntryPointError
    :members:

.. autoexception:: discord.ext.commands.ExtensionFailed
    :members:

.. autoexception:: discord.ext.commands.ExtensionNotFound
    :members:


Exception Hierarchy
+++++++++++++++++++++

.. exception_hierarchy::

    - :exc:`~.DiscordException`
        - :exc:`~.commands.CommandError`
            - :exc:`~.commands.ConversionError`
            - :exc:`~.commands.UserInputError`
                - :exc:`~.commands.MissingRequiredArgument`
                - :exc:`~.commands.TooManyArguments`
                - :exc:`~.commands.BadArgument`
                - :exc:`~.commands.BadUnionArgument`
                - :exc:`~.commands.ArgumentParsingError`
                    - :exc:`~.commands.UnexpectedQuoteError`
                    - :exc:`~.commands.InvalidEndOfQuotedStringError`
                    - :exc:`~.commands.ExpectedClosingQuoteError`
            - :exc:`~.commands.CommandNotFound`
            - :exc:`~.commands.CheckFailure`
                - :exc:`~.commands.PrivateMessageOnly`
                - :exc:`~.commands.NoPrivateMessage`
                - :exc:`~.commands.NotOwner`
                - :exc:`~.commands.MissingPermissions`
                - :exc:`~.commands.BotMissingPermissions`
                - :exc:`~.commands.MissingRole`
                - :exc:`~.commands.BotMissingRole`
                - :exc:`~.commands.MissingAnyRole`
                - :exc:`~.commands.BotMissingAnyRole`
                - :exc:`~.commands.NSFWChannelRequired`
            - :exc:`~.commands.DisabledCommand`
            - :exc:`~.commands.CommandInvokeError`
            - :exc:`~.commands.CommandOnCooldown`
        - :exc:`~.commands.ExtensionError`
            - :exc:`~.commands.ExtensionAlreadyLoaded`
            - :exc:`~.commands.ExtensionNotLoaded`
            - :exc:`~.commands.NoEntryPointError`
            - :exc:`~.commands.ExtensionFailed`
            - :exc:`~.commands.ExtensionNotFound`
