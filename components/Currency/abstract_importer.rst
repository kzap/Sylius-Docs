.. _component_currency_importer_abstract-importer:

AbstractImporter
================

The abstract class **AbstractImporter** provides you with a handy method called ``updateOrCreate``
which manages the update of existing currencies or creating new if the ones given don't exist.
After that it saves all your currencies to a database.

.. note::
   This class implements the :ref:`component_currency_importer_importer-interface`.

By default there are two importers already implemented:

* :ref:`component_currency_importer_european-central-bank-importer`
* :ref:`component_currency_importer_open-exchange-rates-importer`

.. tip::
   Of course you are not limited to the default importers as you can simply make your own! |br|
   The only thing you need to do is extend the **AbstractImporter**.
