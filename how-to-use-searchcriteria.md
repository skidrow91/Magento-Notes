# How to use searchCriteria to get list object in magento 2

If you want to get list object in magento 2, you can use collection. Additional, you can use getList() from repository interface of object. Following by code as below, I try to using searchCriteria to get quotes from specific customer instead of collection.

~~~~

    public function __construct(
        \Magento\Framework\Api\Search\FilterGroup $filterGroup,
        \Magento\Framework\Api\Filter $filter,
        \Magento\Framework\Api\SearchCriteria $searchCriteria,
        \Magento\Quote\Api\CartRepositoryInterface $cartRepository
    ){
        $this->filterGroup = $filterGroup;
        $this->filter = $filter;
        $this->searchCriteria = $searchCriteria;
        $this->cartRepository = $cartRepository;
    }

    public function execute()
    {
        $customerId = xyz;
        $filter = $this->filter->setField('customer_id')->setValue($customerId)->setConditionType('eq');
        $filterGroup = $this->filterGroup->setFilters([$filter]);
        $searchCriteria = $this->searchCriteria->setFilterGroups([$filterGroup]);
        $carts = $this->cartRepository->getList($searchCriteria);
        foreach ($carts->getItems() as $item) { ... }
    }

~~~~

Or

~~~~

    public function __construct(
        \Magento\Framework\Api\FilterBuilder $filterBuilder,
        \Magento\Framework\Api\SearchCriteriaBuilder $searchCriteriaBuilder,
        \Magento\Quote\Api\CartRepositoryInterface $cartRepository
    ){
        $this->filterBuilder = $filterBuilder;
        $this->searchCriteriaBuilder = $searchCriteriaBuilder;
        $this->cartRepository = $cartRepository;
    }

    public function execute()
    {
        $customerId = xyz;
        $filter = $this->filterBuilder->setField('customer_id')->setValue($customerId)->create();
        $searchCriteriaBuilder = $this->searchCriteriaBuilder->addFilters([$filter])->create();
        $carts = $this->cartRepository->getList($searchCriteriaBuilder);
        foreach ($carts->getItems() as $item) { ... }
    }

~~~~

Two ways are similar.