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

### Resource Connection\(DB\)

```php
$resource = $objectManager->get('Magento\Framework\App\ResourceConnection');
$connection = $resource->getConnection();
//Product entity id = 4
$selectStatusSQL = "SELECT `attribute_id` FROM eav_attribute where entity_type_id = 4 AND attribute_code = 'special_price' ";
$resultStatus = $connection->fetchOne($selectStatusSQL);
$specialPriceAttributeId = $resultStatus;
```

