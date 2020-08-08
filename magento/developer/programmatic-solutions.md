# Programmatic Solutions

### Enable/Disable Product

```php
$objectManager = \Magento\Framework\App\ObjectManager::getInstance();
$productObject = $objectManager->create('Magento\Catalog\Api\ProductRepositoryInterface');
$product = $productObject->get($sku);
$product->setStatus(\Magento\Catalog\Model\Product\Attribute\Source\Status::STATUS_DISABLED);
// $product->setStatus(\Magento\Catalog\Model\Product\Attribute\Source\Status::STATUS_ENABLED);
$productObject->save($product);

```

### Update product Attributes

```php
$productActionObject = $objectManager->create('Magento\Catalog\Model\Product\Action');
$productActionObject->updateAttributes($idArray, array($title => $value), $storeId);

```

