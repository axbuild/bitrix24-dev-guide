# Iblock Module | Модуль Информационные блоки

## Overview | Обзор

The Iblock module provides functionality for managing information blocks, including elements, properties, and sections. | Модуль Информационные блоки предоставляет функциональность для управления информационными блоками, включая элементы, свойства и разделы.

## Methods | Методы

### Elements | Элементы

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.iblock.element.list',
    [
        'iblockId' => 1,
        'select' => ['*', 'PROPERTY_*'],
        'filter' => ['ACTIVE' => 'Y'],
        'order' => ['SORT' => 'ASC', 'ID' => 'DESC'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$elements = \Bitrix\Iblock\ElementTable::getList([
    'select' => ['*', 'PROPERTY_*'],
    'filter' => ['=IBLOCK_ID' => 1, '=ACTIVE' => 'Y'],
    'order' => ['SORT' => 'ASC', 'ID' => 'DESC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$elements = CIBlockElement::GetList(
    ['SORT' => 'ASC', 'ID' => 'DESC'],
    ['IBLOCK_ID' => 1, 'ACTIVE' => 'Y'],
    false,
    ['nTopCount' => 50],
    ['*', 'PROPERTY_*']
);
```

#### Add | Добавление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.iblock.element.add',
    [
        'iblockId' => 1,
        'fields' => [
            'NAME' => 'New Element',
            'CODE' => 'new-element',
            'IBLOCK_ID' => 1,
            'ACTIVE' => 'Y',
            'SORT' => 500,
            'PROPERTY_VALUES' => [
                'PROPERTY_CODE' => 'Property Value'
            ]
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\ElementTable::add([
    'NAME' => 'New Element',
    'CODE' => 'new-element',
    'IBLOCK_ID' => 1,
    'ACTIVE' => 'Y',
    'SORT' => 500
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$elementFields = [
    'NAME' => 'New Element',
    'CODE' => 'new-element',
    'IBLOCK_ID' => 1,
    'ACTIVE' => 'Y',
    'SORT' => 500
];
$element = new CIBlockElement();
$elementId = $element->Add($elementFields);

// Add properties after element creation
// Добавление свойств после создания элемента
$element->SetPropertyValues($elementId, 'Property Value', 'PROPERTY_CODE');
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.iblock.element.update',
    [
        'iblockId' => 1,
        'elementId' => 123,
        'fields' => [
            'NAME' => 'Updated Element',
            'ACTIVE' => 'N',
            'PROPERTY_VALUES' => [
                'PROPERTY_CODE' => 'Updated Property Value'
            ]
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\ElementTable::update(123, [
    'NAME' => 'Updated Element',
    'ACTIVE' => 'N'
]);

// Update properties
// Обновление свойств
\Bitrix\Iblock\Element::setPropertyValues(123, 1, 'Updated Property Value', 'PROPERTY_CODE');

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$elementFields = [
    'NAME' => 'Updated Element',
    'ACTIVE' => 'N'
];
$element = new CIBlockElement();
$element->Update(123, $elementFields);

// Update properties
// Обновление свойств
$element->SetPropertyValues(123, 'Updated Property Value', 'PROPERTY_CODE');
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.iblock.element.delete',
    [
        'iblockId' => 1,
        'elementId' => 123
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\ElementTable::delete(123);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$element = new CIBlockElement();
$element->Delete(123);
```

### Sections | Разделы

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.iblock.section.list',
    [
        'iblockId' => 1,
        'select' => ['*', 'UF_*'],
        'filter' => ['ACTIVE' => 'Y'],
        'order' => ['SORT' => 'ASC', 'ID' => 'DESC'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$sections = \Bitrix\Iblock\SectionTable::getList([
    'select' => ['*', 'UF_*'],
    'filter' => ['=IBLOCK_ID' => 1, '=ACTIVE' => 'Y'],
    'order' => ['SORT' => 'ASC', 'ID' => 'DESC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$sections = CIBlockSection::GetList(
    ['SORT' => 'ASC', 'ID' => 'DESC'],
    ['IBLOCK_ID' => 1, 'ACTIVE' => 'Y'],
    false,
    ['*', 'UF_*'],
    ['nTopCount' => 50]
);
```

#### Add | Добавление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.iblock.section.add',
    [
        'iblockId' => 1,
        'fields' => [
            'NAME' => 'New Section',
            'CODE' => 'new-section',
            'IBLOCK_ID' => 1,
            'ACTIVE' => 'Y',
            'SORT' => 500,
            'SECTION_ID' => 0,
            'DESCRIPTION' => 'Section description'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\SectionTable::add([
    'NAME' => 'New Section',
    'CODE' => 'new-section',
    'IBLOCK_ID' => 1,
    'ACTIVE' => 'Y',
    'SORT' => 500,
    'SECTION_ID' => 0,
    'DESCRIPTION' => 'Section description'
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$sectionFields = [
    'NAME' => 'New Section',
    'CODE' => 'new-section',
    'IBLOCK_ID' => 1,
    'ACTIVE' => 'Y',
    'SORT' => 500,
    'SECTION_ID' => 0,
    'DESCRIPTION' => 'Section description'
];
$section = new CIBlockSection();
$sectionId = $section->Add($sectionFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.iblock.section.update',
    [
        'iblockId' => 1,
        'sectionId' => 123,
        'fields' => [
            'NAME' => 'Updated Section',
            'ACTIVE' => 'N',
            'DESCRIPTION' => 'Updated description'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\SectionTable::update(123, [
    'NAME' => 'Updated Section',
    'ACTIVE' => 'N',
    'DESCRIPTION' => 'Updated description'
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$sectionFields = [
    'NAME' => 'Updated Section',
    'ACTIVE' => 'N',
    'DESCRIPTION' => 'Updated description'
];
$section = new CIBlockSection();
$section->Update(123, $sectionFields);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.iblock.section.delete',
    [
        'iblockId' => 1,
        'sectionId' => 123
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\SectionTable::delete(123);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$section = new CIBlockSection();
$section->Delete(123);
```

### Properties | Свойства

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.iblock.property.list',
    [
        'iblockId' => 1,
        'select' => ['*'],
        'filter' => ['ACTIVE' => 'Y'],
        'order' => ['SORT' => 'ASC', 'ID' => 'DESC'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$properties = \Bitrix\Iblock\PropertyTable::getList([
    'select' => ['*'],
    'filter' => ['=IBLOCK_ID' => 1, '=ACTIVE' => 'Y'],
    'order' => ['SORT' => 'ASC', 'ID' => 'DESC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$properties = CIBlockProperty::GetList(
    ['SORT' => 'ASC', 'ID' => 'DESC'],
    ['IBLOCK_ID' => 1, 'ACTIVE' => 'Y']
);
```

#### Add | Добавление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.iblock.property.add',
    [
        'iblockId' => 1,
        'fields' => [
            'NAME' => 'New Property',
            'CODE' => 'NEW_PROPERTY',
            'IBLOCK_ID' => 1,
            'ACTIVE' => 'Y',
            'SORT' => 500,
            'PROPERTY_TYPE' => 'S',
            'WITH_DESCRIPTION' => 'N',
            'MULTIPLE' => 'N',
            'IS_REQUIRED' => 'N'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\PropertyTable::add([
    'NAME' => 'New Property',
    'CODE' => 'NEW_PROPERTY',
    'IBLOCK_ID' => 1,
    'ACTIVE' => 'Y',
    'SORT' => 500,
    'PROPERTY_TYPE' => 'S',
    'WITH_DESCRIPTION' => 'N',
    'MULTIPLE' => 'N',
    'IS_REQUIRED' => 'N'
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$propertyFields = [
    'NAME' => 'New Property',
    'CODE' => 'NEW_PROPERTY',
    'IBLOCK_ID' => 1,
    'ACTIVE' => 'Y',
    'SORT' => 500,
    'PROPERTY_TYPE' => 'S',
    'WITH_DESCRIPTION' => 'N',
    'MULTIPLE' => 'N',
    'IS_REQUIRED' => 'N'
];
$property = new CIBlockProperty();
$propertyId = $property->Add($propertyFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.iblock.property.update',
    [
        'iblockId' => 1,
        'propertyId' => 123,
        'fields' => [
            'NAME' => 'Updated Property',
            'ACTIVE' => 'N',
            'IS_REQUIRED' => 'Y'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\PropertyTable::update(123, [
    'NAME' => 'Updated Property',
    'ACTIVE' => 'N',
    'IS_REQUIRED' => 'Y'
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$propertyFields = [
    'NAME' => 'Updated Property',
    'ACTIVE' => 'N',
    'IS_REQUIRED' => 'Y'
];
$property = new CIBlockProperty();
$property->Update(123, $propertyFields);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.iblock.property.delete',
    [
        'iblockId' => 1,
        'propertyId' => 123
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\PropertyTable::delete(123);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$property = new CIBlockProperty();
$property->Delete(123);
``` 