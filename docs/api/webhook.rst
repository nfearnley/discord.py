.. currentmodule:: discord

.. _discord_api_webhook:

Webhook Support
------------------

discord.py offers support for creating, editing, and executing webhooks through the :class:`Webhook` class.

.. autoclass:: Webhook
    :members:

Adapters
~~~~~~~~~

Adapters allow you to change how the request should be handled. They all build on a single
interface, :meth:`WebhookAdapter.request`.

.. autoclass:: WebhookAdapter
    :members:

.. autoclass:: AsyncWebhookAdapter
    :members:

.. autoclass:: RequestsWebhookAdapter
    :members:
