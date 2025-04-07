# LDAP Module | Модуль LDAP

## Overview | Обзор

The LDAP module provides functionality for integrating Bitrix24 with external authentication systems and directories using the LDAP protocol. It allows for user synchronization, authentication, and directory services integration. | Модуль LDAP предоставляет функциональность для интеграции Bitrix24 с внешними системами аутентификации и каталогами с использованием протокола LDAP. Он позволяет выполнять синхронизацию пользователей, аутентификацию и интеграцию с сервисами каталогов.

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

## Handlers | Обработчики

### Connection Handlers | Обработчики соединения

#### Connection Handler | Обработчик соединения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
class CustomConnectionHandler extends \Bitrix\LDAP\Connection\Handler
{
    public function onBeforeConnect($params)
    {
        // Code executed before LDAP connection is established
        // Код, выполняемый перед установкой соединения LDAP
        return $params;
    }
    
    public function onAfterConnect($params, $result)
    {
        // Code executed after LDAP connection is established
        // Код, выполняемый после установки соединения LDAP
        return $result;
    }
    
    public function onBeforeDisconnect($params)
    {
        // Code executed before LDAP connection is closed
        // Код, выполняемый перед закрытием соединения LDAP
        return $params;
    }
    
    public function onAfterDisconnect($params, $result)
    {
        // Code executed after LDAP connection is closed
        // Код, выполняемый после закрытия соединения LDAP
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\LDAP\Connection\Handler::register('custom_connection', CustomConnectionHandler::class);

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
class CCustomConnectionHandler extends CLDAPConnectionHandler
{
    public function OnBeforeConnect($params)
    {
        // Code executed before LDAP connection is established
        // Код, выполняемый перед установкой соединения LDAP
        return $params;
    }
    
    public function OnAfterConnect($params, $result)
    {
        // Code executed after LDAP connection is established
        // Код, выполняемый после установки соединения LDAP
        return $result;
    }
    
    public function OnBeforeDisconnect($params)
    {
        // Code executed before LDAP connection is closed
        // Код, выполняемый перед закрытием соединения LDAP
        return $params;
    }
    
    public function OnAfterDisconnect($params, $result)
    {
        // Code executed after LDAP connection is closed
        // Код, выполняемый после закрытия соединения LDAP
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CLDAPConnectionHandler::Register('custom_connection', 'CCustomConnectionHandler');
```

### User Handlers | Обработчики пользователей

#### User Handler | Обработчик пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
class CustomUserHandler extends \Bitrix\LDAP\User\Handler
{
    public function onBeforeUserSearch($params)
    {
        // Code executed before user search
        // Код, выполняемый перед поиском пользователя
        return $params;
    }
    
    public function onAfterUserSearch($params, $result)
    {
        // Code executed after user search
        // Код, выполняемый после поиска пользователя
        return $result;
    }
    
    public function onBeforeUserImport($params)
    {
        // Code executed before user import
        // Код, выполняемый перед импортом пользователя
        return $params;
    }
    
    public function onAfterUserImport($params, $result)
    {
        // Code executed after user import
        // Код, выполняемый после импорта пользователя
        return $result;
    }
    
    public function onBeforeUserUpdate($params)
    {
        // Code executed before user update
        // Код, выполняемый перед обновлением пользователя
        return $params;
    }
    
    public function onAfterUserUpdate($params, $result)
    {
        // Code executed after user update
        // Код, выполняемый после обновления пользователя
        return $result;
    }
    
    public function onBeforeUserDelete($params)
    {
        // Code executed before user delete
        // Код, выполняемый перед удалением пользователя
        return $params;
    }
    
    public function onAfterUserDelete($params, $result)
    {
        // Code executed after user delete
        // Код, выполняемый после удаления пользователя
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\LDAP\User\Handler::register('custom_user', CustomUserHandler::class);

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
class CCustomUserHandler extends CLDAPUserHandler
{
    public function OnBeforeUserSearch($params)
    {
        // Code executed before user search
        // Код, выполняемый перед поиском пользователя
        return $params;
    }
    
    public function OnAfterUserSearch($params, $result)
    {
        // Code executed after user search
        // Код, выполняемый после поиска пользователя
        return $result;
    }
    
    public function OnBeforeUserImport($params)
    {
        // Code executed before user import
        // Код, выполняемый перед импортом пользователя
        return $params;
    }
    
    public function OnAfterUserImport($params, $result)
    {
        // Code executed after user import
        // Код, выполняемый после импорта пользователя
        return $result;
    }
    
    public function OnBeforeUserUpdate($params)
    {
        // Code executed before user update
        // Код, выполняемый перед обновлением пользователя
        return $params;
    }
    
    public function OnAfterUserUpdate($params, $result)
    {
        // Code executed after user update
        // Код, выполняемый после обновления пользователя
        return $result;
    }
    
    public function OnBeforeUserDelete($params)
    {
        // Code executed before user delete
        // Код, выполняемый перед удалением пользователя
        return $params;
    }
    
    public function OnAfterUserDelete($params, $result)
    {
        // Code executed after user delete
        // Код, выполняемый после удаления пользователя
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CLDAPUserHandler::Register('custom_user', 'CCustomUserHandler');
```

### Group Handlers | Обработчики групп

#### Group Handler | Обработчик группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
class CustomGroupHandler extends \Bitrix\LDAP\Group\Handler
{
    public function onBeforeGroupSearch($params)
    {
        // Code executed before group search
        // Код, выполняемый перед поиском группы
        return $params;
    }
    
    public function onAfterGroupSearch($params, $result)
    {
        // Code executed after group search
        // Код, выполняемый после поиска группы
        return $result;
    }
    
    public function onBeforeGroupImport($params)
    {
        // Code executed before group import
        // Код, выполняемый перед импортом группы
        return $params;
    }
    
    public function onAfterGroupImport($params, $result)
    {
        // Code executed after group import
        // Код, выполняемый после импорта группы
        return $result;
    }
    
    public function onBeforeGroupUpdate($params)
    {
        // Code executed before group update
        // Код, выполняемый перед обновлением группы
        return $params;
    }
    
    public function onAfterGroupUpdate($params, $result)
    {
        // Code executed after group update
        // Код, выполняемый после обновления группы
        return $result;
    }
    
    public function onBeforeGroupDelete($params)
    {
        // Code executed before group delete
        // Код, выполняемый перед удалением группы
        return $params;
    }
    
    public function onAfterGroupDelete($params, $result)
    {
        // Code executed after group delete
        // Код, выполняемый после удаления группы
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\LDAP\Group\Handler::register('custom_group', CustomGroupHandler::class);

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
class CCustomGroupHandler extends CLDAPGroupHandler
{
    public function OnBeforeGroupSearch($params)
    {
        // Code executed before group search
        // Код, выполняемый перед поиском группы
        return $params;
    }
    
    public function OnAfterGroupSearch($params, $result)
    {
        // Code executed after group search
        // Код, выполняемый после поиска группы
        return $result;
    }
    
    public function OnBeforeGroupImport($params)
    {
        // Code executed before group import
        // Код, выполняемый перед импортом группы
        return $params;
    }
    
    public function OnAfterGroupImport($params, $result)
    {
        // Code executed after group import
        // Код, выполняемый после импорта группы
        return $result;
    }
    
    public function OnBeforeGroupUpdate($params)
    {
        // Code executed before group update
        // Код, выполняемый перед обновлением группы
        return $params;
    }
    
    public function OnAfterGroupUpdate($params, $result)
    {
        // Code executed after group update
        // Код, выполняемый после обновления группы
        return $result;
    }
    
    public function OnBeforeGroupDelete($params)
    {
        // Code executed before group delete
        // Код, выполняемый перед удалением группы
        return $params;
    }
    
    public function OnAfterGroupDelete($params, $result)
    {
        // Code executed after group delete
        // Код, выполняемый после удаления группы
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CLDAPGroupHandler::Register('custom_group', 'CCustomGroupHandler');
```

### Synchronization Handlers | Обработчики синхронизации

#### Synchronization Handler | Обработчик синхронизации

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
class CustomSynchronizationHandler extends \Bitrix\LDAP\Synchronization\Handler
{
    public function onBeforeSynchronizationStart($params)
    {
        // Code executed before synchronization starts
        // Код, выполняемый перед началом синхронизации
        return $params;
    }
    
    public function onAfterSynchronizationStart($params, $result)
    {
        // Code executed after synchronization starts
        // Код, выполняемый после начала синхронизации
        return $result;
    }
    
    public function onBeforeSynchronizationEnd($params)
    {
        // Code executed before synchronization ends
        // Код, выполняемый перед завершением синхронизации
        return $params;
    }
    
    public function onAfterSynchronizationEnd($params, $result)
    {
        // Code executed after synchronization ends
        // Код, выполняемый после завершения синхронизации
        return $result;
    }
    
    public function onSynchronizationError($params)
    {
        // Code executed when synchronization error occurs
        // Код, выполняемый при возникновении ошибки синхронизации
        return $params;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\LDAP\Synchronization\Handler::register('custom_synchronization', CustomSynchronizationHandler::class);

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
class CCustomSynchronizationHandler extends CLDAPSynchronizationHandler
{
    public function OnBeforeSynchronizationStart($params)
    {
        // Code executed before synchronization starts
        // Код, выполняемый перед началом синхронизации
        return $params;
    }
    
    public function OnAfterSynchronizationStart($params, $result)
    {
        // Code executed after synchronization starts
        // Код, выполняемый после начала синхронизации
        return $result;
    }
    
    public function OnBeforeSynchronizationEnd($params)
    {
        // Code executed before synchronization ends
        // Код, выполняемый перед завершением синхронизации
        return $params;
    }
    
    public function OnAfterSynchronizationEnd($params, $result)
    {
        // Code executed after synchronization ends
        // Код, выполняемый после завершения синхронизации
        return $result;
    }
    
    public function OnSynchronizationError($params)
    {
        // Code executed when synchronization error occurs
        // Код, выполняемый при возникновении ошибки синхронизации
        return $params;
    }
}

// Register handler
// Регистрация обработчика
CLDAPSynchronizationHandler::Register('custom_synchronization', 'CCustomSynchronizationHandler');
```

### Authentication Handlers | Обработчики аутентификации

#### Authentication Handler | Обработчик аутентификации

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('ldap')
// Требуется: Bitrix\Main\Loader::includeModule('ldap')
class CustomAuthenticationHandler extends \Bitrix\LDAP\Authentication\Handler
{
    public function onBeforeAuthentication($params)
    {
        // Code executed before authentication
        // Код, выполняемый перед аутентификацией
        return $params;
    }
    
    public function onAfterAuthentication($params, $result)
    {
        // Code executed after authentication
        // Код, выполняемый после аутентификации
        return $result;
    }
    
    public function onAuthenticationError($params)
    {
        // Code executed when authentication error occurs
        // Код, выполняемый при возникновении ошибки аутентификации
        return $params;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\LDAP\Authentication\Handler::register('custom_authentication', CustomAuthenticationHandler::class);

// Legacy
// Requires: CModule::IncludeModule('ldap')
// Требуется: CModule::IncludeModule('ldap')
class CCustomAuthenticationHandler extends CLDAPAuthenticationHandler
{
    public function OnBeforeAuthentication($params)
    {
        // Code executed before authentication
        // Код, выполняемый перед аутентификацией
        return $params;
    }
    
    public function OnAfterAuthentication($params, $result)
    {
        // Code executed after authentication
        // Код, выполняемый после аутентификации
        return $result;
    }
    
    public function OnAuthenticationError($params)
    {
        // Code executed when authentication error occurs
        // Код, выполняемый при возникновении ошибки аутентификации
        return $params;
    }
}

// Register handler
// Регистрация обработчика
CLDAPAuthenticationHandler::Register('custom_authentication', 'CCustomAuthenticationHandler');
``` 