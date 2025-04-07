# Pull Module | Модуль Pull

## Overview | Обзор

The Pull module provides functionality for real-time push notifications and updates in Bitrix24. It enables instant delivery of messages, events, and data updates to users through various channels including web browsers and mobile applications. | Модуль Pull предоставляет функциональность для отправки push-уведомлений и обновлений в реальном времени в Bitrix24. Он обеспечивает мгновенную доставку сообщений, событий и обновлений данных пользователям через различные каналы, включая веб-браузеры и мобильные приложения.

## Methods | Методы

### Configuration | Конфигурация

#### Initialize Pull | Инициализация Pull

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
\Bitrix\Pull\Config::getInstance()->init([
    'userId' => $USER->GetID(),
    'serverUrl' => 'https://pull.example.com',
    'serverKey' => 'your_server_key',
    'serverSecret' => 'your_server_secret'
]);

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
CPullOptions::Init();
```

#### Get Pull Settings | Получение настроек Pull

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
$settings = \Bitrix\Pull\Config::getInstance()->getSettings();

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
$settings = CPullOptions::GetSettings();
```

#### Update Pull Settings | Обновление настроек Pull

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
$result = \Bitrix\Pull\Config::getInstance()->updateSettings([
    'serverUrl' => 'https://new.pull.example.com',
    'serverKey' => 'new_server_key',
    'serverSecret' => 'new_server_secret'
]);

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
$result = CPullOptions::UpdateSettings([
    'serverUrl' => 'https://new.pull.example.com',
    'serverKey' => 'new_server_key',
    'serverSecret' => 'new_server_secret'
]);
```

### Channel Management | Управление каналами

#### Create Channel | Создание канала

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
$channel = \Bitrix\Pull\Channel::create([
    'userId' => $USER->GetID(),
    'type' => 'user',
    'expires' => 86400 // 24 hours
]);

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
$channel = CPullChannel::Create([
    'USER_ID' => $USER->GetID(),
    'TYPE' => 'user',
    'EXPIRES' => 86400 // 24 hours
]);
```

#### Get Channel | Получение канала

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
$channel = \Bitrix\Pull\Channel::get([
    'userId' => $USER->GetID(),
    'type' => 'user'
]);

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
$channel = CPullChannel::Get([
    'USER_ID' => $USER->GetID(),
    'TYPE' => 'user'
]);
```

#### Delete Channel | Удаление канала

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
$result = \Bitrix\Pull\Channel::delete([
    'userId' => $USER->GetID(),
    'type' => 'user'
]);

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
$result = CPullChannel::Delete([
    'USER_ID' => $USER->GetID(),
    'TYPE' => 'user'
]);
```

### Message Management | Управление сообщениями

