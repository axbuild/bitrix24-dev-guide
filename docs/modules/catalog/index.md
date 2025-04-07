# Catalog Module | Модуль Каталог

## Overview | Обзор

The Catalog module provides functionality for managing products, prices, and product properties in Bitrix24. It is essential for e-commerce operations and product management. | Модуль Каталог предоставляет функциональность для управления товарами, ценами и свойствами товаров в Bitrix24. Он необходим для операций электронной коммерции и управления товарами.

## Methods | Методы

### Products | Товары

#### Get Product | Получение товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$product = \Bitrix\Catalog\ProductTable::getList([
    'filter' => ['=ID' => $productId],
    'select' => ['*', 'ELEMENT.NAME', 'ELEMENT.DETAIL_PAGE_URL']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$product = CCatalogProduct::GetByID($productId);
```

#### Get Product List | Получение списка товаров

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$products = \Bitrix\Catalog\ProductTable::getList([
    'filter' => ['=ACTIVE' => 'Y'],
    'select' => ['*', 'ELEMENT.NAME', 'ELEMENT.DETAIL_PAGE_URL'],
    'limit' => 10
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$products = CCatalogProduct::GetList(
    ['ID' => 'ASC'],
    ['ACTIVE' => 'Y'],
    false,
    ['nTopCount' => 10],
    ['*', 'ELEMENT.NAME', 'ELEMENT.DETAIL_PAGE_URL']
);
```

#### Add Product | Добавление товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\ProductTable::add([
    'ID' => $elementId,
    'QUANTITY' => 100,
    'QUANTITY_TRACE' => 'Y',
    'WEIGHT' => 1000,
    'PRICE_TYPE' => 'S',
    'CAN_BUY_ZERO' => 'N',
    'NEGATIVE_AMOUNT_TRACE' => 'N',
    'TMP_ID' => null,
    'TYPE' => \Bitrix\Catalog\ProductTable::TYPE_PRODUCT,
    'AVAILABLE' => 'Y',
    'BUNDLE' => 'N'
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogProduct::Add([
    'ID' => $elementId,
    'QUANTITY' => 100,
    'QUANTITY_TRACE' => 'Y',
    'WEIGHT' => 1000,
    'PRICE_TYPE' => 'S',
    'CAN_BUY_ZERO' => 'N',
    'NEGATIVE_AMOUNT_TRACE' => 'N',
    'TMP_ID' => null,
    'TYPE' => CCatalogProduct::TYPE_PRODUCT,
    'AVAILABLE' => 'Y',
    'BUNDLE' => 'N'
]);
```

#### Update Product | Обновление товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\ProductTable::update($productId, [
    'QUANTITY' => 50,
    'AVAILABLE' => 'Y'
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogProduct::Update($productId, [
    'QUANTITY' => 50,
    'AVAILABLE' => 'Y'
]);
```

#### Delete Product | Удаление товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\ProductTable::delete($productId);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogProduct::Delete($productId);
```

### Prices | Цены

#### Get Price | Получение цены

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$price = \Bitrix\Catalog\PriceTable::getList([
    'filter' => [
        '=PRODUCT_ID' => $productId,
        '=CATALOG_GROUP_ID' => $priceTypeId
    ]
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$price = CCatalogProduct::GetOptimalPrice($productId, 1, $USER->GetUserGroupArray());
```

