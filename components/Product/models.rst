Models
======

.. _component_product_model_product:

Product
-------

The **Product** model represents every unique product in the catalog.
By default it contains the following properties:

+-------------+---------------------------------------+
| Property    | Description                           |
+=============+=======================================+
| id          | Unique id of the product              |
+-------------+---------------------------------------+
| archetype   | An archetype assigned to this product |
+-------------+---------------------------------------+
| availableOn | When the product is available         |
+-------------+---------------------------------------+
| attributes  | Attributes assigned to this product   |
+-------------+---------------------------------------+
| variants    | Variants assigned to this product     |
+-------------+---------------------------------------+
| options     | Options assigned to this product      |
+-------------+---------------------------------------+
| createdAt   | Product's date of creation            |
+-------------+---------------------------------------+
| updatedAt   | Product's date of update              |
+-------------+---------------------------------------+
| deletedAt   | Product's date of deletion            |
+-------------+---------------------------------------+

.. note::
   This model extends the :ref:`component_translation_model_abstract-translatable`
   and implements the :ref:`component_product_model_product-interface`. |br|
   For more detailed information go to `Sylius API Product`_.

.. _Sylius API Product: http://api.sylius.org/Sylius/Component/Product/Model/Product.html

.. _component_product_model_product-translation:

ProductTranslation
------------------

This model is responsible for keeping a translation
of product's simple properties according to given locale.
By default it has the following properties:

+-----------------+--------------------------------------+
| Property        | Description                          |
+=================+======================================+
| id              | Unique id of the product translation |
+-----------------+--------------------------------------+
| name            | Product's name                       |
+-----------------+--------------------------------------+
| slug            | Product's slug                       |
+-----------------+--------------------------------------+
| description     | Product's description                |
+-----------------+--------------------------------------+
| metaKeywords    | Product's meta keywords              |
+-----------------+--------------------------------------+
| metaDescription | Product's meta description           |
+-----------------+--------------------------------------+

.. note::
   This model extends the :ref:`component_translation_model_abstract-translation`
   and implements the :ref:`component_product_model_product-translation-interface`. |br|
   For more detailed information go to `Sylius API ProductTranslation`_.

.. _Sylius API ProductTranslation: http://api.sylius.org/Sylius/Component/Product/Model/ProductTranslation.html

.. _component_product_model_attribute-value:

AttributeValue
--------------

This **AttributeValue** extension ensures that it's **subject**
is an instance of the :ref:`component_product_model_product-interface`.

.. note::
   This model extends the :ref:`component_attribute_model_attribute-value`
   and implements the :ref:`component_product_model_attribute-value-interface`. |br|
   For more detailed information go to `Sylius API AttributeValue`_.

.. _Sylius API AttributeValue: http://api.sylius.org/Sylius/Component/Product/Model/AttributeValue.html

.. _component_product_model_variant:

Variant
-------

This **Variant** extension ensures that it's **object**
is an instance of the :ref:`component_product_model_product-interface`
and provides an additional property:

+-------------+---------------------------------------------------------+
| Property    | Description                                             |
+=============+=========================================================+
| availableOn | The date indicating when a product variant is available |
+-------------+---------------------------------------------------------+

.. note::
   This model extends the :ref:`component_variation_model_variant`
   and implements the :ref:`component_product_model_variant-interface`. |br|
   For more detailed information go to `Sylius API Variant`_.

.. _Sylius API Variant: http://api.sylius.org/Sylius/Component/Product/Model/Variant.html

Extended Models
---------------

The following models only extend their basis, without any kind of addition.
If you want to know more about a specific base model,
follow the link enclosed under its name.

.. _component_product_model_archetype:

Archetype
---------

.. note::
   This model extends the :ref:`component_archetype_model_archetype`
   and implements the :ref:`component_product_model_archetype-interface`. |br|
   For more detailed information go to `Sylius API Archetype`_.

.. _Sylius API Archetype: http://api.sylius.org/Sylius/Component/Product/Model/Archetype.html

.. _component_product_model_archetype-translation:

ArchetypeTranslation
--------------------

.. note::
   This model extends the :ref:`component_archetype_model_archetype-translation`
   and implements the :ref:`component_product_model_archetype-translation-interface`. |br|
   For more detailed information go to `Sylius API ArchetypeTranslation`_.

.. _Sylius API ArchetypeTranslation: http://api.sylius.org/Sylius/Component/Product/Model/ArchetypeTranslation.html

.. _component_product_model_attribute:

Attribute
---------

.. note::
   This model extends the :ref:`component_attribute_model_attribute`
   and implements the :ref:`component_product_model_attribute-interface`. |br|
   For more detailed information go to `Sylius API Attribute`_.

.. _Sylius API Attribute: http://api.sylius.org/Sylius/Component/Product/Model/Attribute.html

.. _component_product_model_attribute-translation:

AttributeTranslation
--------------------

.. note::
   This model extends the :ref:`component_attribute_model_attribute-translation`
   and implements the :ref:`component_product_model_attribute-translation-interface`. |br|
   For more detailed information go to `Sylius API AttributeTranslation`_.

.. _Sylius API AttributeTranslation: http://api.sylius.org/Sylius/Component/Product/Model/AttributeTranslation.html

.. _component_product_model_option:

Option
------

.. note::
   This model extends the :ref:`component_variation_model_option`
   and implements the :ref:`component_product_model_option-interface`. |br|
   For more detailed information go to `Sylius API Option`_.

.. _Sylius API Option: http://api.sylius.org/Sylius/Component/Product/Model/Option.html

.. _component_product_model_option-value:

OptionValue
-----------

.. note::
   This model extends the :ref:`component_variation_model_option-value`
   and implements the :ref:`component_product_model_option-value-interface`. |br|
   For more detailed information go to `Sylius API OptionValue`_.

.. _Sylius API OptionValue: http://api.sylius.org/Sylius/Component/Product/Model/OptionValue.html

.. _component_product_model_option-translation:

OptionTranslation
-----------------

.. note::
   This model extends the :ref:`component_variation_model_option-translation`
   and implements the :ref:`component_product_model_option-translation-interface`. |br|
   For more detailed information go to `Sylius API OptionTranslation`_.

.. _Sylius API OptionTranslation: http://api.sylius.org/Sylius/Component/Product/Model/OptionTranslation.html
