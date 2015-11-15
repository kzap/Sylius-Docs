Basic Usage
===========

In order to benefit from the component's features at first we need to create a basic class that will implement
the :ref:`component_promotion_model_promotion-subject-interface`. Let's assume that we would like to
have a system that applies promotions on Tickets. Our **Ticket** class therefore will implement the
:ref:`component_promotion_model_promotion-countable-subject-interface` to give us an ability to count the subjects
for promotion application purposes.

.. code-block:: php

    <?php

    use Doctrine\Common\Collections\Collection;
    use Doctrine\Common\Collections\ArrayCollection;
    use Sylius\Component\Promotion\Model\PromotionCountableSubjectInterface;
    use Sylius\Component\Promotion\Model\PromotionSubjectInterface;
    use Sylius\Component\Promotion\Model\PromotionInterface;

    class Ticket implements PromotionCountableSubjectInterface
    {
        /**
         * @var int
         */
        private $quantity;
    
        /**
         * @var Collection
         */
        private $promotions;

        /**
         * @var int
         */
        private $unitPrice;

        public function __construct()
        {
            $this->promotions = new ArrayCollection();
        }
        /**
         * @return int
         */
        public function getQuantity()
        {
            return $this->quantity;
        }

        /**
         * @param int $quantity
         */
        public function setQuantity($quantity)
        {
            $this->quantity = $quantity;
        }

        /**
         * {@inheritdoc}
         */
        public function getPromotions()
        {
            return $this->promotions;
        }

        /**
         * {@inheritdoc}
         */
        public function hasPromotion(PromotionInterface $promotion)
        {
            return $this->promotions->contains($promotion);
        }

        /**
         * {@inheritdoc}
         */
        public function getPromotionSubjectTotal()
        {
            //implementation
        }

        /**
         * {@inheritdoc}
         */
        public function addPromotion(PromotionInterface $promotion)
        {
            if (!$this->hasPromotion($promotion)) {
                $this->promotions->add($promotion);
            }
        }

        /**
         * {@inheritdoc}
         */
        public function removePromotion(PromotionInterface $promotion)
        {
            if($this->hasPromotion($promotion))
            {
                $this->promotions->removeElement($promotion);
            }
        }

        /**
         * {@inheritdoc}
         */
        public function getPromotionSubjectCount()
        {
            return $this->getQuantity();
        }

        /**
         * @return int
         */
        public function getUnitPrice()
        {
            return $this->unitPrice;
        }

        /**
         * @param int $price
         */
        public function setUnitPrice($price)
        {
            $this->unitPrice = $price;
        }

        /**
         * @return int
         */
        public function getTotal()
        {
            return $this->getUnitPrice() * $this->getQuantity();
        }
    }

.. _component_promotion_generator_coupon-generator:

CouponGenerator
---------------

In order to automate the process of coupon generation the component provides us with a Coupon Generator.

.. code-block:: php

    <?php

    use Sylius\Component\Promotion\Model\Promotion;
    use Sylius\Component\Promotion\Generator\Instruction;
    use Sylius\Component\Promotion\Generator\CouponGenerator;

    $promotion = new Promotion();

    $instruction = new Instruction(); // $amount = 5 by default

    /**
     * @param RepositoryInterface    $repository
     * @param EntityManagerInterface $manager
     */
    $generator = new CouponGenerator($repository, $manager);

    //This will generate and persist 5 coupons into the database
    //basing on the instruction provided for the given promotion object
    $generator->generate($promotion, $instruction);

    // We can also generate one unique code, and assign it to a new Coupon.
    $code = $generator->generateUniqueCode();
    $coupon = new Coupon();
    $coupon->setCode($code);

Checkers
--------

.. _component_promotion_checker_item-count-rule-checker:

ItemCountRuleChecker
~~~~~~~~~~~~~~~~~~~~

Let's now see how to use the **ItemCountRuleChecker**:

