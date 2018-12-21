# How to get product attribute value in magento 2

To get attribute value of product with store_id is 0, we can:

~~~~

    public function __construct(\Magento\Catalog\Api\ProductRepositoryInterface $productRepository) {
        $this->productRepository = $productRepository;
    }

    public function execute(){
        $productId = xxx;
        $product = $this->productRepository->getById($productId, false, 0);
        echo $product->getData('attribute-code');
    }

~~~~