# Iblock Module | Модуль Информационные блоки

## Overview | Обзор

The Iblock module provides functionality for managing information blocks, their elements, sections, and properties in Bitrix24. It is a core module for content management and data structuring. | Модуль Информационные блоки предоставляет функциональность для управления информационными блоками, их элементами, разделами и свойствами в Bitrix24. Это основной модуль для управления контентом и структурирования данных.

## Methods | Методы

### Information Blocks | Информационные блоки

#### Get Iblock | Получение информационного блока

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$iblock = \Bitrix\Iblock\IblockTable::getList([
    'filter' => ['=ID' => $iblockId],
    'select' => ['*']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$iblock = CIBlock::GetByID($iblockId)->Fetch();
```

#### Get Iblock List | Получение списка информационных блоков

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$iblocks = \Bitrix\Iblock\IblockTable::getList([
    'filter' => ['=ACTIVE' => 'Y'],
    'select' => ['*'],
    'order' => ['SORT' => 'ASC']
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$iblocks = CIBlock::GetList(
    ['SORT' => 'ASC'],
    ['ACTIVE' => 'Y']
);
```

#### Add Iblock | Добавление информационного блока

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\IblockTable::add([
    'NAME' => 'News',
    'CODE' => 'news',
    'IBLOCK_TYPE_ID' => 'content',
    'SITE_ID' => ['s1'],
    'SORT' => 100,
    'GROUP_ID' => ['1' => 'X', '2' => 'R'],
    'VERSION' => 2,
    'ACTIVE' => 'Y',
    'DESCRIPTION' => 'News information block',
    'DESCRIPTION_TYPE' => 'text',
    'XML_ID' => 'NEWS_IBLOCK_XML_ID'
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$result = CIBlock::Add([
    'NAME' => 'News',
    'CODE' => 'news',
    'IBLOCK_TYPE_ID' => 'content',
    'SITE_ID' => ['s1'],
    'SORT' => 100,
    'GROUP_ID' => ['1' => 'X', '2' => 'R'],
    'VERSION' => 2,
    'ACTIVE' => 'Y',
    'DESCRIPTION' => 'News information block',
    'DESCRIPTION_TYPE' => 'text',
    'XML_ID' => 'NEWS_IBLOCK_XML_ID'
]);
```

#### Update Iblock | Обновление информационного блока

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\IblockTable::update($iblockId, [
    'NAME' => 'Updated News',
    'SORT' => 200
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$result = CIBlock::SetFields($iblockId, [
    'NAME' => 'Updated News',
    'SORT' => 200
]);
```

#### Delete Iblock | Удаление информационного блока

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\IblockTable::delete($iblockId);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$result = CIBlock::Delete($iblockId);
```

### Elements | Элементы

#### Get Element | Получение элемента

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$element = \Bitrix\Iblock\ElementTable::getList([
    'filter' => ['=ID' => $elementId],
    'select' => ['*', 'PROPERTY_*']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$element = CIBlockElement::GetByID($elementId)->Fetch();
```

#### Get Element List | Получение списка элементов

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$elements = \Bitrix\Iblock\ElementTable::getList([
    'filter' => [
        '=IBLOCK_ID' => $iblockId,
        '=ACTIVE' => 'Y'
    ],
    'select' => ['*', 'PROPERTY_*'],
    'order' => ['SORT' => 'ASC'],
    'limit' => 10
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$elements = CIBlockElement::GetList(
    ['SORT' => 'ASC'],
    ['IBLOCK_ID' => $iblockId, 'ACTIVE' => 'Y'],
    false,
    ['nTopCount' => 10],
    ['*', 'PROPERTY_*']
);
```

#### Add Element | Добавление элемента

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\ElementTable::add([
    'IBLOCK_ID' => $iblockId,
    'NAME' => 'New Element',
    'CODE' => 'new-element',
    'ACTIVE' => 'Y',
    'SORT' => 100,
    'PREVIEW_TEXT' => 'Preview text',
    'PREVIEW_TEXT_TYPE' => 'text',
    'DETAIL_TEXT' => 'Detail text',
    'DETAIL_TEXT_TYPE' => 'text',
    'DATE_ACTIVE_FROM' => new \Bitrix\Main\Type\DateTime(),
    'DATE_ACTIVE_TO' => new \Bitrix\Main\Type\DateTime(),
    'XML_ID' => 'NEW_ELEMENT_XML_ID'
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$result = CIBlockElement::Add([
    'IBLOCK_ID' => $iblockId,
    'NAME' => 'New Element',
    'CODE' => 'new-element',
    'ACTIVE' => 'Y',
    'SORT' => 100,
    'PREVIEW_TEXT' => 'Preview text',
    'PREVIEW_TEXT_TYPE' => 'text',
    'DETAIL_TEXT' => 'Detail text',
    'DETAIL_TEXT_TYPE' => 'text',
    'DATE_ACTIVE_FROM' => new \Bitrix\Main\Type\DateTime(),
    'DATE_ACTIVE_TO' => new \Bitrix\Main\Type\DateTime(),
    'XML_ID' => 'NEW_ELEMENT_XML_ID'
]);
```

#### Update Element | Обновление элемента

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\ElementTable::update($elementId, [
    'NAME' => 'Updated Element',
    'SORT' => 200
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$result = CIBlockElement::Update($elementId, [
    'NAME' => 'Updated Element',
    'SORT' => 200
]);
```

#### Delete Element | Удаление элемента

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\ElementTable::delete($elementId);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$result = CIBlockElement::Delete($elementId);
```

### Sections | Разделы

#### Get Section | Получение раздела

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$section = \Bitrix\Iblock\SectionTable::getList([
    'filter' => ['=ID' => $sectionId],
    'select' => ['*']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$section = CIBlockSection::GetByID($sectionId)->Fetch();
```

#### Get Section List | Получение списка разделов

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$sections = \Bitrix\Iblock\SectionTable::getList([
    'filter' => [
        '=IBLOCK_ID' => $iblockId,
        '=ACTIVE' => 'Y'
    ],
    'select' => ['*'],
    'order' => ['SORT' => 'ASC']
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$sections = CIBlockSection::GetList(
    ['SORT' => 'ASC'],
    ['IBLOCK_ID' => $iblockId, 'ACTIVE' => 'Y']
);
```

#### Add Section | Добавление раздела

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
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
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$result = CIBlockSection::Add([
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
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\SectionTable::update($sectionId, [
    'NAME' => 'Updated Section',
    'SORT' => 200
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$result = CIBlockSection::Update($sectionId, [
    'NAME' => 'Updated Section',
    'SORT' => 200
]);
```

#### Delete Section | Удаление раздела

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\SectionTable::delete($sectionId);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$result = CIBlockSection::Delete($sectionId);
```

### Properties | Свойства

#### Get Property | Получение свойства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$property = \Bitrix\Iblock\PropertyTable::getList([
    'filter' => ['=ID' => $propertyId],
    'select' => ['*']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$property = CIBlockProperty::GetByID($propertyId)->Fetch();
```

#### Get Property List | Получение списка свойств

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$properties = \Bitrix\Iblock\PropertyTable::getList([
    'filter' => [
        '=IBLOCK_ID' => $iblockId,
        '=ACTIVE' => 'Y'
    ],
    'select' => ['*'],
    'order' => ['SORT' => 'ASC']
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$properties = CIBlockProperty::GetList(
    ['SORT' => 'ASC'],
    ['IBLOCK_ID' => $iblockId, 'ACTIVE' => 'Y']
);
```

#### Add Property | Добавление свойства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\PropertyTable::add([
    'IBLOCK_ID' => $iblockId,
    'NAME' => 'New Property',
    'CODE' => 'new_property',
    'PROPERTY_TYPE' => 'S',
    'SORT' => 100,
    'ACTIVE' => 'Y',
    'WITH_DESCRIPTION' => 'N',
    'MULTIPLE' => 'N',
    'MULTIPLE_CNT' => 1,
    'IS_REQUIRED' => 'N',
    'XML_ID' => 'NEW_PROPERTY_XML_ID'
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$result = CIBlockProperty::Add([
    'IBLOCK_ID' => $iblockId,
    'NAME' => 'New Property',
    'CODE' => 'new_property',
    'PROPERTY_TYPE' => 'S',
    'SORT' => 100,
    'ACTIVE' => 'Y',
    'WITH_DESCRIPTION' => 'N',
    'MULTIPLE' => 'N',
    'MULTIPLE_CNT' => 1,
    'IS_REQUIRED' => 'N',
    'XML_ID' => 'NEW_PROPERTY_XML_ID'
]);
```

#### Update Property | Обновление свойства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\PropertyTable::update($propertyId, [
    'NAME' => 'Updated Property',
    'SORT' => 200
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$result = CIBlockProperty::Update($propertyId, [
    'NAME' => 'Updated Property',
    'SORT' => 200
]);
```

#### Delete Property | Удаление свойства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\PropertyTable::delete($propertyId);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$result = CIBlockProperty::Delete($propertyId);
```

### Property Values | Значения свойств

#### Get Property Value | Получение значения свойства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$propertyValue = \Bitrix\Iblock\ElementPropertyTable::getList([
    'filter' => [
        '=IBLOCK_PROPERTY_ID' => $propertyId,
        '=IBLOCK_ELEMENT_ID' => $elementId
    ],
    'select' => ['*']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$propertyValue = CIBlockElement::GetProperty(
    $iblockId,
    $elementId,
    ['sort' => 'asc'],
    ['ID' => $propertyId]
)->Fetch();
```

#### Get Property Values | Получение значений свойств

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$propertyValues = \Bitrix\Iblock\ElementPropertyTable::getList([
    'filter' => ['=IBLOCK_ELEMENT_ID' => $elementId],
    'select' => ['*', 'PROPERTY.NAME']
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$propertyValues = CIBlockElement::GetProperty(
    $iblockId,
    $elementId,
    ['sort' => 'asc'],
    ['*']
);
```

#### Set Property Value | Установка значения свойства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\ElementPropertyTable::add([
    'IBLOCK_PROPERTY_ID' => $propertyId,
    'IBLOCK_ELEMENT_ID' => $elementId,
    'VALUE' => 'Property value',
    'DESCRIPTION' => 'Property description'
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$result = CIBlockElement::SetPropertyValues(
    $elementId,
    $iblockId,
    'Property value',
    $propertyId
);
```

#### Update Property Value | Обновление значения свойства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\ElementPropertyTable::update($propertyValueId, [
    'VALUE' => 'Updated property value',
    'DESCRIPTION' => 'Updated property description'
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$result = CIBlockElement::SetPropertyValues(
    $elementId,
    $iblockId,
    'Updated property value',
    $propertyId
);
```

#### Delete Property Value | Удаление значения свойства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\ElementPropertyTable::delete($propertyValueId);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$result = CIBlockElement::SetPropertyValues(
    $elementId,
    $iblockId,
    null,
    $propertyId
);
``` 