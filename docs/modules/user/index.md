# User Module | Модуль Пользователи

## Overview | Обзор

The User module provides functionality for managing users, their groups, and access rights in Bitrix24. It is a core module for user authentication, authorization, and profile management. | Модуль Пользователи предоставляет функциональность для управления пользователями, их группами и правами доступа в Bitrix24. Это основной модуль для аутентификации, авторизации и управления профилями пользователей.

## Methods | Методы

### Users | Пользователи

#### Get User | Получение пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$user = \Bitrix\Main\UserTable::getList([
    'filter' => ['=ID' => $userId],
    'select' => ['*']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$user = CUser::GetByID($userId)->Fetch();
```

#### Get User List | Получение списка пользователей

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$users = \Bitrix\Main\UserTable::getList([
    'filter' => ['=ACTIVE' => 'Y'],
    'select' => ['*'],
    'order' => ['NAME' => 'ASC'],
    'limit' => 10
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$users = CUser::GetList(
    ['NAME' => 'ASC'],
    ['ACTIVE' => 'Y'],
    ['*'],
    ['nTopCount' => 10]
);
```

#### Add User | Добавление пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\UserTable::add([
    'LOGIN' => 'newuser',
    'PASSWORD' => 'password123',
    'EMAIL' => 'newuser@example.com',
    'NAME' => 'New',
    'LAST_NAME' => 'User',
    'SECOND_NAME' => 'Middle',
    'PERSONAL_GENDER' => 'M',
    'PERSONAL_PROFESSION' => 'Developer',
    'PERSONAL_WWW' => 'https://example.com',
    'PERSONAL_BIRTHDAY' => '1990-01-01',
    'PERSONAL_PHOTO' => null,
    'PERSONAL_ICQ' => '123456789',
    'PERSONAL_PHONE' => '+1234567890',
    'PERSONAL_FAX' => '+1234567891',
    'PERSONAL_MOBILE' => '+1234567892',
    'PERSONAL_CITY' => 'Moscow',
    'WORK_POSITION' => 'Senior Developer',
    'WORK_COMPANY' => 'Example Company',
    'ACTIVE' => 'Y',
    'GROUP_ID' => [1, 2],
    'XML_ID' => 'NEW_USER_XML_ID'
]);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CUser::Add([
    'LOGIN' => 'newuser',
    'PASSWORD' => 'password123',
    'EMAIL' => 'newuser@example.com',
    'NAME' => 'New',
    'LAST_NAME' => 'User',
    'SECOND_NAME' => 'Middle',
    'PERSONAL_GENDER' => 'M',
    'PERSONAL_PROFESSION' => 'Developer',
    'PERSONAL_WWW' => 'https://example.com',
    'PERSONAL_BIRTHDAY' => '1990-01-01',
    'PERSONAL_PHOTO' => null,
    'PERSONAL_ICQ' => '123456789',
    'PERSONAL_PHONE' => '+1234567890',
    'PERSONAL_FAX' => '+1234567891',
    'PERSONAL_MOBILE' => '+1234567892',
    'PERSONAL_CITY' => 'Moscow',
    'WORK_POSITION' => 'Senior Developer',
    'WORK_COMPANY' => 'Example Company',
    'ACTIVE' => 'Y',
    'GROUP_ID' => [1, 2],
    'XML_ID' => 'NEW_USER_XML_ID'
]);
```

#### Update User | Обновление пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\UserTable::update($userId, [
    'NAME' => 'Updated',
    'LAST_NAME' => 'User',
    'EMAIL' => 'updated@example.com'
]);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CUser::Update($userId, [
    'NAME' => 'Updated',
    'LAST_NAME' => 'User',
    'EMAIL' => 'updated@example.com'
]);
```

#### Delete User | Удаление пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\UserTable::delete($userId);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CUser::Delete($userId);
```

#### Change Password | Изменение пароля

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\UserTable::update($userId, [
    'PASSWORD' => 'newpassword123'
]);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CUser::ChangePassword($userId, 'newpassword123');
```

