# Добавление / Add

[English](#english) | [Русский](#russian)

## English

### CRM Module

#### REST API
```php
$result = CRest::call('crm.lead.add', [
    'fields' => [
        'TITLE' => 'New Lead',
        'NAME' => 'John',
        'LAST_NAME' => 'Doe',
        'STATUS_ID' => 'NEW'
    ]
]);
```

#### D7
```php
use Bitrix\Crm\LeadTable;

$result = LeadTable::add([
    'TITLE' => 'New Lead',
    'NAME' => 'John',
    'LAST_NAME' => 'Doe',
    'STATUS_ID' => 'NEW'
]);
```

#### Legacy
```php
$fields = [
    'TITLE' => 'New Lead',
    'NAME' => 'John',
    'LAST_NAME' => 'Doe',
    'STATUS_ID' => 'NEW'
];
$lead = new CCrmLead(false);
$result = $lead->Add($fields);
```

### Information Blocks

#### REST API
```php
$result = CRest::call('crm.lead.add', [
    'fields' => [
        'IBLOCK_ID' => 1,
        'NAME' => 'New Element',
        'PROPERTY_VALUES' => [
            'PROPERTY_CODE' => 'Value'
        ]
    ]
]);
```

#### D7
```php
use Bitrix\Iblock\Elements\ElementTable;

$result = ElementTable::add([
    'IBLOCK_ID' => 1,
    'NAME' => 'New Element',
    'PROPERTY_VALUES' => [
        'PROPERTY_CODE' => 'Value'
    ]
]);
```

#### Legacy
```php
$fields = [
    'IBLOCK_ID' => 1,
    'NAME' => 'New Element',
    'PROPERTY_VALUES' => [
        'PROPERTY_CODE' => 'Value'
    ]
];
$element = new CIBlockElement;
$result = $element->Add($fields);
```

## Русский

### Модуль CRM

#### REST API
```php
$result = CRest::call('crm.lead.add', [
    'fields' => [
        'TITLE' => 'Новый лид',
        'NAME' => 'Иван',
        'LAST_NAME' => 'Иванов',
        'STATUS_ID' => 'NEW'
    ]
]);
```

#### D7
```php
use Bitrix\Crm\LeadTable;

$result = LeadTable::add([
    'TITLE' => 'Новый лид',
    'NAME' => 'Иван',
    'LAST_NAME' => 'Иванов',
    'STATUS_ID' => 'NEW'
]);
```

#### Старое ядро
```php
$fields = [
    'TITLE' => 'Новый лид',
    'NAME' => 'Иван',
    'LAST_NAME' => 'Иванов',
    'STATUS_ID' => 'NEW'
];
$lead = new CCrmLead(false);
$result = $lead->Add($fields);
```

### Информационные блоки

#### REST API
```php
$result = CRest::call('crm.lead.add', [
    'fields' => [
        'IBLOCK_ID' => 1,
        'NAME' => 'Новый элемент',
        'PROPERTY_VALUES' => [
            'PROPERTY_CODE' => 'Значение'
        ]
    ]
]);
```

#### D7
```php
use Bitrix\Iblock\Elements\ElementTable;

$result = ElementTable::add([
    'IBLOCK_ID' => 1,
    'NAME' => 'Новый элемент',
    'PROPERTY_VALUES' => [
        'PROPERTY_CODE' => 'Значение'
    ]
]);
```

#### Старое ядро
```php
$fields = [
    'IBLOCK_ID' => 1,
    'NAME' => 'Новый элемент',
    'PROPERTY_VALUES' => [
        'PROPERTY_CODE' => 'Значение'
    ]
];
$element = new CIBlockElement;
$result = $element->Add($fields);
``` 