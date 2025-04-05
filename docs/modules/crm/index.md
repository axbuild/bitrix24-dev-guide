# CRM Module / Модуль CRM

[English](#english) | [Русский](#russian)

## English

### Overview

The CRM module provides functionality for managing customer relationships, including leads, deals, contacts, and companies.

### Available Entities

- [Leads](leads.md)
- [Deals](deals.md)
- [Contacts](contacts.md)
- [Companies](companies.md)
- [Products](products.md)
- [Quotes](quotes.md)
- [Invoices](invoices.md)

### Common Operations

#### Get List
```php
// REST API
$leads = CRest::call('crm.lead.list', [
    'filter' => ['ASSIGNED_BY_ID' => 1],
    'select' => ['ID', 'TITLE', 'NAME', 'STATUS_ID']
]);

// D7
use Bitrix\Crm\LeadTable;
$leads = LeadTable::getList([
    'select' => ['ID', 'TITLE', 'NAME', 'STATUS_ID'],
    'filter' => ['=ASSIGNED_BY_ID' => 1]
])->fetchAll();

// Legacy
$filter = ['ASSIGNED_BY_ID' => 1];
$select = ['ID', 'TITLE', 'NAME', 'STATUS_ID'];
$leads = CCrmLead::GetList(
    ['ID' => 'ASC'],
    $filter,
    $select
);
```

#### Add
```php
// REST API
$result = CRest::call('crm.lead.add', [
    'fields' => [
        'TITLE' => 'New Lead',
        'NAME' => 'John',
        'LAST_NAME' => 'Doe',
        'STATUS_ID' => 'NEW'
    ]
]);

// D7
use Bitrix\Crm\LeadTable;
$result = LeadTable::add([
    'TITLE' => 'New Lead',
    'NAME' => 'John',
    'LAST_NAME' => 'Doe',
    'STATUS_ID' => 'NEW'
]);

// Legacy
$fields = [
    'TITLE' => 'New Lead',
    'NAME' => 'John',
    'LAST_NAME' => 'Doe',
    'STATUS_ID' => 'NEW'
];
$lead = new CCrmLead(false);
$result = $lead->Add($fields);
```

#### Update
```php
// REST API
$result = CRest::call('crm.lead.update', [
    'id' => 1,
    'fields' => [
        'TITLE' => 'Updated Lead',
        'STATUS_ID' => 'IN_PROCESS'
    ]
]);

// D7
use Bitrix\Crm\LeadTable;
$result = LeadTable::update(1, [
    'TITLE' => 'Updated Lead',
    'STATUS_ID' => 'IN_PROCESS'
]);

// Legacy
$fields = [
    'TITLE' => 'Updated Lead',
    'STATUS_ID' => 'IN_PROCESS'
];
$lead = new CCrmLead(false);
$result = $lead->Update(1, $fields);
```

#### Delete
```php
// REST API
$result = CRest::call('crm.lead.delete', [
    'id' => 1
]);

// D7
use Bitrix\Crm\LeadTable;
$result = LeadTable::delete(1);

// Legacy
$lead = new CCrmLead(false);
$result = $lead->Delete(1);
```

## Русский

### Обзор

Модуль CRM предоставляет функциональность для управления отношениями с клиентами, включая лиды, сделки, контакты и компании.

### Доступные сущности

- [Лиды](leads.md)
- [Сделки](deals.md)
- [Контакты](contacts.md)
- [Компании](companies.md)
- [Товары](products.md)
- [Предложения](quotes.md)
- [Счета](invoices.md)

### Основные операции

#### Получение списка
```php
// REST API
$leads = CRest::call('crm.lead.list', [
    'filter' => ['ASSIGNED_BY_ID' => 1],
    'select' => ['ID', 'TITLE', 'NAME', 'STATUS_ID']
]);

// D7
use Bitrix\Crm\LeadTable;
$leads = LeadTable::getList([
    'select' => ['ID', 'TITLE', 'NAME', 'STATUS_ID'],
    'filter' => ['=ASSIGNED_BY_ID' => 1]
])->fetchAll();

// Старое ядро
$filter = ['ASSIGNED_BY_ID' => 1];
$select = ['ID', 'TITLE', 'NAME', 'STATUS_ID'];
$leads = CCrmLead::GetList(
    ['ID' => 'ASC'],
    $filter,
    $select
);
```

#### Добавление
```php
// REST API
$result = CRest::call('crm.lead.add', [
    'fields' => [
        'TITLE' => 'Новый лид',
        'NAME' => 'Иван',
        'LAST_NAME' => 'Иванов',
        'STATUS_ID' => 'NEW'
    ]
]);

// D7
use Bitrix\Crm\LeadTable;
$result = LeadTable::add([
    'TITLE' => 'Новый лид',
    'NAME' => 'Иван',
    'LAST_NAME' => 'Иванов',
    'STATUS_ID' => 'NEW'
]);

// Старое ядро
$fields = [
    'TITLE' => 'Новый лид',
    'NAME' => 'Иван',
    'LAST_NAME' => 'Иванов',
    'STATUS_ID' => 'NEW'
];
$lead = new CCrmLead(false);
$result = $lead->Add($fields);
```

#### Обновление
```php
// REST API
$result = CRest::call('crm.lead.update', [
    'id' => 1,
    'fields' => [
        'TITLE' => 'Обновленный лид',
        'STATUS_ID' => 'IN_PROCESS'
    ]
]);

// D7
use Bitrix\Crm\LeadTable;
$result = LeadTable::update(1, [
    'TITLE' => 'Обновленный лид',
    'STATUS_ID' => 'IN_PROCESS'
]);

// Старое ядро
$fields = [
    'TITLE' => 'Обновленный лид',
    'STATUS_ID' => 'IN_PROCESS'
];
$lead = new CCrmLead(false);
$result = $lead->Update(1, $fields);
```

#### Удаление
```php
// REST API
$result = CRest::call('crm.lead.delete', [
    'id' => 1
]);

// D7
use Bitrix\Crm\LeadTable;
$result = LeadTable::delete(1);

// Старое ядро
$lead = new CCrmLead(false);
$result = $lead->Delete(1);
``` 