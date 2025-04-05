# CRM Leads / Лиды CRM

[English](#english) | [Русский](#russian)

## English

### Get List / Получение списка

#### REST API
```php
$leads = CRest::call('crm.lead.list', [
    'filter' => ['ASSIGNED_BY_ID' => 1],
    'select' => ['ID', 'TITLE', 'NAME', 'LAST_NAME', 'STATUS_ID']
]);
```

#### D7
```php
use Bitrix\Crm\LeadTable;

$leads = LeadTable::getList([
    'select' => ['ID', 'TITLE', 'NAME', 'LAST_NAME', 'STATUS_ID'],
    'filter' => ['=ASSIGNED_BY_ID' => 1]
])->fetchAll();
```

#### Legacy
```php
$filter = ['ASSIGNED_BY_ID' => 1];
$select = ['ID', 'TITLE', 'NAME', 'LAST_NAME', 'STATUS_ID'];
$leads = CCrmLead::GetList(
    ['ID' => 'ASC'],
    $filter,
    $select
);
```

### Add / Добавление

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

### Update / Обновление

#### REST API
```php
$result = CRest::call('crm.lead.update', [
    'id' => 1,
    'fields' => [
        'TITLE' => 'Updated Lead',
        'STATUS_ID' => 'IN_PROCESS'
    ]
]);
```

#### D7
```php
use Bitrix\Crm\LeadTable;

$result = LeadTable::update(1, [
    'TITLE' => 'Updated Lead',
    'STATUS_ID' => 'IN_PROCESS'
]);
```

#### Legacy
```php
$fields = [
    'TITLE' => 'Updated Lead',
    'STATUS_ID' => 'IN_PROCESS'
];
$lead = new CCrmLead(false);
$result = $lead->Update(1, $fields);
```

### Delete / Удаление

#### REST API
```php
$result = CRest::call('crm.lead.delete', [
    'id' => 1
]);
```

#### D7
```php
use Bitrix\Crm\LeadTable;

$result = LeadTable::delete(1);
```

#### Legacy
```php
$lead = new CCrmLead(false);
$result = $lead->Delete(1);
```

### Convert to Deal / Конвертация в сделку

#### REST API
```php
$result = CRest::call('crm.lead.convert', [
    'id' => 1,
    'fields' => [
        'ASSIGNED_BY_ID' => 1,
        'STAGE_ID' => 'NEW'
    ]
]);
```

#### D7
```php
use Bitrix\Crm\LeadTable;
use Bitrix\Crm\Conversion\LeadConversionConfig;

$lead = LeadTable::getList([
    'filter' => ['=ID' => 1]
])->fetch();

$config = new LeadConversionConfig();
$config->setEntityID($lead['ID']);
$config->setEntityTypeID(\CCrmOwnerType::Lead);
$config->setEntityFields($lead);
$config->setEntityInfos([
    \CCrmOwnerType::DealName => [
        'ASSIGNED_BY_ID' => 1,
        'STAGE_ID' => 'NEW'
    ]
]);

$converter = new \Bitrix\Crm\Conversion\LeadConverter($config);
$result = $converter->convert();
```

#### Legacy
```php
$lead = new CCrmLead(false);
$lead->Load(1);

$converter = new CCrmLeadConverter($lead);
$result = $converter->Convert([
    'ASSIGNED_BY_ID' => 1,
    'STAGE_ID' => 'NEW'
]);
```

## Русский

### Получение списка

#### REST API
```php
$leads = CRest::call('crm.lead.list', [
    'filter' => ['ASSIGNED_BY_ID' => 1],
    'select' => ['ID', 'TITLE', 'NAME', 'LAST_NAME', 'STATUS_ID']
]);
```

#### D7
```php
use Bitrix\Crm\LeadTable;

$leads = LeadTable::getList([
    'select' => ['ID', 'TITLE', 'NAME', 'LAST_NAME', 'STATUS_ID'],
    'filter' => ['=ASSIGNED_BY_ID' => 1]
])->fetchAll();
```

#### Старое ядро
```php
$filter = ['ASSIGNED_BY_ID' => 1];
$select = ['ID', 'TITLE', 'NAME', 'LAST_NAME', 'STATUS_ID'];
$leads = CCrmLead::GetList(
    ['ID' => 'ASC'],
    $filter,
    $select
);
```

### Добавление

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

### Обновление

#### REST API
```php
$result = CRest::call('crm.lead.update', [
    'id' => 1,
    'fields' => [
        'TITLE' => 'Обновленный лид',
        'STATUS_ID' => 'IN_PROCESS'
    ]
]);
```

#### D7
```php
use Bitrix\Crm\LeadTable;

$result = LeadTable::update(1, [
    'TITLE' => 'Обновленный лид',
    'STATUS_ID' => 'IN_PROCESS'
]);
```

#### Старое ядро
```php
$fields = [
    'TITLE' => 'Обновленный лид',
    'STATUS_ID' => 'IN_PROCESS'
];
$lead = new CCrmLead(false);
$result = $lead->Update(1, $fields);
```

### Удаление

#### REST API
```php
$result = CRest::call('crm.lead.delete', [
    'id' => 1
]);
```

#### D7
```php
use Bitrix\Crm\LeadTable;

$result = LeadTable::delete(1);
```

#### Старое ядро
```php
$lead = new CCrmLead(false);
$result = $lead->Delete(1);
```

### Конвертация в сделку

#### REST API
```php
$result = CRest::call('crm.lead.convert', [
    'id' => 1,
    'fields' => [
        'ASSIGNED_BY_ID' => 1,
        'STAGE_ID' => 'NEW'
    ]
]);
```

#### D7
```php
use Bitrix\Crm\LeadTable;
use Bitrix\Crm\Conversion\LeadConversionConfig;

$lead = LeadTable::getList([
    'filter' => ['=ID' => 1]
])->fetch();

$config = new LeadConversionConfig();
$config->setEntityID($lead['ID']);
$config->setEntityTypeID(\CCrmOwnerType::Lead);
$config->setEntityFields($lead);
$config->setEntityInfos([
    \CCrmOwnerType::DealName => [
        'ASSIGNED_BY_ID' => 1,
        'STAGE_ID' => 'NEW'
    ]
]);

$converter = new \Bitrix\Crm\Conversion\LeadConverter($config);
$result = $converter->convert();
```

#### Старое ядро
```php
$lead = new CCrmLead(false);
$lead->Load(1);

$converter = new CCrmLeadConverter($lead);
$result = $converter->Convert([
    'ASSIGNED_BY_ID' => 1,
    'STAGE_ID' => 'NEW'
]);
``` 