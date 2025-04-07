# User Module | Модуль Пользователи

## Overview | Обзор

The User module provides functionality for managing users, including authentication, authorization, and user profile management. | Модуль Пользователи предоставляет функциональность для управления пользователями, включая аутентификацию, авторизацию и управление профилями пользователей.

## Methods | Методы

### Users | Пользователи

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'user.get',
    [
        'filter' => ['ACTIVE' => true],
        'sort' => ['ID' => 'DESC'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$users = \Bitrix\Main\UserTable::getList([
    'select' => ['*', 'UF_*'],
    'filter' => ['=ACTIVE' => 'Y'],
    'order' => ['ID' => 'DESC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$users = CUser::GetList(
    ['ID' => 'DESC'],
    ['ACTIVE' => 'Y'],
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
    'user.add',
    [
        'fields' => [
            'EMAIL' => 'user@example.com',
            'LOGIN' => 'username',
            'PASSWORD' => 'password123',
            'NAME' => 'John',
            'LAST_NAME' => 'Doe',
            'SECOND_NAME' => 'Smith',
            'PERSONAL_GENDER' => 'M',
            'PERSONAL_PROFESSION' => 'Developer',
            'PERSONAL_WWW' => 'https://example.com',
            'PERSONAL_BIRTHDAY' => '1990-01-01',
            'PERSONAL_PHOTO' => '',
            'PERSONAL_ICQ' => '123456789',
            'PERSONAL_PHONE' => '+1234567890',
            'PERSONAL_FAX' => '',
            'PERSONAL_MOBILE' => '+1234567890',
            'PERSONAL_CITY' => 'New York',
            'WORK_POSITION' => 'Senior Developer',
            'WORK_COMPANY' => 'Acme Corp',
            'UF_DEPARTMENT' => [1, 2]
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$result = \Bitrix\Main\UserTable::add([
    'EMAIL' => 'user@example.com',
    'LOGIN' => 'username',
    'PASSWORD' => 'password123',
    'NAME' => 'John',
    'LAST_NAME' => 'Doe',
    'SECOND_NAME' => 'Smith',
    'PERSONAL_GENDER' => 'M',
    'PERSONAL_PROFESSION' => 'Developer',
    'PERSONAL_WWW' => 'https://example.com',
    'PERSONAL_BIRTHDAY' => '1990-01-01',
    'PERSONAL_ICQ' => '123456789',
    'PERSONAL_PHONE' => '+1234567890',
    'PERSONAL_MOBILE' => '+1234567890',
    'PERSONAL_CITY' => 'New York',
    'WORK_POSITION' => 'Senior Developer',
    'WORK_COMPANY' => 'Acme Corp',
    'UF_DEPARTMENT' => [1, 2]
]);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$userFields = [
    'EMAIL' => 'user@example.com',
    'LOGIN' => 'username',
    'PASSWORD' => 'password123',
    'NAME' => 'John',
    'LAST_NAME' => 'Doe',
    'SECOND_NAME' => 'Smith',
    'PERSONAL_GENDER' => 'M',
    'PERSONAL_PROFESSION' => 'Developer',
    'PERSONAL_WWW' => 'https://example.com',
    'PERSONAL_BIRTHDAY' => '1990-01-01',
    'PERSONAL_ICQ' => '123456789',
    'PERSONAL_PHONE' => '+1234567890',
    'PERSONAL_MOBILE' => '+1234567890',
    'PERSONAL_CITY' => 'New York',
    'WORK_POSITION' => 'Senior Developer',
    'WORK_COMPANY' => 'Acme Corp',
    'UF_DEPARTMENT' => [1, 2]
];
$user = new CUser();
$userId = $user->Add($userFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'user.update',
    [
        'ID' => 123,
        'fields' => [
            'NAME' => 'Johnny',
            'LAST_NAME' => 'Doe',
            'EMAIL' => 'johnny@example.com',
            'WORK_POSITION' => 'Lead Developer'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$result = \Bitrix\Main\UserTable::update(123, [
    'NAME' => 'Johnny',
    'LAST_NAME' => 'Doe',
    'EMAIL' => 'johnny@example.com',
    'WORK_POSITION' => 'Lead Developer'
]);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$userFields = [
    'NAME' => 'Johnny',
    'LAST_NAME' => 'Doe',
    'EMAIL' => 'johnny@example.com',
    'WORK_POSITION' => 'Lead Developer'
];
$user = new CUser();
$user->Update(123, $userFields);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'user.delete',
    ['ID' => 123]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$result = \Bitrix\Main\UserTable::delete(123);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$user = new CUser();
$user->Delete(123);
```

### User Groups | Группы пользователей

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'sonet_group.get',
    [
        'filter' => ['ACTIVE' => 'Y'],
        'sort' => ['ID' => 'DESC'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$groups = \Bitrix\Socialnetwork\WorkgroupTable::getList([
    'select' => ['*'],
    'filter' => ['=ACTIVE' => 'Y'],
    'order' => ['ID' => 'DESC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$groups = CSocNetGroup::GetList(
    ['ID' => 'DESC'],
    ['ACTIVE' => 'Y'],
    false,
    ['nTopCount' => 50],
    ['*']
);
```

#### Add | Добавление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'sonet_group.add',
    [
        'fields' => [
            'NAME' => 'New Group',
            'DESCRIPTION' => 'Group description',
            'VISIBLE' => 'Y',
            'OPENED' => 'Y',
            'SUBJECT_ID' => 1,
            'KEYWORDS' => 'keywords',
            'INITIATE_PERMS' => 'A',
            'SPAM_PERMS' => 'A',
            'OWNER_ID' => 1
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\WorkgroupTable::add([
    'NAME' => 'New Group',
    'DESCRIPTION' => 'Group description',
    'VISIBLE' => 'Y',
    'OPENED' => 'Y',
    'SUBJECT_ID' => 1,
    'KEYWORDS' => 'keywords',
    'INITIATE_PERMS' => 'A',
    'SPAM_PERMS' => 'A',
    'OWNER_ID' => 1
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$groupFields = [
    'NAME' => 'New Group',
    'DESCRIPTION' => 'Group description',
    'VISIBLE' => 'Y',
    'OPENED' => 'Y',
    'SUBJECT_ID' => 1,
    'KEYWORDS' => 'keywords',
    'INITIATE_PERMS' => 'A',
    'SPAM_PERMS' => 'A',
    'OWNER_ID' => 1
];
$group = new CSocNetGroup();
$groupId = $group->Add($groupFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'sonet_group.update',
    [
        'ID' => 123,
        'fields' => [
            'NAME' => 'Updated Group',
            'DESCRIPTION' => 'Updated description',
            'VISIBLE' => 'N'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\WorkgroupTable::update(123, [
    'NAME' => 'Updated Group',
    'DESCRIPTION' => 'Updated description',
    'VISIBLE' => 'N'
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$groupFields = [
    'NAME' => 'Updated Group',
    'DESCRIPTION' => 'Updated description',
    'VISIBLE' => 'N'
];
$group = new CSocNetGroup();
$group->Update(123, $groupFields);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'sonet_group.delete',
    ['ID' => 123]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\WorkgroupTable::delete(123);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$group = new CSocNetGroup();
$group->Delete(123);
```

### User Authentication | Аутентификация пользователей

#### Login | Вход

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$result = \Bitrix\Main\UserTable::getList([
    'select' => ['*'],
    'filter' => [
        '=LOGIN' => 'username',
        '=PASSWORD' => md5('password123')
    ],
    'limit' => 1
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$user = new CUser();
$result = $user->Login('username', 'password123');
```

#### Logout | Выход

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
\Bitrix\Main\UserTable::getList([
    'select' => ['*'],
    'filter' => ['=ID' => $userId],
    'limit' => 1
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$user = new CUser();
$user->Logout();
```

### User Permissions | Права пользователей

#### Get User Groups | Получение групп пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$userGroups = \Bitrix\Main\UserGroupTable::getList([
    'select' => ['GROUP_ID'],
    'filter' => ['=USER_ID' => $userId]
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$userGroups = CUser::GetUserGroup($userId);
```

#### Check Permission | Проверка прав

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$hasPermission = \Bitrix\Main\UserAccessTable::getList([
    'select' => ['ID'],
    'filter' => [
        '=USER_ID' => $userId,
        '=ACCESS_CODE' => 'G1'
    ],
    'limit' => 1
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$hasPermission = $USER->IsAdmin() || in_array(1, $USER->GetUserGroupArray());
``` 