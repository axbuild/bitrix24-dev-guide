# LDAP Module | Модуль LDAP

## Overview | Обзор

The LDAP module provides functionality for integration with external authentication systems and directories using the LDAP protocol. It allows for user synchronization, authentication, and directory services integration. | Модуль LDAP предоставляет функциональность для интеграции с внешними системами аутентификации и каталогами с использованием протокола LDAP. Он позволяет синхронизировать пользователей, выполнять аутентификацию и интегрировать сервисы каталогов.

## Methods | Методы

### Connection | Подключение

#### Initialize LDAP Connection | Инициализация LDAP подключения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
$ldapServer = new \Bitrix\Ldap\LdapServer([
    'SERVER' => 'ldap.example.com',
    'PORT' => 389,
    'BASE_DN' => 'dc=example,dc=com',
    'ADMIN_LOGIN' => 'admin',
    'ADMIN_PASSWORD' => 'password',
    'USE_TLS' => true
]);

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
$ldapServer = new CLDAPServer();
$ldapServer->Connect('ldap.example.com', 389, 'admin', 'password', 'dc=example,dc=com');
```

#### Test Connection | Проверка подключения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
$result = $ldapServer->testConnection();

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
$result = $ldapServer->TestConnection();
```

### User Operations | Операции с пользователями

#### Search Users | Поиск пользователей

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
$users = $ldapServer->searchUsers([
    'filter' => [
        'objectClass' => 'person',
        'cn' => '*John*'
    ],
    'attributes' => ['cn', 'mail', 'telephoneNumber']
]);

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
$users = $ldapServer->SearchUsers(
    '(objectClass=person)(cn=*John*)',
    ['cn', 'mail', 'telephoneNumber']
);
```

#### Get User Details | Получение деталей пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
$userDetails = $ldapServer->getUserDetails('cn=John Doe,dc=example,dc=com');

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
$userDetails = $ldapServer->GetUserDetails('cn=John Doe,dc=example,dc=com');
```

#### Authenticate User | Аутентификация пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
$result = $ldapServer->authenticateUser('username', 'password');

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
$result = $ldapServer->AuthenticateUser('username', 'password');
```

### Synchronization | Синхронизация

#### Start Synchronization | Запуск синхронизации

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
$sync = new \Bitrix\Ldap\Synchronization($ldapServer);
$result = $sync->start([
    'sync_users' => true,
    'sync_groups' => true,
    'create_users' => true,
    'update_users' => true
]);

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
$sync = new CLDAPSync($ldapServer);
$result = $sync->Start([
    'sync_users' => true,
    'sync_groups' => true,
    'create_users' => true,
    'update_users' => true
]);
```

#### Get Synchronization Status | Получение статуса синхронизации

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
$status = $sync->getStatus();

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
$status = $sync->GetStatus();
```

### Group Operations | Операции с группами

#### Search Groups | Поиск групп

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
$groups = $ldapServer->searchGroups([
    'filter' => [
        'objectClass' => 'groupOfNames',
        'cn' => '*Admin*'
    ],
    'attributes' => ['cn', 'member']
]);

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
$groups = $ldapServer->SearchGroups(
    '(objectClass=groupOfNames)(cn=*Admin*)',
    ['cn', 'member']
);
```

#### Get Group Members | Получение участников группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
$members = $ldapServer->getGroupMembers('cn=Administrators,dc=example,dc=com');

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
$members = $ldapServer->GetGroupMembers('cn=Administrators,dc=example,dc=com');
```

### Settings | Настройки

#### Get LDAP Settings | Получение настроек LDAP

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
$settings = \Bitrix\Ldap\Settings::getInstance()->getSettings();

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
$settings = CLDAPSettings::GetSettings();
```

#### Update LDAP Settings | Обновление настроек LDAP

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
$result = \Bitrix\Ldap\Settings::getInstance()->updateSettings([
    'SERVER' => 'new.ldap.example.com',
    'PORT' => 636,
    'USE_SSL' => true
]);

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
$result = CLDAPSettings::UpdateSettings([
    'SERVER' => 'new.ldap.example.com',
    'PORT' => 636,
    'USE_SSL' => true
]);
```

### Error Handling | Обработка ошибок

#### Get Last Error | Получение последней ошибки

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
$error = $ldapServer->getLastError();

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
$error = $ldapServer->GetLastError();
```

#### Check Connection Status | Проверка статуса подключения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
$isConnected = $ldapServer->isConnected();

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
$isConnected = $ldapServer->IsConnected();
``` 