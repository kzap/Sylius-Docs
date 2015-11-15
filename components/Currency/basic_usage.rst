Basic Usage
===========

Getting a Currency name
-----------------------

The ``getName`` method uses Symfony's `Intl`_ class to
convert currency's code into a human friendly form.

.. _Intl: http://symfony.com/doc/current/components/intl.html

.. code-block:: php

   <?php

   use Sylius\Component\Currency\Model\Currency;

   $currency = new Currency();

   $currency->setCode('USD');

   $currency->getName(); // returns 'US Dollar'

.. note::
   The output of ``getName`` may vary as the name is generated accordingly to the set locale.

.. _component_currency_context_currency-context:

CurrencyContext
---------------

The **CurrencyContext** gives you the ability to quickly
set and retrieve currency names from a given :doc:`/components/Storage/index`.

.. tip::
   You can use a custom storage, as long as it implements the :ref:`component_storage_storage-interface`.

In this example let's use the default :ref:`component_storage_session-storage`.

.. code-block:: php

   <?php

   use Sylius\Component\Currency\Context\CurrencyContext;
   use Sylius\Component\Storage\SessionStorage;
   use Symfony\Component\HttpFoundation\Session\Session;

   $session = new Session();
   $session->start();
   $sessionStorage = new SessionStorage($session);

   $currency = 'USD'; // the currency which will be used by default in this context

   $currencyContext = new CurrencyContext($sessionStorage, $currency);

   $currencyContext->getDefaultCurrency(); // returns 'USD'
   $currencyContext->getCurrency('GBP'); // returns 'USD' as the currency given is not in storage
   $currencyContext->setCurrency('GBP');
   $currencyContext->getCurrency('GBP'); // returns 'GBP' for now it's available in the storage

.. note::
   This service implements the :ref:`component_currency_context_currency-context-interface`. |br|
   For more detailed information go to `Sylius API CurrencyContext`_.

.. _Sylius API CurrencyContext: http://api.sylius.org/Sylius/Component/Currency/Context/CurrencyContext.html

.. caution::
   Be aware that setting the default currency is done only once while creating the context,
   afterwards you cannot change it.

.. _component_currency_converter_currency-converter:

CurrencyConverter
-----------------

The **CurrencyConverter** allows you to convert a value accordingly to the exchange rate of specified currency.

.. code-block:: php

   <?php

   use Sylius/Component/Currency/Converter/CurrencyConverter;
   use Sylius/Component/Currency/Model/Currency;

   $currencyRepository = new InMemoryRepository();

   $currency = new Currency();
   $currency->setCode('USD');
   $currency->setExchangeRate(1.5);

   $currencyConverter = new CurrencyConverter($currencyRepository);

   $currencyConverter->convert(1000, 'USD'); // returns 1500

.. note::
   This service implements the :ref:`component_currency_converter_currency-converter-interface`. |br|
   For more detailed information go to `Sylius API CurrencyConverter`_.

.. _Sylius API CurrencyConverter: http://api.sylius.org/Sylius/Component/Currency/Converter/CurrencyConverter.html

.. caution::
   Throws :ref:`component_currency_converter_unavailable-currency-exception`.

Importers
---------

Importers allow you to get up-to-date exchange rates from given provider.
The rates are set from your chosen base currency to all other managed currencies.

.. _component_currency_importer_european-central-bank-importer:

EuropeanCentralBankImporter
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The source of **EuropeanCentralBankImporter**'s data is the `European Central Bank`_.

.. _European Central Bank: http://www.ecb.int

.. code-block:: php

   <?php

   use Sylius\Component\Currency\Importer\EuropeanCentralBankImporter;
   // also use an object manager

   $manager = // your manager
   $repository = new InMemoryRepository();

   $baseCurrency = 'EUR';
   $managedCurrencies = array('USD', 'JPY', 'GBP');

   $euroImporter = new EuropeanCentralBankImporter($manager, $repository);

   $euroImporter->configure(array('base_currency' => $baseCurrency)); // sets base currency for this importer

   $euroImporter->import($managedCurrencies); // updates exchange rates for managed currencies

.. note::
   This service extends the :ref:`component_currency_importer_abstract-importer`. |br|
   For more detailed information go to `Sylius API EuropeanCentralBankImporter`_.

.. _Sylius API EuropeanCentralBankImporter: http://api.sylius.org/Sylius/Component/Currency/Importer/EuropeanCentralBankImporter.html

.. _component_currency_importer_open-exchange-rates-importer:

OpenExchangeRatesImporter
~~~~~~~~~~~~~~~~~~~~~~~~~

The **OpenExchangeRatesImporter** gets it's data from `Open Exchange Rates`_.

.. _Open Exchange Rates: http://openexchangerates.org

.. code-block:: php

   use Sylius\Component\Currency\Importer\OpenExchangeRatesImporter;
   // also use an object manager

   $manager = // your manager
   $repository = new InMemoryRepository();

   $app_id = 'PLN';
   $managedCurrencies = array('USD', 'JPY', 'GBP');

   $openImporter = new OpenExchangeRatesImporter($manager, $repository);

   $openImporter->configure(array('app_id' => $app_id)); // sets app id for this importer

   $openImporter->import($managedCurrencies); // updates exchange rates for managed currencies

.. note::
   This service extends the :ref:`component_currency_importer_abstract-importer`. |br|
   For more detailed information go to `Sylius API OpenExchangeRatesImporter`_.

.. _Sylius API OpenExchangeRatesImporter: http://api.sylius.org/Sylius/Component/Currency/Importer/OpenExchangeRatesImporter.html

.. _component_currency_provider_currency-provider:

CurrencyProvider
----------------

The **CurrencyProvider** allows you to get all available currencies.

.. code-block:: php

   <?php

   use Sylius\Component\Currency\Provider\CurrencyProvider;

   $currencyRepository = new InMemoryRepository();
   $currencyProvider = new CurrencyProvider($currencyRepository);

   $currencyProvider->getAvailableCurrencies(); // returns an array of Currency objects

.. note::
   This service implements the :ref:`component_currency_provider_currency-provider-interface`. |br|
   For more detailed information go to `Sylius API CurrencyProvider`_.

.. _Sylius API CurrencyProvider: http://api.sylius.org/Sylius/Component/Currency/Provider/CurrencyProvider.html
