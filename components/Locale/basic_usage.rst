Basic Usage
===========

LocaleContext
-------------

The **LocaleContext** allows you to manage the currently used locale.

.. code-block:: php

	<?php

	use Sylius\Component\Locale\Context\LocaleContext;
	use Sylius\Component\Resource\Repository\InMemoryRepository;

	$inMemoryRepository = new InMemoryRepository();

	$localeContext = new LocaleContext($inMemoryRepository, 'en');

	$localeContext->getDefaultLocale() // Output will be 'en'.
	$localeContext->getCurrentLocale() // Output based on your storage implementation.
	$localeContext->setCurrentLocale('us') // It will set your default locale in your storage.

.. note::
	For more detailed information go to `Sylius API LocaleContext`_.

.. _Sylius API LocaleContext: http://api.sylius.org/Sylius/Component/Locale/Context/LocaleContext.html

LocaleProvider
--------------

The **LocaleProvider** allows you to get all available locales.

.. code-block:: php

	<?php

	use Sylius\Component\Locale\Provider\LocaleProvider;

	$inMemoryRepository = new InMemoryRepository();

	$localeProvider = new LocaleProvider($inMemoryRepository);

	$localeProvider->getAvailableLocales() //Output will be a collection of all enabled locales
	$localeProvider->isLocaleAvailable('en') //It will check if that locale is enabled

.. note::
	For more detailed information go to `Sylius API LocaleProvider`_.

.. _Sylius API LocaleProvider: http://api.sylius.org/Sylius/Component/Locale/Provider/LocaleProvider.html
