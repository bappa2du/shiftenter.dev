---
description: Magento project based playground for testing
---

# Playground

### Magento project custom file for testing

If you want test with some custom class or custom query or any other functionality, then create a test file as demo.php or whatever you like and play with that as below

{% tabs %}
{% tab title="demo.php" %}
```php
<?php

ini_set('error_reporting', E_ALL);
ini_set('display_errors', 1);
ini_set('display_startup_errors', 1);

require __DIR__ . '/app/bootstrap.php';
$bootstrap = \Magento\Framework\App\Bootstrap::create(BP, $_SERVER);
$objectManager = $bootstrap->getObjectManager();
$appState = $objectManager->get(\Magento\Framework\App\State::class);
//$layerResolver = $objectManager->get(\Magento\Catalog\Model\Layer\Resolver::class);
$appState->setAreaCode('frontend');
$storeId = 0;

/** @var \Magento\Framework\App\ResourceConnection $resource */
$resource = $objectManager->get('Magento\Framework\App\ResourceConnection');
$connection = $resource->getConnection();

$query = <<<QUERY
select p.name,p.sku,c.name as category,c.name,concat('/media/catalog/product',p.thumbnail) as image,
p.price,p.special_price,p.brand,p.unit,p.url_key,p.unit_weight,p.certified
from catalog_product_flat_1 as p
join catalog_category_product as r
on p.entity_id = r.product_id
join catalog_category_flat_store_1 as c
on c.entity_id = r.category_id
where c.url_path like 'mat-dryck-utrustning%'
limit 20,40;
QUERY;

$data = $connection->fetchAll($query);


```
{% endtab %}
{% endtabs %}