#### Send Message | Отправка сообщения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
$result = \Bitrix\Pull\Message::send([
    'channel' => 'user_' . $USER->GetID(),
    'module_id' => 'main',
    'command' => 'notification',
    'params' => [
        'title' => 'New Message',
        'text' => 'You have a new message',
        'link' => '/messages/'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
$result = CPullWatch::AddToStack('user_' . $USER->GetID(), [
    'module_id' => 'main',
    'command' => 'notification',
    'params' => [
        'title' => 'New Message',
        'text' => 'You have a new message',
        'link' => '/messages/'
    ]
]);
```

#### Send Message to Multiple Users | Отправка сообщения нескольким пользователям

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
$result = \Bitrix\Pull\Message::sendToUsers(
    [1, 2, 3], // User IDs
    [
        'module_id' => 'main',
        'command' => 'notification',
        'params' => [
            'title' => 'Group Message',
            'text' => 'This is a group message',
            'link' => '/group/'
        ]
    ]
);

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
$result = CPullWatch::AddToStack('user_1,user_2,user_3', [
    'module_id' => 'main',
    'command' => 'notification',
    'params' => [
        'title' => 'Group Message',
        'text' => 'This is a group message',
        'link' => '/group/'
    ]
]);
```

#### Send Message to Group | Отправка сообщения группе

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
$result = \Bitrix\Pull\Message::sendToGroup(
    'group_1', // Group ID
    [
        'module_id' => 'main',
        'command' => 'notification',
        'params' => [
            'title' => 'Group Message',
            'text' => 'This is a group message',
            'link' => '/group/'
        ]
    ]
);

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
$result = CPullWatch::AddToStack('group_1', [
    'module_id' => 'main',
    'command' => 'notification',
    'params' => [
        'title' => 'Group Message',
        'text' => 'This is a group message',
        'link' => '/group/'
    ]
]);
```

### Subscription Management | Управление подписками

#### Subscribe to Channel | Подписка на канал

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
$result = \Bitrix\Pull\Watch::subscribe([
    'userId' => $USER->GetID(),
    'channel' => 'user_' . $USER->GetID(),
    'moduleId' => 'main'
]);

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
$result = CPullWatch::Add($USER->GetID(), 'user_' . $USER->GetID(), true);
```

#### Unsubscribe from Channel | Отписка от канала

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
$result = \Bitrix\Pull\Watch::unsubscribe([
    'userId' => $USER->GetID(),
    'channel' => 'user_' . $USER->GetID(),
    'moduleId' => 'main'
]);

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
$result = CPullWatch::Delete($USER->GetID(), 'user_' . $USER->GetID());
```

#### Get Subscriptions | Получение подписок

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
$subscriptions = \Bitrix\Pull\Watch::getSubscriptions([
    'userId' => $USER->GetID()
]);

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
$subscriptions = CPullWatch::GetList([
    'USER_ID' => $USER->GetID()
]);
```

### Event Management | Управление событиями

#### Register Event | Регистрация события

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
$result = \Bitrix\Pull\Event::register([
    'moduleId' => 'main',
    'event' => 'user_login',
    'params' => [
        'userId' => $USER->GetID(),
        'userName' => $USER->GetLogin()
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
$result = CPullEvent::Add([
    'MODULE_ID' => 'main',
    'EVENT' => 'user_login',
    'PARAMS' => [
        'USER_ID' => $USER->GetID(),
        'USER_NAME' => $USER->GetLogin()
    ]
]);
```

#### Get Events | Получение событий

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
$events = \Bitrix\Pull\Event::get([
    'channel' => 'user_' . $USER->GetID(),
    'lastId' => 0,
    'limit' => 50
]);

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
$events = CPullEvent::GetList([
    'CHANNEL_ID' => 'user_' . $USER->GetID(),
    'LAST_ID' => 0,
    'LIMIT' => 50
]);
```

#### Delete Events | Удаление событий

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
$result = \Bitrix\Pull\Event::delete([
    'channel' => 'user_' . $USER->GetID(),
    'lastId' => 100
]);

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
$result = CPullEvent::Delete([
    'CHANNEL_ID' => 'user_' . $USER->GetID(),
    'LAST_ID' => 100
]);
```

### Client Integration | Интеграция с клиентом

#### Get Client Script | Получение клиентского скрипта

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('pull')
// Требуется: Bitrix\Main\Loader::includeModule('pull')
$script = \Bitrix\Pull\Client::getScript([
    'userId' => $USER->GetID(),
    'serverUrl' => 'https://pull.example.com',
    'serverKey' => 'your_server_key'
]);

// Legacy
// Requires: CModule::IncludeModule('pull')
// Требуется: CModule::IncludeModule('pull')
$script = CPullWatch::GetScript([
    'USER_ID' => $USER->GetID(),
    'SERVER_URL' => 'https://pull.example.com',
    'SERVER_KEY' => 'your_server_key'
]);
```

#### Initialize Client | Инициализация клиента

```php
// JavaScript
// Requires: Pull client script
// Требуется: Скрипт клиента Pull
BX.Pull.init({
    userId: 1,
    serverUrl: 'https://pull.example.com',
    serverKey: 'your_server_key',
    onConnect: function() {
        console.log('Connected to Pull server');
    },
    onError: function(error) {
        console.error('Pull error:', error);
    }
});
```

#### Subscribe to Events | Подписка на события

```php
// JavaScript
// Requires: Pull client script
// Требуется: Скрипт клиента Pull
BX.Pull.subscribe({
    moduleId: 'main',
    callback: function(data) {
        console.log('Received event:', data);
    }
});
```

#### Unsubscribe from Events | Отписка от событий

```php
// JavaScript
// Requires: Pull client script
// Требуется: Скрипт клиента Pull
BX.Pull.unsubscribe({
    moduleId: 'main'
});
``` 