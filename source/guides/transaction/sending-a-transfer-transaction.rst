:orphan:

.. post:: 10 Aug, 2018
    :category: Transfer Transaction
    :excerpt: 1
    :nocomments:

##############################
Sending a transfer transaction
##############################

Transfer :doc:`mosaics <../../concepts/mosaic>` and messages between two accounts.

#############
Prerequisites
#############

- Finish the :doc:`getting started section <../../getting-started/setup-workstation>`
- Have one :ref:`account with cat.currency <setup-getting-a-test-account>`

**********
Background
**********

.. figure:: ../../resources/images/examples/transfer-transaction.png
    :align: center
    :width: 450px

    Sending a transfer Transaction

Alice wants to send ``10 cat.currency`` to Bob, whose address is ``SD5DT3-CH4BLA-BL5HIM-EKP2TA-PUKF4N-Y3L5HR-IR54``.

Monitoring the network
======================

Once an account announces a transaction, the server will always return an OK response. Receiving an OK response does not mean the transaction is valid. A good practice is to monitor transactions before being announced.

To understand the transaction lifecycle, we recommend you to open three new terminals. The first terminal :doc:`monitors announced transactions<../transaction/monitoring-a-transaction-status>` validation errors.

.. code-block:: bash

    $> nem2-cli monitor status

Monitoring ``unconfirmed`` shows you which transactions have reached the network, but are not included in a block yet.

.. code-block:: bash

    $> nem2-cli monitor unconfirmed

Once a transaction is included, you will see it under the ``confirmed`` terminal.

.. code-block:: bash

    $> nem2-cli monitor confirmed

************************
Let’s get into some code
************************

1. Create the transfer transaction, including Bob address as the recipient and ``10 cat.currency``.

.. example-code::

    .. literalinclude:: ../../resources/examples/typescript/transaction/SendingATransferTransaction.ts
        :caption: |sending-a-transfer-transaction-ts|
        :language: typescript
        :lines:  31-38

    .. literalinclude:: ../../resources/examples/javascript/transaction/SendingATransferTransaction.js
        :caption: |sending-a-transfer-transaction-js|
        :language: javascript
        :lines:  31-38

As you may have noticed, transfer transactions require an array of mosaics as a parameter, allowing to send transfer transactions with multiple mosaics at the same time.

If you own more than one mosaic, you can send them together in the same transaction:

.. example-code::

    .. literalinclude:: ../../resources/examples/typescript/transaction/SendingATransferTransactionWithMultipleMosaics.ts
        :caption: |sending-a-transfer-transaction-with-multiple-mosaics-ts|
        :language: typescript
        :lines:  39-40

    .. literalinclude:: ../../resources/examples/javascript/transaction/SendingATransferTransactionWithMultipleMosaics.js
        :caption: |sending-a-transfer-transaction-with-multiple-mosaics-js|
        :language: javascript
        :lines:  38-39

.. note:: NEM mainly works with absolute amounts. To get an absolute amount, multiply the amount of assets you want to send by 10\ :sup:`divisibility`.  For example, if the mosaic has :doc:`divisibility <../mosaic/getting-mosaic-information>` 2, to send 10 units (relative) you should define 1000 (absolute) instead.

2. Sign the transaction with Alice's account.

.. example-code::

    .. literalinclude:: ../../resources/examples/typescript/transaction/SendingATransferTransaction.ts
        :caption: |sending-a-transfer-transaction-ts|
        :language: typescript
        :lines:  41-45

    .. literalinclude:: ../../resources/examples/javascript/transaction/SendingATransferTransaction.js
        :caption: |sending-a-transfer-transaction-js|
        :language: javascript
        :lines:  41-45

3. Once signed, :doc:`announce the transaction <../../concepts/transaction>` to the network.

.. example-code::

    .. literalinclude:: ../../resources/examples/typescript/transaction/SendingATransferTransaction.ts
        :caption: |sending-a-transfer-transaction-ts|
        :language: typescript
        :lines:  48-

    .. literalinclude:: ../../resources/examples/javascript/transaction/SendingATransferTransaction.js
        :caption: |sending-a-transfer-transaction-js|
        :language: javascript
        :lines:  48-

    .. literalinclude:: ../../resources/examples/cli/transaction/SendingATransferTransaction.sh
        :caption: |sending-a-transfer-transaction-cli|
        :language: bash
        :start-after: #!/bin/sh

4. Open the terminal where you are monitoring account transactions ``status``. It should be empty. If there is an error, you can check :ref:`the error code meaning here <status-errors>`.

A new transaction should have appeared in the terminal where you are monitoring ``unconfirmed``. At this point, the transaction has reached the network, but it is not clear if it will get included in a block.

If it is included in a block, the transaction gets processed, and the amount stated in the transaction gets transferred from the sender's account to the recipient's account.

.. |sending-a-transfer-transaction-ts| raw:: html

   <a href="https://github.com/nemtech/nem2-docs/blob/master/source/resources/examples/typescript/transaction/SendingATransferTransaction.ts" target="_blank">View Code</a>

.. |sending-a-transfer-transaction-js| raw:: html

   <a href="https://github.com/nemtech/nem2-docs/blob/master/source/resources/examples/javascript/transaction/SendingATransferTransaction.js" target="_blank">View Code</a>

.. |sending-a-transfer-transaction-cli| raw:: html

   <a href="https://github.com/nemtech/nem2-docs/blob/master/source/resources/examples/cli/transaction/SendingATransferTransaction.sh" target="_blank">View Code</a>

.. |sending-a-transfer-transaction-with-multiple-mosaics-ts| raw:: html

   <a href="https://github.com/nemtech/nem2-docs/blob/master/source/resources/examples/typescript/transaction/SendingATransferTransactionWithMultipleMosaics.ts" target="_blank">View Code</a>

.. |sending-a-transfer-transaction-with-multiple-mosaics-js| raw:: html

   <a href="https://github.com/nemtech/nem2-docs/blob/master/source/resources/examples/javascript/transaction/SendingATransferTransactionWithMultipleMosaics.js" target="_blank">View Code</a>

.. |sending-a-transfer-transaction-with-multiple-mosaics-cli| raw:: html

   <a href="https://github.com/nemtech/nem2-docs/blob/master/source/resources/examples/cli/transaction/SendingATransferTransactionWithMultipleMosaics.sh" target="_blank">View Code</a>