#### Get Price List | Получение списка цен

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$prices = \Bitrix\Catalog\PriceTable::getList([
    'filter' => ['=PRODUCT_ID' => $productId],
    'select' => ['*', 'CATALOG_GROUP.NAME']
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$prices = CCatalogProduct::GetPriceList($productId);
```

#### Set Price | Установка цены

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\PriceTable::setBasePrice($productId, $price, $currency);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogProduct::SetOptimalPrice($productId, $price, $currency);
```

#### Update Price | Обновление цены

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\PriceTable::update($priceId, [
    'PRICE' => $newPrice,
    'CURRENCY' => $currency
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogProduct::UpdatePrice($productId, $priceTypeId, $newPrice, $currency);
```

#### Delete Price | Удаление цены

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\PriceTable::delete($priceId);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogProduct::DeletePrice($productId, $priceTypeId);
```

### Price Types | Типы цен

#### Get Price Types | Получение типов цен

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$priceTypes = \Bitrix\Catalog\GroupTable::getList([
    'filter' => ['=BASE' => 'N'],
    'select' => ['*']
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$priceTypes = CCatalogGroup::GetList(
    ['SORT' => 'ASC'],
    ['BASE' => 'N']
);
```

#### Add Price Type | Добавление типа цены

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\GroupTable::add([
    'NAME' => 'Wholesale Price',
    'BASE' => 'N',
    'SORT' => 100,
    'XML_ID' => 'WHOLESALE',
    'DESCRIPTION' => 'Wholesale price for bulk purchases'
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogGroup::Add([
    'NAME' => 'Wholesale Price',
    'BASE' => 'N',
    'SORT' => 100,
    'XML_ID' => 'WHOLESALE',
    'DESCRIPTION' => 'Wholesale price for bulk purchases'
]);
```

#### Update Price Type | Обновление типа цены

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\GroupTable::update($priceTypeId, [
    'NAME' => 'New Wholesale Price',
    'SORT' => 200
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogGroup::Update($priceTypeId, [
    'NAME' => 'New Wholesale Price',
    'SORT' => 200
]);
```

#### Delete Price Type | Удаление типа цены

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\GroupTable::delete($priceTypeId);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogGroup::Delete($priceTypeId);
```

### Product Properties | Свойства товаров

#### Get Product Properties | Получение свойств товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$properties = \Bitrix\Catalog\ProductPropertyTable::getList([
    'filter' => ['=PRODUCT_ID' => $productId],
    'select' => ['*', 'PROPERTY.NAME']
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$properties = CCatalogProduct::GetProductProperties($productId);
```

#### Set Product Property | Установка свойства товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\ProductPropertyTable::add([
    'PRODUCT_ID' => $productId,
    'PROPERTY_ID' => $propertyId,
    'VALUE' => $propertyValue
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogProduct::SetProductProperties($productId, [
    $propertyId => $propertyValue
]);
```

#### Update Product Property | Обновление свойства товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\ProductPropertyTable::update($propertyId, [
    'VALUE' => $newPropertyValue
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogProduct::SetProductProperties($productId, [
    $propertyId => $newPropertyValue
]);
```

#### Delete Product Property | Удаление свойства товара

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Catalog\ProductPropertyTable::delete($propertyId);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogProduct::DeleteProductProperties($productId, [$propertyId]);
```

### Product Sections | Разделы товаров

#### Get Section | Получение раздела

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$section = \Bitrix\Iblock\SectionTable::getList([
    'filter' => ['=ID' => $sectionId],
    'select' => ['*']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$section = CCatalogSection::GetByID($sectionId);
```

#### Get Section List | Получение списка разделов

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$sections = \Bitrix\Iblock\SectionTable::getList([
    'filter' => ['=IBLOCK_ID' => $iblockId, '=ACTIVE' => 'Y'],
    'select' => ['*'],
    'order' => ['SORT' => 'ASC']
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$sections = CCatalogSection::GetList(
    ['SORT' => 'ASC'],
    ['IBLOCK_ID' => $iblockId, 'ACTIVE' => 'Y']
);
```

#### Add Section | Добавление раздела

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Iblock\SectionTable::add([
    'IBLOCK_ID' => $iblockId,
    'NAME' => 'New Section',
    'CODE' => 'new-section',
    'SORT' => 100,
    'ACTIVE' => 'Y',
    'DESCRIPTION' => 'Section description',
    'DESCRIPTION_TYPE' => 'text',
    'PICTURE' => null,
    'DETAIL_PICTURE' => null,
    'XML_ID' => 'NEW_SECTION_XML_ID'
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogSection::Add([
    'IBLOCK_ID' => $iblockId,
    'NAME' => 'New Section',
    'CODE' => 'new-section',
    'SORT' => 100,
    'ACTIVE' => 'Y',
    'DESCRIPTION' => 'Section description',
    'DESCRIPTION_TYPE' => 'text',
    'PICTURE' => null,
    'DETAIL_PICTURE' => null,
    'XML_ID' => 'NEW_SECTION_XML_ID'
]);
```

#### Update Section | Обновление раздела

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Iblock\SectionTable::update($sectionId, [
    'NAME' => 'Updated Section',
    'SORT' => 200
]);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogSection::Update($sectionId, [
    'NAME' => 'Updated Section',
    'SORT' => 200
]);
```

#### Delete Section | Удаление раздела

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('catalog')
// Требуется: Bitrix\Main\Loader::includeModule('catalog')
$result = \Bitrix\Iblock\SectionTable::delete($sectionId);

// Legacy
// Requires: CModule::IncludeModule('catalog')
// Требуется: CModule::IncludeModule('catalog')
$result = CCatalogSection::Delete($sectionId);
``` 