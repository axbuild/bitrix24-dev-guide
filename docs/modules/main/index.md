# Main Module | Модуль Главный

[English](#english) | [Русский](#russian)

## English

### Overview | Обзор

The Main module provides core functionality for Bitrix24, including system settings, user authentication, file management, and database operations. | Модуль Главный предоставляет основную функциональность для Bitrix24, включая системные настройки, аутентификацию пользователей, управление файлами и операции с базой данных.

### Available Entities

- [Users](users.md)
- [Groups](groups.md)
- [Departments](departments.md)
- [Files](files.md)
- [Settings](settings.md)

## Русский

### Обзор

Основной модуль является ядром Bitrix24 и предоставляет базовую функциональность для всей системы.

### Доступные сущности

- [Пользователи](users.md)
- [Группы](groups.md)
- [Подразделения](departments.md)
- [Файлы](files.md)
- [Настройки](settings.md)

## Methods | Методы

### System Settings | Системные настройки

#### Get Option | Получение опции

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$optionValue = \Bitrix\Main\Config\Option::get('main', 'option_name', 'default_value');

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$optionValue = COption::GetOptionString('main', 'option_name', 'default_value');
```

#### Set Option | Установка опции

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
\Bitrix\Main\Config\Option::set('main', 'option_name', 'option_value');

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
COption::SetOptionString('main', 'option_name', 'option_value');
```

#### Delete Option | Удаление опции

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
\Bitrix\Main\Config\Option::delete('main', ['option_name']);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
COption::RemoveOption('main', 'option_name');
```

### User Authentication | Аутентификация пользователей

#### Login | Вход в систему

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$result = \Bitrix\Main\UserTable::getList([
    'filter' => [
        '=LOGIN' => 'user_login',
        '=PASSWORD' => md5('user_password')
    ]
])->fetch();

if ($result) {
    $user = new \CUser();
    $user->Authorize($result['ID']);
}

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$user = new CUser();
$result = $user->Login('user_login', 'user_password');
```

#### Logout | Выход из системы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$user = new \CUser();
$user->Logout();

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$user = new CUser();
$user->Logout();
```

#### Check Authorization | Проверка авторизации

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$user = new \CUser();
$isAuthorized = $user->IsAuthorized();

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$user = new CUser();
$isAuthorized = $user->IsAuthorized();
```

### File Management | Управление файлами

#### Upload File | Загрузка файла

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$fileArray = \CFile::MakeFileArray($_SERVER['DOCUMENT_ROOT'] . '/upload/temp/file.jpg');
$fileId = \CFile::SaveFile($fileArray, 'main');

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$fileArray = CFile::MakeFileArray($_SERVER['DOCUMENT_ROOT'] . '/upload/temp/file.jpg');
$fileId = CFile::SaveFile($fileArray, 'main');
```

#### Get File | Получение файла

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$fileArray = \CFile::GetFileArray($fileId);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$fileArray = CFile::GetFileArray($fileId);
```

#### Delete File | Удаление файла

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
\CFile::Delete($fileId);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
CFile::Delete($fileId);
```

### Database Operations | Операции с базой данных

#### Execute Query | Выполнение запроса

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$connection = \Bitrix\Main\Application::getConnection();
$result = $connection->query('SELECT * FROM b_user WHERE ID = 1');

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$result = $DB->Query('SELECT * FROM b_user WHERE ID = 1');
```

#### Execute Query with Parameters | Выполнение запроса с параметрами

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$connection = \Bitrix\Main\Application::getConnection();
$sql = "SELECT * FROM b_user WHERE ID = :id AND ACTIVE = :active";
$result = $connection->query($sql, ['id' => 1, 'active' => 'Y']);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$sql = "SELECT * FROM b_user WHERE ID = " . intval($id) . " AND ACTIVE = 'Y'";
$result = $DB->Query($sql);
```

#### Execute Transaction | Выполнение транзакции

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$connection = \Bitrix\Main\Application::getConnection();
$connection->startTransaction();
try {
    $connection->query('INSERT INTO b_user (LOGIN, PASSWORD) VALUES ("user1", "pass1")');
    $connection->query('INSERT INTO b_user (LOGIN, PASSWORD) VALUES ("user2", "pass2")');
    $connection->commitTransaction();
} catch (\Exception $e) {
    $connection->rollbackTransaction();
}

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$DB->StartTransaction();
$DB->Query('INSERT INTO b_user (LOGIN, PASSWORD) VALUES ("user1", "pass1")');
$DB->Query('INSERT INTO b_user (LOGIN, PASSWORD) VALUES ("user2", "pass2")');
$DB->Commit();
```

### Event Management | Управление событиями

#### Register Event Handler | Регистрация обработчика события

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
\Bitrix\Main\EventManager::getInstance()->addEventHandler(
    'main',
    'OnBeforeUserAdd',
    'MyEventHandler',
    '/local/php_interface/include/events.php'
);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
AddEventHandler('main', 'OnBeforeUserAdd', 'MyEventHandler');
```

#### Unregister Event Handler | Отмена регистрации обработчика события

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
\Bitrix\Main\EventManager::getInstance()->removeEventHandler(
    'main',
    'OnBeforeUserAdd',
    'MyEventHandler'
);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
RemoveEventHandler('main', 'OnBeforeUserAdd', 'MyEventHandler');
```

#### Send Event | Отправка события

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('main')
// Требуется: Bitrix\Main\Loader::includeModule('main')
$event = new \Bitrix\Main\Event('main', 'OnBeforeUserAdd', ['fields' => $userFields]);
$event->send();

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$event = new CEvent();
$event->Send('main', 'OnBeforeUserAdd', ['fields' => $userFields]);
``` 