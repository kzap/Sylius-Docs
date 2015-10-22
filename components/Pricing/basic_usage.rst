Basic Usage
===========

Calculators
-----------

Standard Calculator
~~~~~~~~~~~~~~~~~~~

**StandardCalculator** class calculates the unit price of a subject.

.. code-block:: php

    <?php

    use Sylius\Component\Pricing\Calculator\StandardCalculator;

    $standardCalculator = new StandardCalculator();
    $priceableObject = new PriceableObject();
    $priceableObject->setPrice(1099);
    $priceableObject->setPricingConfiguration(array());
    $standardCalculator->calculate($priceableObject, $priceableObject->getPricingConfiguration());
    //return 1099

.. note::
    ``PriceableObject`` is a class, which implements ``PriceableInterface`` and we need create it ourselves.

Volume Based Calculator
~~~~~~~~~~~~~~~~~~~~~~~

**VolumeBasedCalculator** class calculates unit price depending on the quantity of subjects.

.. code-block:: php

    <?php

    use Sylius\Component\Pricing\Calculator\VolumeBasedCalculator;

    $volumeBasedCalculator = new VolumeBasedCalculator();
    $configuration = array(
        array(            //if quantity is between 2-9 the price is for each 300
            'min' => 2,
            'max' => 9,
            'price' => 300,
        ),
        array(
            'min' => 10, // if is more than 10 then price is 200
            'max' => null,
            'price' => 500,
        ),
    );//else is 599 (because the price from priceableObject is 599)

    $priceableObject = new PriceableObject();
    $priceableObject->setPricingConfiguration($configuration);
    $priceableObject->setPrice(599);

    $context = array('quantity' => 4);
    //if you don't pass $context to calculate method then quantity will be 1
    $volumeBasedCalculator->
    calculate($priceableObject, $priceableObject->getPricingConfiguration(), $context);
    // return 300
    //If the quantity of subjects are not in the ranges from $configuration, then the price
    // will be the same as price, which was set in priceableObject.

.. note::
    ``PriceableObject`` is a class, which implements ``PriceableInterface`` and you need create it yourself.

Delegating Calculator
~~~~~~~~~~~~~~~~~~~~~

**DelegatingCalculator** class delegates the calculation of charge for particular subject to a correct calculator
instance, based on the type defined on the subject.

.. code-block:: php

    <?php

    use Sylius\Component\Pricing\Calculator\StandardCalculator;
    use Sylius\Component\Pricing\Calculator\VolumeBasedCalculator;
    use Sylius\Component\Pricing\Calculator\DelegatingCalculator;
    use Sylius\Component\Registry\ServiceRegistry;
    //you can also create custom service registry, which should implement ServiceRegistryInterface

    $standardCalculator = new StandardCalculator();
    $volumeBasedCalculator = new VolumeBasedCalculator();

    $serviceRegistry =
    new ServiceRegistry('Sylius\Component\Pricing\Calculator\CalculatorInterface');
    $serviceRegistry->register(Calculators::STANDARD, $standardCalculator);
    $serviceRegistry->register(Calculators::VOLUME_BASED, $volumeBasedCalculator);

    $delegatingCalculator = new DelegatingCalculator($serviceRegistry);

    $priceableObject = new PriceableObject();
    $priceableObject->setPrice(398);
    $priceableObject->setPricingCalculator(Calculators::STANDARD);
    $priceableObject->setPricingConfiguration(array());

    $delegatingCalculator->calculate($priceableObject); //returns 398

    $configuration = array(
        array(
            'min' => 1,
            'max' => 9,
            'price' => 300,
        ),
        array(
            'min' => 10,
            'max' => null,
            'price' => 200,
        ),
    );

    $context = array('quantity' => 4);
    $priceableObject->setPricingConfiguration($configuration);
    $priceableObject->setPricingCalculator(Calculators::VOLUME_BASED);

    $delegatingCalculator->calculate($priceableObject, $context);
    //returns 200, because the pricing calculator was changed

.. note::
    ``PriceableObject`` is a class, which implements ``PriceableInterface`` and you need create it yourself.
