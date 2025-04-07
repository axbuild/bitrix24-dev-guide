# CRM Module | Модуль CRM

## Overview | Обзор

The CRM module provides functionality for managing customer relationships, including leads, deals, contacts, and companies. | Модуль CRM предоставляет функциональность для управления взаимоотношениями с клиентами, включая лиды, сделки, контакты и компании.

## Methods | Методы

### Leads | Лиды

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.lead.list',
    [
        'select' => ['*', 'UF_*'],
        'filter' => ['>OPPORTUNITY' => 1000],
        'order' => ['ID' => 'DESC'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$leads = \Bitrix\Crm\LeadTable::getList([
    'select' => ['*', 'UF_*'],
    'filter' => ['>OPPORTUNITY' => 1000],
    'order' => ['ID' => 'DESC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$leads = CCrmLead::GetList(
    ['ID' => 'DESC'],
    ['>OPPORTUNITY' => 1000],
    true,
    ['nTopCount' => 50],
    ['*', 'UF_*']
);
```

#### Add | Добавление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.lead.add',
    [
        'fields' => [
            'TITLE' => 'New Lead',
            'NAME' => 'John',
            'LAST_NAME' => 'Doe',
            'OPPORTUNITY' => 5000,
            'CURRENCY_ID' => 'USD',
            'ASSIGNED_BY_ID' => 1
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$result = \Bitrix\Crm\Lead::add([
    'TITLE' => 'New Lead',
    'NAME' => 'John',
    'LAST_NAME' => 'Doe',
    'OPPORTUNITY' => 5000,
    'CURRENCY_ID' => 'USD',
    'ASSIGNED_BY_ID' => 1
]);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$leadFields = [
    'TITLE' => 'New Lead',
    'NAME' => 'John',
    'LAST_NAME' => 'Doe',
    'OPPORTUNITY' => 5000,
    'CURRENCY_ID' => 'USD',
    'ASSIGNED_BY_ID' => 1
];
$lead = new CCrmLead();
$leadId = $lead->Add($leadFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.lead.update',
    [
        'id' => 123,
        'fields' => [
            'OPPORTUNITY' => 6000,
            'STATUS_ID' => 'CONVERTED'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$result = \Bitrix\Crm\Lead::update(123, [
    'OPPORTUNITY' => 6000,
    'STATUS_ID' => 'CONVERTED'
]);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$leadFields = [
    'OPPORTUNITY' => 6000,
    'STATUS_ID' => 'CONVERTED'
];
$lead = new CCrmLead();
$lead->Update(123, $leadFields);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.lead.delete',
    ['id' => 123]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$result = \Bitrix\Crm\Lead::delete(123);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$lead = new CCrmLead();
$lead->Delete(123);
```

### Deals | Сделки

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.deal.list',
    [
        'select' => ['*', 'UF_*'],
        'filter' => ['>OPPORTUNITY' => 1000],
        'order' => ['ID' => 'DESC'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$deals = \Bitrix\Crm\DealTable::getList([
    'select' => ['*', 'UF_*'],
    'filter' => ['>OPPORTUNITY' => 1000],
    'order' => ['ID' => 'DESC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$deals = CCrmDeal::GetList(
    ['ID' => 'DESC'],
    ['>OPPORTUNITY' => 1000],
    true,
    ['nTopCount' => 50],
    ['*', 'UF_*']
);
```

#### Add | Добавление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.deal.add',
    [
        'fields' => [
            'TITLE' => 'New Deal',
            'OPPORTUNITY' => 5000,
            'CURRENCY_ID' => 'USD',
            'ASSIGNED_BY_ID' => 1,
            'STAGE_ID' => 'NEW'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$result = \Bitrix\Crm\Deal::add([
    'TITLE' => 'New Deal',
    'OPPORTUNITY' => 5000,
    'CURRENCY_ID' => 'USD',
    'ASSIGNED_BY_ID' => 1,
    'STAGE_ID' => 'NEW'
]);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$dealFields = [
    'TITLE' => 'New Deal',
    'OPPORTUNITY' => 5000,
    'CURRENCY_ID' => 'USD',
    'ASSIGNED_BY_ID' => 1,
    'STAGE_ID' => 'NEW'
];
$deal = new CCrmDeal();
$dealId = $deal->Add($dealFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.deal.update',
    [
        'id' => 123,
        'fields' => [
            'OPPORTUNITY' => 6000,
            'STAGE_ID' => 'WON'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$result = \Bitrix\Crm\Deal::update(123, [
    'OPPORTUNITY' => 6000,
    'STAGE_ID' => 'WON'
]);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$dealFields = [
    'OPPORTUNITY' => 6000,
    'STAGE_ID' => 'WON'
];
$deal = new CCrmDeal();
$deal->Update(123, $dealFields);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.deal.delete',
    ['id' => 123]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$result = \Bitrix\Crm\Deal::delete(123);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$deal = new CCrmDeal();
$deal->Delete(123);
```

### Contacts | Контакты

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.contact.list',
    [
        'select' => ['*', 'UF_*'],
        'filter' => ['TYPE_ID' => 'EMPLOYEE'],
        'order' => ['ID' => 'DESC'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$contacts = \Bitrix\Crm\ContactTable::getList([
    'select' => ['*', 'UF_*'],
    'filter' => ['TYPE_ID' => 'EMPLOYEE'],
    'order' => ['ID' => 'DESC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$contacts = CCrmContact::GetList(
    ['ID' => 'DESC'],
    ['TYPE_ID' => 'EMPLOYEE'],
    true,
    ['nTopCount' => 50],
    ['*', 'UF_*']
);
```

#### Add | Добавление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.contact.add',
    [
        'fields' => [
            'NAME' => 'John',
            'LAST_NAME' => 'Doe',
            'EMAIL' => [['VALUE' => 'john@example.com', 'VALUE_TYPE' => 'WORK']],
            'PHONE' => [['VALUE' => '+1234567890', 'VALUE_TYPE' => 'WORK']]
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$result = \Bitrix\Crm\Contact::add([
    'NAME' => 'John',
    'LAST_NAME' => 'Doe',
    'EMAIL' => [['VALUE' => 'john@example.com', 'VALUE_TYPE' => 'WORK']],
    'PHONE' => [['VALUE' => '+1234567890', 'VALUE_TYPE' => 'WORK']]
]);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$contactFields = [
    'NAME' => 'John',
    'LAST_NAME' => 'Doe',
    'EMAIL' => [['VALUE' => 'john@example.com', 'VALUE_TYPE' => 'WORK']],
    'PHONE' => [['VALUE' => '+1234567890', 'VALUE_TYPE' => 'WORK']]
];
$contact = new CCrmContact();
$contactId = $contact->Add($contactFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.contact.update',
    [
        'id' => 123,
        'fields' => [
            'NAME' => 'Johnny',
            'EMAIL' => [['VALUE' => 'johnny@example.com', 'VALUE_TYPE' => 'WORK']]
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$result = \Bitrix\Crm\Contact::update(123, [
    'NAME' => 'Johnny',
    'EMAIL' => [['VALUE' => 'johnny@example.com', 'VALUE_TYPE' => 'WORK']]
]);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$contactFields = [
    'NAME' => 'Johnny',
    'EMAIL' => [['VALUE' => 'johnny@example.com', 'VALUE_TYPE' => 'WORK']]
];
$contact = new CCrmContact();
$contact->Update(123, $contactFields);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.contact.delete',
    ['id' => 123]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$result = \Bitrix\Crm\Contact::delete(123);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$contact = new CCrmContact();
$contact->Delete(123);
```

### Companies | Компании

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.company.list',
    [
        'select' => ['*', 'UF_*'],
        'filter' => ['COMPANY_TYPE' => 'CUSTOMER'],
        'order' => ['ID' => 'DESC'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$companies = \Bitrix\Crm\CompanyTable::getList([
    'select' => ['*', 'UF_*'],
    'filter' => ['COMPANY_TYPE' => 'CUSTOMER'],
    'order' => ['ID' => 'DESC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$companies = CCrmCompany::GetList(
    ['ID' => 'DESC'],
    ['COMPANY_TYPE' => 'CUSTOMER'],
    true,
    ['nTopCount' => 50],
    ['*', 'UF_*']
);
```

#### Add | Добавление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.company.add',
    [
        'fields' => [
            'TITLE' => 'Acme Corp',
            'COMPANY_TYPE' => 'CUSTOMER',
            'INDUSTRY' => 'IT',
            'EMAIL' => [['VALUE' => 'info@acme.com', 'VALUE_TYPE' => 'WORK']],
            'PHONE' => [['VALUE' => '+1234567890', 'VALUE_TYPE' => 'WORK']]
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$result = \Bitrix\Crm\Company::add([
    'TITLE' => 'Acme Corp',
    'COMPANY_TYPE' => 'CUSTOMER',
    'INDUSTRY' => 'IT',
    'EMAIL' => [['VALUE' => 'info@acme.com', 'VALUE_TYPE' => 'WORK']],
    'PHONE' => [['VALUE' => '+1234567890', 'VALUE_TYPE' => 'WORK']]
]);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$companyFields = [
    'TITLE' => 'Acme Corp',
    'COMPANY_TYPE' => 'CUSTOMER',
    'INDUSTRY' => 'IT',
    'EMAIL' => [['VALUE' => 'info@acme.com', 'VALUE_TYPE' => 'WORK']],
    'PHONE' => [['VALUE' => '+1234567890', 'VALUE_TYPE' => 'WORK']]
];
$company = new CCrmCompany();
$companyId = $company->Add($companyFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.company.update',
    [
        'id' => 123,
        'fields' => [
            'TITLE' => 'Acme Corporation',
            'INDUSTRY' => 'Technology'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$result = \Bitrix\Crm\Company::update(123, [
    'TITLE' => 'Acme Corporation',
    'INDUSTRY' => 'Technology'
]);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$companyFields = [
    'TITLE' => 'Acme Corporation',
    'INDUSTRY' => 'Technology'
];
$company = new CCrmCompany();
$company->Update(123, $companyFields);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.company.delete',
    ['id' => 123]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$result = \Bitrix\Crm\Company::delete(123);

// Legacy
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('crm')
$company = new CCrmCompany();
$company->Delete(123);
``` 