# Department Module | Модуль Подразделения

## Overview | Обзор

The Department module provides functionality for managing organizational structure, including departments, positions, and employee assignments. | Модуль Подразделения предоставляет функциональность для управления организационной структурой, включая подразделения, должности и назначения сотрудников.

## Methods | Методы

### Departments | Подразделения

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'department.get',
    [
        'filter' => ['ACTIVE' => 'Y'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$departments = \Bitrix\Iblock\SectionTable::getList([
    'select' => ['*', 'UF_*'],
    'filter' => ['=IBLOCK_ID' => 5, '=ACTIVE' => 'Y'],
    'order' => ['SORT' => 'ASC', 'NAME' => 'ASC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$departments = CIBlockSection::GetList(
    ['SORT' => 'ASC', 'NAME' => 'ASC'],
    ['IBLOCK_ID' => 5, 'ACTIVE' => 'Y'],
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
    'department.add',
    [
        'fields' => [
            'NAME' => 'New Department',
            'SORT' => 500,
            'PARENT' => 1,
            'UF_HEAD' => 1,
            'UF_PARENT' => 1
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\SectionTable::add([
    'NAME' => 'New Department',
    'CODE' => 'new-department',
    'IBLOCK_ID' => 5,
    'ACTIVE' => 'Y',
    'SORT' => 500,
    'SECTION_ID' => 1,
    'UF_HEAD' => 1,
    'UF_PARENT' => 1
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$departmentFields = [
    'NAME' => 'New Department',
    'CODE' => 'new-department',
    'IBLOCK_ID' => 5,
    'ACTIVE' => 'Y',
    'SORT' => 500,
    'SECTION_ID' => 1,
    'UF_HEAD' => 1,
    'UF_PARENT' => 1
];
$department = new CIBlockSection();
$departmentId = $department->Add($departmentFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'department.update',
    [
        'ID' => 123,
        'fields' => [
            'NAME' => 'Updated Department',
            'UF_HEAD' => 2
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\SectionTable::update(123, [
    'NAME' => 'Updated Department',
    'UF_HEAD' => 2
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$departmentFields = [
    'NAME' => 'Updated Department',
    'UF_HEAD' => 2
];
$department = new CIBlockSection();
$department->Update(123, $departmentFields);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'department.delete',
    ['ID' => 123]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\SectionTable::delete(123);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$department = new CIBlockSection();
$department->Delete(123);
```

### Positions | Должности

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'user.position.get',
    [
        'filter' => ['ACTIVE' => 'Y'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$positions = \Bitrix\Iblock\ElementTable::getList([
    'select' => ['*', 'PROPERTY_*'],
    'filter' => ['=IBLOCK_ID' => 46, '=ACTIVE' => 'Y'],
    'order' => ['SORT' => 'ASC', 'NAME' => 'ASC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$positions = CIBlockElement::GetList(
    ['SORT' => 'ASC', 'NAME' => 'ASC'],
    ['IBLOCK_ID' => 46, 'ACTIVE' => 'Y'],
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
    'user.position.add',
    [
        'fields' => [
            'NAME' => 'New Position',
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
    'NAME' => 'New Position',
    'CODE' => 'new-position',
    'IBLOCK_ID' => 46,
    'ACTIVE' => 'Y',
    'SORT' => 500
]);

// Add properties after element creation
// Добавление свойств после создания элемента
\Bitrix\Iblock\Element::setPropertyValues($elementId, 46, 'Property Value', 'PROPERTY_CODE');

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$positionFields = [
    'NAME' => 'New Position',
    'CODE' => 'new-position',
    'IBLOCK_ID' => 46,
    'ACTIVE' => 'Y',
    'SORT' => 500
];
$position = new CIBlockElement();
$positionId = $position->Add($positionFields);

// Add properties after element creation
// Добавление свойств после создания элемента
$position->SetPropertyValues($positionId, 'Property Value', 'PROPERTY_CODE');
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'user.position.update',
    [
        'ID' => 123,
        'fields' => [
            'NAME' => 'Updated Position',
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
    'NAME' => 'Updated Position'
]);

// Update properties
// Обновление свойств
\Bitrix\Iblock\Element::setPropertyValues(123, 46, 'Updated Property Value', 'PROPERTY_CODE');

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$positionFields = [
    'NAME' => 'Updated Position'
];
$position = new CIBlockElement();
$position->Update(123, $positionFields);

// Update properties
// Обновление свойств
$position->SetPropertyValues(123, 'Updated Property Value', 'PROPERTY_CODE');
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'user.position.delete',
    ['ID' => 123]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('iblock')
// Требуется: Bitrix\Main\Loader::includeModule('iblock')
$result = \Bitrix\Iblock\ElementTable::delete(123);

// Legacy
// Requires: CModule::IncludeModule('iblock')
// Требуется: CModule::IncludeModule('iblock')
$position = new CIBlockElement();
$position->Delete(123);
```

### Employee Assignments | Назначения сотрудников

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'user.get',
    [
        'filter' => ['ACTIVE' => true, 'UF_DEPARTMENT' => [1, 2]],
        'sort' => ['ID' => 'DESC'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$employees = \Bitrix\Main\UserTable::getList([
    'select' => ['*', 'UF_*'],
    'filter' => ['=ACTIVE' => 'Y', '=UF_DEPARTMENT' => [1, 2]],
    'order' => ['ID' => 'DESC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$employees = CUser::GetList(
    ['ID' => 'DESC'],
    ['ACTIVE' => 'Y', 'UF_DEPARTMENT' => [1, 2]],
    ['*', 'UF_*'],
    ['nTopCount' => 50]
);
```

#### Assign to Department | Назначение в подразделение

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'user.update',
    [
        'ID' => 123,
        'fields' => [
            'UF_DEPARTMENT' => [1, 2]
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$result = \Bitrix\Main\UserTable::update(123, [
    'UF_DEPARTMENT' => [1, 2]
]);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$userFields = [
    'UF_DEPARTMENT' => [1, 2]
];
$user = new CUser();
$user->Update(123, $userFields);
```

#### Assign Position | Назначение должности

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'user.update',
    [
        'ID' => 123,
        'fields' => [
            'WORK_POSITION' => 'Senior Developer'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$result = \Bitrix\Main\UserTable::update(123, [
    'WORK_POSITION' => 'Senior Developer'
]);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$userFields = [
    'WORK_POSITION' => 'Senior Developer'
];
$user = new CUser();
$user->Update(123, $userFields);
``` 