#### Get User Groups | Получение групп пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$userGroups = \Bitrix\Main\UserGroupTable::getList([
    'filter' => ['=USER_ID' => $userId],
    'select' => ['*', 'GROUP.NAME']
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$userGroups = CUser::GetUserGroup($userId);
```

#### Add User to Group | Добавление пользователя в группу

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\UserGroupTable::add([
    'USER_ID' => $userId,
    'GROUP_ID' => $groupId
]);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CUser::SetUserGroup($userId, [$groupId]);
```

#### Remove User from Group | Удаление пользователя из группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\UserGroupTable::delete([
    'USER_ID' => $userId,
    'GROUP_ID' => $groupId
]);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$userGroups = CUser::GetUserGroup($userId);
$userGroups = array_diff($userGroups, [$groupId]);
$result = CUser::SetUserGroup($userId, $userGroups);
```

### User Groups | Группы пользователей

#### Get Group | Получение группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$group = \Bitrix\Main\GroupTable::getList([
    'filter' => ['=ID' => $groupId],
    'select' => ['*']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$group = CGroup::GetByID($groupId)->Fetch();
```

#### Get Group List | Получение списка групп

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$groups = \Bitrix\Main\GroupTable::getList([
    'filter' => ['=ACTIVE' => 'Y'],
    'select' => ['*'],
    'order' => ['NAME' => 'ASC']
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$groups = CGroup::GetList(
    ['NAME' => 'ASC'],
    ['ACTIVE' => 'Y']
);
```

#### Add Group | Добавление группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\GroupTable::add([
    'NAME' => 'New Group',
    'DESCRIPTION' => 'Group description',
    'STRING_ID' => 'new_group',
    'C_SORT' => 100,
    'ACTIVE' => 'Y',
    'XML_ID' => 'NEW_GROUP_XML_ID'
]);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CGroup::Add([
    'NAME' => 'New Group',
    'DESCRIPTION' => 'Group description',
    'STRING_ID' => 'new_group',
    'C_SORT' => 100,
    'ACTIVE' => 'Y',
    'XML_ID' => 'NEW_GROUP_XML_ID'
]);
```

#### Update Group | Обновление группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\GroupTable::update($groupId, [
    'NAME' => 'Updated Group',
    'DESCRIPTION' => 'Updated description'
]);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CGroup::Update($groupId, [
    'NAME' => 'Updated Group',
    'DESCRIPTION' => 'Updated description'
]);
```

#### Delete Group | Удаление группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\GroupTable::delete($groupId);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CGroup::Delete($groupId);
```

### User Fields | Пользовательские поля