.. code-block:: php

    <?php

    use Ticket;
    use Sylius\Component\Promotion\Checker\ItemCountRuleChecker;

    $itemCountChecker = new ItemCountRuleChecker();

    $subject = new Ticket();
    $subject->setQuantity(3);

    $configuration = array('count' => 2);

    $itemCountChecker->isEligible($subject, $configuration); // returns true

.. _component_promotion_checker_promotion-eligibility-checker:

PromotionEligibilityChecker
~~~~~~~~~~~~~~~~~~~~~~~~~~~

This is a service that checks if the promotion rules are eligible for a given subject.

.. code-block:: php

    <?php

    use Sylius\Component\Promotion\Model\Promotion;
    use Sylius\Component\Promotion\Model\Rule;
    use Sylius\Component\Promotion\Model\Action;
    use Sylius\Component\Promotion\Checker\PromotionEligibilityChecker;
    use Ticket;

    $registry = new ServiceRegistry('Sylius\Component\Promotion\Model\RuleInterface');
    $dispatcher = new EventDispatcher();

    /**
     * @param ServiceRegistryInterface $registry
     * @param EventDispatcherInterface $dispatcher
     */
    $checker = new PromotionEligibilityChecker($registry, $dispatcher);

    // Let's create a new promotion
    $promotion = new Promotion();
    $promotion->setName('Test');

    // And a new action for that promotion, that will give a fixed discount of 10
    $action = new Action();
    $action->setType('fixed_discount');
    $action->setConfiguration(array('amount' => 10));
    $action->setPromotion($promotion);

    // That promotion will also have a rule - works for item amounts over 2
    $rule = new Rule();
    $rule->setType('item_count');

    $configuration = array('count' => 2);
    $rule->setConfiguration($configuration);

    $registry->register('item_count', $rule);

    $promotion->addRule($rule);

    // Now we need an object that implements the PromotionSubjectInterface
    // so we will use our custom Ticket class.
    $subject = new Ticket();

    $subject->addPromotion($promotion);
    $subject->setQuantity(3);
    $subject->setUnitPrice(10);

    $checker->isEligible($subject, $promotion); // Returns true

.. note::

    It implements the :ref:`component_promotion_checker_promotion-eligibility-checker-interface`.

.. _component_promotion_action_promotion-applicator:

PromotionApplicator
-------------------

In order to automate the process of promotion application the component provides us with a Promotion Applicator,
which is able to apply and revert single promotions on a subject implementing *

.. code-block:: php

    <?php

    use Sylius\Component\Promotion\Action\PromotionApplicator;
    use Sylius\Component\Promotion\Model\Promotion;
    use Sylius\Component\Registry\ServiceRegistry;
    use Ticket;

    $registry = new ServiceRegistry('Sylius\Component\Promotion\Model\ActionInterface');
    $promotionApplicator = new PromotionApplicator($registry);

    $promotion = new Promotion();

    $subject = new Ticket();
    $subject->addPromotion($promotion);

    $promotionApplicator->apply($subject, $promotion);

    $promotionApplicator->revert($subject, $promotion);

.. note::

    It implements the :ref:`component_promotion_action_promotion-applicator-interface`.

.. _component_promotion_processor_promotion-processor:

PromotionProcessor
------------------

The component provides us with a ``PromotionProcessor`` which checks all rules and applies configured actions if rules are eligible.


.. code-block:: php

    <?php

    use Sylius\Component\Promotion\Processor\PromotionProcessor;
    use Ticket;

    /**
     * @param PromotionRepositoryInterface         $repository
     * @param PromotionEligibilityCheckerInterface $checker
     * @param PromotionApplicatorInterface         $applicator
     */
    $processor = new PromotionProcessor($repository, $checker, $applicator);

    $subject = new Ticket();

    $processor->process($subject);

.. note::

    It implements the :ref:`component_promotion_processor_promotion-processor-interface`.