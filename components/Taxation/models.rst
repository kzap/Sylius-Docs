Models
======

TaxRate
-------

Tax rate model holds the configuration for particular tax rate.

+-----------------+------------------------------------+-----------------------+
| Property        | Description                        | Type                  |
+=================+====================================+=======================+
| id              | Unique id of the tax rate          | mixed                 |
+-----------------+------------------------------------+-----------------------+
| category        | Tax rate category                  | TaxCategoryInterface  |
+-----------------+------------------------------------+-----------------------+
| name            | Name of the rate                   | string                |
+-----------------+------------------------------------+-----------------------+
| amount          | Amount as float (for example 0,23) | float                 |
+-----------------+------------------------------------+-----------------------+
| includedInPrice | Is the tax included in price?      | bool                  |
+-----------------+------------------------------------+-----------------------+
| calculator      | Type of calculator                 | string                |
+-----------------+------------------------------------+-----------------------+
| createdAt       | Date when the rate was created     | \\DateTime            |
+-----------------+------------------------------------+-----------------------+
| updatedAt       | Date of the last tax rate update   | \\DateTime            |
+-----------------+------------------------------------+-----------------------+

.. note::
    This model implements ``TaxRateInterface``.

TaxCategory
-----------

Tax category model holds the configuration for particular tax category.

+-----------------+--------------------------------------------------------+---------------------+
| Property        | Description                                            | Type                |
+=================+========================================================+=====================+
| id              | Unique id of the tax category                          | mixed               |
+-----------------+--------------------------------------------------------+---------------------+
| name            | Name of the category                                   | string              |
+-----------------+--------------------------------------------------------+---------------------+
| description     | Description of tax category                            | string              |
+-----------------+--------------------------------------------------------+---------------------+
| rates           | Collection of tax rates belonging to this tax category | TaxRateInterface[]  |
+-----------------+--------------------------------------------------------+---------------------+
| createdAt       | Date when the category was created                     | \\DateTime          |
+-----------------+--------------------------------------------------------+---------------------+
| updatedAt       | Date of the last tax category update                   | \\DateTime          |
+-----------------+--------------------------------------------------------+---------------------+

.. note::
    This model implements ``TaxCategoryInterface``.