#### Get User Field | Получение пользовательского поля

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$userField = \Bitrix\Main\UserFieldTable::getList([
    'filter' => ['=ID' => $userFieldId],
    'select' => ['*']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$userField = CUserField::GetByID($userFieldId);
```

#### Get User Field List | Получение списка пользовательских полей

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$userFields = \Bitrix\Main\UserFieldTable::getList([
    'filter' => ['=ENTITY_ID' => 'USER'],
    'select' => ['*'],
    'order' => ['SORT' => 'ASC']
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$userFields = CUserField::GetList(
    ['SORT' => 'ASC'],
    ['ENTITY_ID' => 'USER']
);
```

#### Add User Field | Добавление пользовательского поля

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\UserFieldTable::add([
    'ENTITY_ID' => 'USER',
    'FIELD_NAME' => 'UF_NEW_FIELD',
    'USER_TYPE_ID' => 'string',
    'SORT' => 100,
    'MULTIPLE' => 'N',
    'MANDATORY' => 'N',
    'SHOW_FILTER' => 'N',
    'SHOW_IN_LIST' => 'Y',
    'EDIT_IN_LIST' => 'Y',
    'IS_SEARCHABLE' => 'N',
    'SETTINGS' => [
        'SIZE' => 100,
        'ROWS' => 1,
        'REGEXP' => '',
        'MIN_LENGTH' => 0,
        'MAX_LENGTH' => 0,
        'DEFAULT_VALUE' => ''
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CUserField::Add([
    'ENTITY_ID' => 'USER',
    'FIELD_NAME' => 'UF_NEW_FIELD',
    'USER_TYPE_ID' => 'string',
    'SORT' => 100,
    'MULTIPLE' => 'N',
    'MANDATORY' => 'N',
    'SHOW_FILTER' => 'N',
    'SHOW_IN_LIST' => 'Y',
    'EDIT_IN_LIST' => 'Y',
    'IS_SEARCHABLE' => 'N',
    'SETTINGS' => [
        'SIZE' => 100,
        'ROWS' => 1,
        'REGEXP' => '',
        'MIN_LENGTH' => 0,
        'MAX_LENGTH' => 0,
        'DEFAULT_VALUE' => ''
    ]
]);
```

#### Update User Field | Обновление пользовательского поля

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\UserFieldTable::update($userFieldId, [
    'SORT' => 200,
    'MANDATORY' => 'Y'
]);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CUserField::Update($userFieldId, [
    'SORT' => 200,
    'MANDATORY' => 'Y'
]);
```

#### Delete User Field | Удаление пользовательского поля

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\UserFieldTable::delete($userFieldId);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CUserField::Delete($userFieldId);
```

### User Field Values | Значения пользовательских полей

#### Get User Field Value | Получение значения пользовательского поля

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$userFieldValue = \Bitrix\Main\UserFieldValueTable::getList([
    'filter' => [
        '=USER_FIELD_ID' => $userFieldId,
        '=ENTITY_ID' => $userId
    ],
    'select' => ['*']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$userFieldValue = CUserField::GetUserFieldValue(
    'USER',
    $userId,
    'UF_NEW_FIELD'
);
```

#### Get User Field Values | Получение значений пользовательских полей

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$userFieldValues = \Bitrix\Main\UserFieldValueTable::getList([
    'filter' => ['=ENTITY_ID' => $userId],
    'select' => ['*', 'FIELD.NAME']
])->fetchAll();

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$userFieldValues = CUserField::GetUserFieldValue(
    'USER',
    $userId,
    'UF_NEW_FIELD'
);
```

#### Set User Field Value | Установка значения пользовательского поля

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\UserFieldValueTable::add([
    'USER_FIELD_ID' => $userFieldId,
    'ENTITY_ID' => $userId,
    'VALUE' => 'Field value'
]);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CUserField::SetUserFieldValue(
    'USER',
    $userId,
    'UF_NEW_FIELD',
    'Field value'
);
```

#### Update User Field Value | Обновление значения пользовательского поля

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\UserFieldValueTable::update($userFieldValueId, [
    'VALUE' => 'Updated field value'
]);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CUserField::SetUserFieldValue(
    'USER',
    $userId,
    'UF_NEW_FIELD',
    'Updated field value'
);
```

#### Delete User Field Value | Удаление значения пользовательского поля

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\UserFieldValueTable::delete($userFieldValueId);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CUserField::SetUserFieldValue(
    'USER',
    $userId,
    'UF_NEW_FIELD',
    null
);
```

### Authentication | Аутентификация

#### Login | Вход в систему

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$result = \Bitrix\Main\UserTable::getList([
    'filter' => [
        '=LOGIN' => 'username',
        '=PASSWORD' => md5('password123')
    ],
    'select' => ['*']
])->fetch();

if ($result) {
    // User authenticated
    // Пользователь аутентифицирован
    $_SESSION['USER_ID'] = $result['ID'];
}

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CUser::Login('username', 'password123');
```

#### Logout | Выход из системы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
unset($_SESSION['USER_ID']);

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$result = CUser::Logout();
```

#### Get Current User | Получение текущего пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$currentUserId = \Bitrix\Main\Engine\CurrentUser::get()->getId();
$currentUser = \Bitrix\Main\UserTable::getList([
    'filter' => ['=ID' => $currentUserId],
    'select' => ['*']
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$currentUser = CUser::GetByID($USER->GetID())->Fetch();
```

#### Check User Access | Проверка доступа пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('user')
// Требуется: Bitrix\Main\Loader::includeModule('user')
$userAccess = \Bitrix\Main\Engine\CurrentUser::get()->getAccess();
$hasAccess = $userAccess->check('user', 'read');

// Legacy
// Requires: CModule::IncludeModule('user')
// Требуется: CModule::IncludeModule('user')
$hasAccess = $USER->IsAdmin() || $USER->CanDoOperation('user_read');
``` 