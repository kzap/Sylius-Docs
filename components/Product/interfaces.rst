Interfaces
==========

Model Interfaces
----------------

.. _component_product_model_product-interface:

ProductInterface
~~~~~~~~~~~~~~~~

This interface should be implemented by models characterizing a product.

.. note::
   This interface extends :ref:`component_archetype_model_archetype-subject-interface`,
   :ref:`component_resource_model_slug-aware-interface`,
   :ref:`component_resource_model_soft-deletable-interface`,
   :ref:`component_resource_model_timestampable-interface`
   and :ref:`component_product_model_product-translation-interface`. |br|
   For more information go to `Sylius API ProductInterface`_.

.. _Sylius API ProductInterface: http://api.sylius.org/Sylius/Component/Product/Model/ProductInterface.html

.. _component_product_model_product-translation-interface:

ProductTranslationInterface
~~~~~~~~~~~~~~~~~~~~~~~~~~~

This interface should be implemented by models used for storing a single translation of product fields.

.. note::
   This interface extends the :ref:`component_resource_model_slug-aware-interface`. |br|
   For more information go to `Sylius API ProductTranslationInterface`_.

.. _Sylius API ProductTranslationInterface: http://api.sylius.org/Sylius/Component/Product/Model/ProductTranslationInterface.html

.. _component_product_model_attribute-value-interface:

AttributeValueInterface
~~~~~~~~~~~~~~~~~~~~~~~

This interfaces should be implemented by models used
to bind an attribute and a value to a specific product.

.. note::
   This interface extends the :ref:`component_attribute_model_attribute-value-interface`. |br|
   For more information go to `Sylius API AttributeValueInterface`_.

.. _Sylius API AttributeValueInterface: http://api.sylius.org/Sylius/Component/Product/Model/AttributeValueInterface.html

.. _component_product_model_variant-interface:

VariantInterface
~~~~~~~~~~~~~~~~

This interface should be implemented by models binding
a product with a specific combination of attributes.

.. note::
   This interface extends the :ref:`component_variant_model_variant-interface`. |br|
   For more information go to `Sylius API VariantInterface`_.

.. _Sylius API VariantInterface: http://api.sylius.org/Sylius/Component/Product/Model/VariantInterface.html

Extended Interfaces
-------------------

The following interfaces only extend their basis without any kind of addition.
If you want to know more about a specific base interface,
follow the link enclosed under it's name.

.. _component_product_model_archetype-interface:

ArchetypeInterface
~~~~~~~~~~~~~~~~~~

.. note::
   This interface extends the :ref:`component_archetype_model_archetype-interface`. |br|
   For more information go to `Sylius API ArchetypeInterface`_.

.. _Sylius API ArchetypeInterface: http://api.sylius.org/Sylius/Component/Product/Model/ArchetypeInterface.html

.. _component_product_model_archetype-translation-interface:

ArchetypeTranslationInterface
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::
   This interface extends the :ref:`component_archetype_model_archetype-translation-interface`. |br|
   For more information go to `Sylius API ArchetypeTranslationInterface`_.

.. _Sylius API ArchetypeTranslationInterface: http://api.sylius.org/Sylius/Component/Product/Model/ArchetypeTranslationInterface.html

.. _component_product_model_attribute-interface:

AttributeInterface
~~~~~~~~~~~~~~~~~~

.. note::
   This interface extends the :ref:`component_attribute_model_attribute-interface`. |br|
   For more information go to `Sylius API AttributeInterface`_.

.. _Sylius API AttributeInterface: http://api.sylius.org/Sylius/Component/Product/Model/AttributeInterface.html

.. _component_product_model_attribute-translation-interface:

AttributeTranslationInterface
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::
   This interface extends the :ref:`component_attribute_model_attribute-translation-interface`. |br|
   For more information go to `Sylius API AttributeTranslationInterface`_.

.. _Sylius API AttributeTranslationInterface: http://api.sylius.org/Sylius/Component/Product/Model/AttributeTranslationInterface.html

.. _component_product_model_option-interface:

OptionInterface
~~~~~~~~~~~~~~~

.. note::
   This interface extends the :ref:`component_variant_model_option-interface`. |br|
   For more information go to `Sylius API OptionInterface`_.

.. _Sylius API OptionInterface: http://api.sylius.org/Sylius/Component/Product/Model/OptionInterface.html

.. _component_product_model_option-value-interface:

OptionValueInterface
~~~~~~~~~~~~~~~~~~~~

.. note::
   This interface extends the :ref:`component_variant_model_option-value-interface`. |br|
   For more information go to `Sylius API OptionValueInterface`_.

.. _Sylius API OptionValueInterface: http://api.sylius.org/Sylius/Component/Product/Model/OptionValueInterface.html

.. _component_product_model_option-translation-interface:

OptionTranslationInterface
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::
   This interface extends the :ref:`component_variant_model_option-translation-interface`. |br|
   For more information go to `Sylius API OptionTranslationInterface`_.

.. _Sylius API OptionTranslationInterface: http://api.sylius.org/Sylius/Component/Product/Model/OptionTranslationInterface.html
