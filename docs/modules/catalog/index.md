# Catalog Module | Модуль Catalog

## Overview | Обзор

The Catalog module provides functionality for managing product catalogs, prices, and product properties in Bitrix24. It enables users to create and manage product catalogs, set up pricing rules, handle product properties, and integrate with other modules like CRM and Sales. | Модуль Catalog предоставляет функциональность для управления каталогами товаров, ценами и свойствами товаров в Bitrix24. Он позволяет пользователям создавать и управлять каталогами товаров, настраивать правила ценообразования, обрабатывать свойства товаров и интегрироваться с другими модулями, такими как CRM и Sales.

## Methods | Методы

### Product Management | Управление товарами

#### Create Product | Создание товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$product = \Bitrix\Catalog\Model\Product::add([
    'NAME' => 'Product Name',
    'CODE' => 'PRODUCT_CODE',
    'IBLOCK_ID' => $iblockId,
    'IBLOCK_SECTION_ID' => $sectionId,
    'VAT_ID' => $vatId,
    'VAT_INCLUDED' => 'Y',
    'QUANTITY' => 100,
    'QUANTITY_TRACE' => 'Y',
    'CAN_BUY_ZERO' => 'N',
    'PRICE_TYPE' => 'S',
    'TMP_ID' => null,
    'PROPERTY_VALUES' => [
        'PROPERTY_CODE' => 'Property Value'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$productId = CCatalogProduct::Add([
    'IBLOCK_ID' => $iblockId,
    'NAME' => 'Product Name',
    'CODE' => 'PRODUCT_CODE',
    'IBLOCK_SECTION_ID' => $sectionId,
    'VAT_ID' => $vatId,
    'VAT_INCLUDED' => 'Y',
    'QUANTITY' => 100,
    'QUANTITY_TRACE' => 'Y',
    'CAN_BUY_ZERO' => 'N',
    'PRICE_TYPE' => 'S',
    'TMP_ID' => null,
    'PROPERTY_VALUES' => [
        'PROPERTY_CODE' => 'Property Value'
    ]
]);
```

#### Get Product | Получение товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$product = \Bitrix\Catalog\Model\Product::getList([
    'filter' => ['ID' => $productId],
    'select' => ['*', 'PROPERTY_*']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$product = CCatalogProduct::GetByID($productId);
```

#### Update Product | Обновление товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\Model\Product::update($productId, [
    'NAME' => 'Updated Product Name',
    'QUANTITY' => 200,
    'PROPERTY_VALUES' => [
        'PROPERTY_CODE' => 'Updated Property Value'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogProduct::Update($productId, [
    'NAME' => 'Updated Product Name',
    'QUANTITY' => 200,
    'PROPERTY_VALUES' => [
        'PROPERTY_CODE' => 'Updated Property Value'
    ]
]);
```

#### Delete Product | Удаление товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\Model\Product::delete($productId);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogProduct::Delete($productId);
```

### Price Management | Управление ценами

#### Set Price | Установка цены

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$price = \Bitrix\Catalog\Model\Price::add([
    'PRODUCT_ID' => $productId,
    'CATALOG_GROUP_ID' => $priceTypeId,
    'PRICE' => 1000.00,
    'CURRENCY' => 'RUB',
    'QUANTITY_FROM' => 0,
    'QUANTITY_TO' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$priceId = CPrice::Add([
    'PRODUCT_ID' => $productId,
    'CATALOG_GROUP_ID' => $priceTypeId,
    'PRICE' => 1000.00,
    'CURRENCY' => 'RUB',
    'QUANTITY_FROM' => 0,
    'QUANTITY_TO' => 0
]);
```

#### Get Price | Получение цены

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$price = \Bitrix\Catalog\Model\Price::getList([
    'filter' => ['PRODUCT_ID' => $productId],
    'select' => ['*']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$price = CPrice::GetBasePrice($productId);
```

#### Update Price | Обновление цены

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\Model\Price::update($priceId, [
    'PRICE' => 1500.00,
    'CURRENCY' => 'RUB'
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CPrice::Update($priceId, [
    'PRICE' => 1500.00,
    'CURRENCY' => 'RUB'
]);
```

#### Delete Price | Удаление цены

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\Model\Price::delete($priceId);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CPrice::Delete($priceId);
```

### Store Management | Управление складами

#### Create Store | Создание склада

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$store = \Bitrix\Catalog\Model\Store::add([
    'TITLE' => 'Main Store',
    'ADDRESS' => 'Store Address',
    'DESCRIPTION' => 'Store Description',
    'GPS_N' => '55.7558',
    'GPS_S' => '37.6173',
    'ISSUING_CENTER' => 'Y',
    'SHIPPING_CENTER' => 'Y',
    'SITE_ID' => 's1',
    'CODE' => 'MAIN_STORE',
    'IMAGE_ID' => $imageId,
    'LOCATION_ID' => $locationId,
    'PHONE' => '+7 (999) 123-45-67',
    'SCHEDULE' => 'Mon-Fri: 9:00-18:00',
    'EMAIL' => 'store@example.com'
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$storeId = CCatalogStore::Add([
    'TITLE' => 'Main Store',
    'ADDRESS' => 'Store Address',
    'DESCRIPTION' => 'Store Description',
    'GPS_N' => '55.7558',
    'GPS_S' => '37.6173',
    'ISSUING_CENTER' => 'Y',
    'SHIPPING_CENTER' => 'Y',
    'SITE_ID' => 's1',
    'CODE' => 'MAIN_STORE',
    'IMAGE_ID' => $imageId,
    'LOCATION_ID' => $locationId,
    'PHONE' => '+7 (999) 123-45-67',
    'SCHEDULE' => 'Mon-Fri: 9:00-18:00',
    'EMAIL' => 'store@example.com'
]);
```

#### Get Store | Получение склада

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$store = \Bitrix\Catalog\Model\Store::getList([
    'filter' => ['ID' => $storeId],
    'select' => ['*']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$store = CCatalogStore::GetByID($storeId);
```

#### Update Store | Обновление склада

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\Model\Store::update($storeId, [
    'TITLE' => 'Updated Store Name',
    'ADDRESS' => 'Updated Store Address',
    'PHONE' => '+7 (999) 765-43-21'
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogStore::Update($storeId, [
    'TITLE' => 'Updated Store Name',
    'ADDRESS' => 'Updated Store Address',
    'PHONE' => '+7 (999) 765-43-21'
]);
```

#### Delete Store | Удаление склада

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\Model\Store::delete($storeId);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogStore::Delete($storeId);
```

### Product Property Management | Управление свойствами товаров

#### Create Product Property | Создание свойства товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$property = \Bitrix\Catalog\Model\ProductProperty::add([
    'IBLOCK_ID' => $iblockId,
    'NAME' => 'Property Name',
    'CODE' => 'PROPERTY_CODE',
    'PROPERTY_TYPE' => 'S',
    'WITH_DESCRIPTION' => 'N',
    'MULTIPLE' => 'N',
    'MULTIPLE_CNT' => 1,
    'IS_REQUIRED' => 'N',
    'SORT' => 100,
    'DEFAULT_VALUE' => '',
    'USER_TYPE' => '',
    'USER_TYPE_SETTINGS' => '',
    'HINT' => '',
    'LINK_IBLOCK_ID' => 0,
    'FILTRABLE' => 'Y',
    'SEARCHABLE' => 'Y',
    'SHOW_FILTER' => 'S',
    'SHOW_IN_LIST' => 'Y',
    'SHOW_COLUMN' => 'N',
    'SHOW_QUICK_VIEW' => 'N',
    'SHOW_QUICK_VIEW_VIEW' => 'N',
    'SHOW_QUICK_VIEW_EDIT' => 'N',
    'SHOW_QUICK_VIEW_DETAIL' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT' => 'N',
    'SHOW_QUICK_VIEW_VIEW_DETAIL' => 'N',
    'SHOW_QUICK_VIEW_EDIT_DETAIL' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL_VIEW' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL_EDIT' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL_DETAIL' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL_VIEW_EDIT' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL_VIEW_DETAIL' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL_EDIT_DETAIL' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL_VIEW_EDIT_DETAIL' => 'N'
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$propertyId = CCatalogProduct::AddProperty([
    'IBLOCK_ID' => $iblockId,
    'NAME' => 'Property Name',
    'CODE' => 'PROPERTY_CODE',
    'PROPERTY_TYPE' => 'S',
    'WITH_DESCRIPTION' => 'N',
    'MULTIPLE' => 'N',
    'MULTIPLE_CNT' => 1,
    'IS_REQUIRED' => 'N',
    'SORT' => 100,
    'DEFAULT_VALUE' => '',
    'USER_TYPE' => '',
    'USER_TYPE_SETTINGS' => '',
    'HINT' => '',
    'LINK_IBLOCK_ID' => 0,
    'FILTRABLE' => 'Y',
    'SEARCHABLE' => 'Y',
    'SHOW_FILTER' => 'S',
    'SHOW_IN_LIST' => 'Y',
    'SHOW_COLUMN' => 'N',
    'SHOW_QUICK_VIEW' => 'N',
    'SHOW_QUICK_VIEW_VIEW' => 'N',
    'SHOW_QUICK_VIEW_EDIT' => 'N',
    'SHOW_QUICK_VIEW_DETAIL' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT' => 'N',
    'SHOW_QUICK_VIEW_VIEW_DETAIL' => 'N',
    'SHOW_QUICK_VIEW_EDIT_DETAIL' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL_VIEW' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL_EDIT' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL_DETAIL' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL_VIEW_EDIT' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL_VIEW_DETAIL' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL_EDIT_DETAIL' => 'N',
    'SHOW_QUICK_VIEW_VIEW_EDIT_DETAIL_VIEW_EDIT_DETAIL' => 'N'
]);
```

#### Get Product Property | Получение свойства товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$property = \Bitrix\Catalog\Model\ProductProperty::getList([
    'filter' => ['ID' => $propertyId],
    'select' => ['*']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$property = CCatalogProduct::GetPropertyByID($propertyId);
```

#### Update Product Property | Обновление свойства товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\Model\ProductProperty::update($propertyId, [
    'NAME' => 'Updated Property Name',
    'SORT' => 200,
    'DEFAULT_VALUE' => 'Updated Default Value'
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogProduct::UpdateProperty($propertyId, [
    'NAME' => 'Updated Property Name',
    'SORT' => 200,
    'DEFAULT_VALUE' => 'Updated Default Value'
]);
```

#### Delete Product Property | Удаление свойства товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\Model\ProductProperty::delete($propertyId);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogProduct::DeleteProperty($propertyId);
```

## Handlers | Обработчики

### Product Handlers | Обработчики товаров

#### Product Handler | Обработчик товаров

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
class CustomProductHandler extends \Bitrix\Catalog\Model\Product\Handler
{
    public function onBeforeProductCreate($params)
    {
        // Code executed before product is created
        // Код, выполняемый перед созданием товара
        return $params;
    }
    
    public function onAfterProductCreate($params, $result)
    {
        // Code executed after product is created
        // Код, выполняемый после создания товара
        return $result;
    }
    
    public function onBeforeProductUpdate($params)
    {
        // Code executed before product is updated
        // Код, выполняемый перед обновлением товара
        return $params;
    }
    
    public function onAfterProductUpdate($params, $result)
    {
        // Code executed after product is updated
        // Код, выполняемый после обновления товара
        return $result;
    }
    
    public function onBeforeProductDelete($params)
    {
        // Code executed before product is deleted
        // Код, выполняемый перед удалением товара
        return $params;
    }
    
    public function onAfterProductDelete($params, $result)
    {
        // Code executed after product is deleted
        // Код, выполняемый после удаления товара
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Catalog\Model\Product\Handler::register('custom_product', CustomProductHandler::class);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
class CCustomProductHandler extends CCatalogProduct
{
    public function OnBeforeProductCreate($params)
    {
        // Code executed before product is created
        // Код, выполняемый перед созданием товара
        return $params;
    }
    
    public function OnAfterProductCreate($params, $result)
    {
        // Code executed after product is created
        // Код, выполняемый после создания товара
        return $result;
    }
    
    public function OnBeforeProductUpdate($params)
    {
        // Code executed before product is updated
        // Код, выполняемый перед обновлением товара
        return $params;
    }
    
    public function OnAfterProductUpdate($params, $result)
    {
        // Code executed after product is updated
        // Код, выполняемый после обновления товара
        return $result;
    }
    
    public function OnBeforeProductDelete($params)
    {
        // Code executed before product is deleted
        // Код, выполняемый перед удалением товара
        return $params;
    }
    
    public function OnAfterProductDelete($params, $result)
    {
        // Code executed after product is deleted
        // Код, выполняемый после удаления товара
        return $result;
    }
}

// Register handler
// Регистрация обработчика
AddEventHandler('catalog', 'OnBeforeProductCreate', ['CCustomProductHandler', 'OnBeforeProductCreate']);
AddEventHandler('catalog', 'OnAfterProductCreate', ['CCustomProductHandler', 'OnAfterProductCreate']);
AddEventHandler('catalog', 'OnBeforeProductUpdate', ['CCustomProductHandler', 'OnBeforeProductUpdate']);
AddEventHandler('catalog', 'OnAfterProductUpdate', ['CCustomProductHandler', 'OnAfterProductUpdate']);
AddEventHandler('catalog', 'OnBeforeProductDelete', ['CCustomProductHandler', 'OnBeforeProductDelete']);
AddEventHandler('catalog', 'OnAfterProductDelete', ['CCustomProductHandler', 'OnAfterProductDelete']);
```

### Price Handlers | Обработчики цен

#### Price Handler | Обработчик цен

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
class CustomPriceHandler extends \Bitrix\Catalog\Model\Price\Handler
{
    public function onBeforePriceCreate($params)
    {
        // Code executed before price is created
        // Код, выполняемый перед созданием цены
        return $params;
    }
    
    public function onAfterPriceCreate($params, $result)
    {
        // Code executed after price is created
        // Код, выполняемый после создания цены
        return $result;
    }
    
    public function onBeforePriceUpdate($params)
    {
        // Code executed before price is updated
        // Код, выполняемый перед обновлением цены
        return $params;
    }
    
    public function onAfterPriceUpdate($params, $result)
    {
        // Code executed after price is updated
        // Код, выполняемый после обновления цены
        return $result;
    }
    
    public function onBeforePriceDelete($params)
    {
        // Code executed before price is deleted
        // Код, выполняемый перед удалением цены
        return $params;
    }
    
    public function onAfterPriceDelete($params, $result)
    {
        // Code executed after price is deleted
        // Код, выполняемый после удаления цены
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Catalog\Model\Price\Handler::register('custom_price', CustomPriceHandler::class);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
class CCustomPriceHandler extends CPrice
{
    public function OnBeforePriceCreate($params)
    {
        // Code executed before price is created
        // Код, выполняемый перед созданием цены
        return $params;
    }
    
    public function OnAfterPriceCreate($params, $result)
    {
        // Code executed after price is created
        // Код, выполняемый после создания цены
        return $result;
    }
    
    public function OnBeforePriceUpdate($params)
    {
        // Code executed before price is updated
        // Код, выполняемый перед обновлением цены
        return $params;
    }
    
    public function OnAfterPriceUpdate($params, $result)
    {
        // Code executed after price is updated
        // Код, выполняемый после обновления цены
        return $result;
    }
    
    public function OnBeforePriceDelete($params)
    {
        // Code executed before price is deleted
        // Код, выполняемый перед удалением цены
        return $params;
    }
    
    public function OnAfterPriceDelete($params, $result)
    {
        // Code executed after price is deleted
        // Код, выполняемый после удаления цены
        return $result;
    }
}

// Register handler
// Регистрация обработчика
AddEventHandler('catalog', 'OnBeforePriceCreate', ['CCustomPriceHandler', 'OnBeforePriceCreate']);
AddEventHandler('catalog', 'OnAfterPriceCreate', ['CCustomPriceHandler', 'OnAfterPriceCreate']);
AddEventHandler('catalog', 'OnBeforePriceUpdate', ['CCustomPriceHandler', 'OnBeforePriceUpdate']);
AddEventHandler('catalog', 'OnAfterPriceUpdate', ['CCustomPriceHandler', 'OnAfterPriceUpdate']);
AddEventHandler('catalog', 'OnBeforePriceDelete', ['CCustomPriceHandler', 'OnBeforePriceDelete']);
AddEventHandler('catalog', 'OnAfterPriceDelete', ['CCustomPriceHandler', 'OnAfterPriceDelete']);
```

### Store Handlers | Обработчики складов

#### Store Handler | Обработчик складов

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
class CustomStoreHandler extends \Bitrix\Catalog\Model\Store\Handler
{
    public function onBeforeStoreCreate($params)
    {
        // Code executed before store is created
        // Код, выполняемый перед созданием склада
        return $params;
    }
    
    public function onAfterStoreCreate($params, $result)
    {
        // Code executed after store is created
        // Код, выполняемый после создания склада
        return $result;
    }
    
    public function onBeforeStoreUpdate($params)
    {
        // Code executed before store is updated
        // Код, выполняемый перед обновлением склада
        return $params;
    }
    
    public function onAfterStoreUpdate($params, $result)
    {
        // Code executed after store is updated
        // Код, выполняемый после обновления склада
        return $result;
    }
    
    public function onBeforeStoreDelete($params)
    {
        // Code executed before store is deleted
        // Код, выполняемый перед удалением склада
        return $params;
    }
    
    public function onAfterStoreDelete($params, $result)
    {
        // Code executed after store is deleted
        // Код, выполняемый после удаления склада
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Catalog\Model\Store\Handler::register('custom_store', CustomStoreHandler::class);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
class CCustomStoreHandler extends CCatalogStore
{
    public function OnBeforeStoreCreate($params)
    {
        // Code executed before store is created
        // Код, выполняемый перед созданием склада
        return $params;
    }
    
    public function OnAfterStoreCreate($params, $result)
    {
        // Code executed after store is created
        // Код, выполняемый после создания склада
        return $result;
    }
    
    public function OnBeforeStoreUpdate($params)
    {
        // Code executed before store is updated
        // Код, выполняемый перед обновлением склада
        return $params;
    }
    
    public function OnAfterStoreUpdate($params, $result)
    {
        // Code executed after store is updated
        // Код, выполняемый после обновления склада
        return $result;
    }
    
    public function OnBeforeStoreDelete($params)
    {
        // Code executed before store is deleted
        // Код, выполняемый перед удалением склада
        return $params;
    }
    
    public function OnAfterStoreDelete($params, $result)
    {
        // Code executed after store is deleted
        // Код, выполняемый после удаления склада
        return $result;
    }
}

// Register handler
// Регистрация обработчика
AddEventHandler('catalog', 'OnBeforeStoreCreate', ['CCustomStoreHandler', 'OnBeforeStoreCreate']);
AddEventHandler('catalog', 'OnAfterStoreCreate', ['CCustomStoreHandler', 'OnAfterStoreCreate']);
AddEventHandler('catalog', 'OnBeforeStoreUpdate', ['CCustomStoreHandler', 'OnBeforeStoreUpdate']);
AddEventHandler('catalog', 'OnAfterStoreUpdate', ['CCustomStoreHandler', 'OnAfterStoreUpdate']);
AddEventHandler('catalog', 'OnBeforeStoreDelete', ['CCustomStoreHandler', 'OnBeforeStoreDelete']);
AddEventHandler('catalog', 'OnAfterStoreDelete', ['CCustomStoreHandler', 'OnAfterStoreDelete']);
```

### Product Property Handlers | Обработчики свойств товаров

#### Product Property Handler | Обработчик свойств товаров

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
class CustomProductPropertyHandler extends \Bitrix\Catalog\Model\ProductProperty\Handler
{
    public function onBeforeProductPropertyCreate($params)
    {
        // Code executed before product property is created
        // Код, выполняемый перед созданием свойства товара
        return $params;
    }
    
    public function onAfterProductPropertyCreate($params, $result)
    {
        // Code executed after product property is created
        // Код, выполняемый после создания свойства товара
        return $result;
    }
    
    public function onBeforeProductPropertyUpdate($params)
    {
        // Code executed before product property is updated
        // Код, выполняемый перед обновлением свойства товара
        return $params;
    }
    
    public function onAfterProductPropertyUpdate($params, $result)
    {
        // Code executed after product property is updated
        // Код, выполняемый после обновления свойства товара
        return $result;
    }
    
    public function onBeforeProductPropertyDelete($params)
    {
        // Code executed before product property is deleted
        // Код, выполняемый перед удалением свойства товара
        return $params;
    }
    
    public function onAfterProductPropertyDelete($params, $result)
    {
        // Code executed after product property is deleted
        // Код, выполняемый после удаления свойства товара
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Catalog\Model\ProductProperty\Handler::register('custom_product_property', CustomProductPropertyHandler::class);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
class CCustomProductPropertyHandler extends CCatalogProduct
{
    public function OnBeforeProductPropertyCreate($params)
    {
        // Code executed before product property is created
        // Код, выполняемый перед созданием свойства товара
        return $params;
    }
    
    public function OnAfterProductPropertyCreate($params, $result)
    {
        // Code executed after product property is created
        // Код, выполняемый после создания свойства товара
        return $result;
    }
    
    public function OnBeforeProductPropertyUpdate($params)
    {
        // Code executed before product property is updated
        // Код, выполняемый перед обновлением свойства товара
        return $params;
    }
    
    public function OnAfterProductPropertyUpdate($params, $result)
    {
        // Code executed after product property is updated
        // Код, выполняемый после обновления свойства товара
        return $result;
    }
    
    public function OnBeforeProductPropertyDelete($params)
    {
        // Code executed before product property is deleted
        // Код, выполняемый перед удалением свойства товара
        return $params;
    }
    
    public function OnAfterProductPropertyDelete($params, $result)
    {
        // Code executed after product property is deleted
        // Код, выполняемый после удаления свойства товара
        return $result;
    }
}

// Register handler
// Регистрация обработчика
AddEventHandler('catalog', 'OnBeforeProductPropertyCreate', ['CCustomProductPropertyHandler', 'OnBeforeProductPropertyCreate']);
AddEventHandler('catalog', 'OnAfterProductPropertyCreate', ['CCustomProductPropertyHandler', 'OnAfterProductPropertyCreate']);
AddEventHandler('catalog', 'OnBeforeProductPropertyUpdate', ['CCustomProductPropertyHandler', 'OnBeforeProductPropertyUpdate']);
AddEventHandler('catalog', 'OnAfterProductPropertyUpdate', ['CCustomProductPropertyHandler', 'OnAfterProductPropertyUpdate']);
AddEventHandler('catalog', 'OnBeforeProductPropertyDelete', ['CCustomProductPropertyHandler', 'OnBeforeProductPropertyDelete']);
AddEventHandler('catalog', 'OnAfterProductPropertyDelete', ['CCustomProductPropertyHandler', 'OnAfterProductPropertyDelete']);
```