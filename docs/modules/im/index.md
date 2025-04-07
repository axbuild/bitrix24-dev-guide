# IM Module | Модуль IM

## Overview | Обзор

The IM module provides functionality for instant messaging in Bitrix24. It enables users to exchange messages, create group chats, share files, and integrate with other modules. | Модуль IM предоставляет функциональность для обмена мгновенными сообщениями в Bitrix24. Он позволяет пользователям обмениваться сообщениями, создавать групповые чаты, делиться файлами и интегрироваться с другими модулями.

## Methods | Методы

### Chat Management | Управление чатами

#### Create Chat | Создание чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$chat = \Bitrix\Im\Chat::add([
    'TITLE' => 'Project Discussion',
    'TYPE' => 'GROUP',
    'USERS' => [$userId1, $userId2, $userId3],
    'DESCRIPTION' => 'Chat for project team members',
    'COLOR' => '#FF0000',
    'AVATAR' => $avatarId
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$chat = CIMChat::Add([
    'TITLE' => 'Project Discussion',
    'TYPE' => 'GROUP',
    'USERS' => [$userId1, $userId2, $userId3],
    'DESCRIPTION' => 'Chat for project team members',
    'COLOR' => '#FF0000',
    'AVATAR' => $avatarId
]);
```

#### Get Chat | Получение чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$chat = \Bitrix\Im\Chat::getById($chatId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$chat = CIMChat::GetByID($chatId);
```

#### Get Chat List | Получение списка чатов

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$chats = \Bitrix\Im\Chat::getList([
    'select' => ['*'],
    'filter' => [
        'USER_ID' => $USER->GetID(),
        'TYPE' => 'GROUP'
    ],
    'order' => ['LAST_MESSAGE_DATE' => 'DESC']
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$chats = CIMChat::GetList([
    'USER_ID' => $USER->GetID(),
    'TYPE' => 'GROUP'
], ['LAST_MESSAGE_DATE' => 'DESC']);
```

#### Update Chat | Обновление чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$chat = \Bitrix\Im\Chat::getById($chatId);
$result = $chat->update([
    'TITLE' => 'Updated Project Discussion',
    'DESCRIPTION' => 'Updated chat for project team members',
    'COLOR' => '#00FF00'
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::Update($chatId, [
    'TITLE' => 'Updated Project Discussion',
    'DESCRIPTION' => 'Updated chat for project team members',
    'COLOR' => '#00FF00'
]);
```

#### Delete Chat | Удаление чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$chat = \Bitrix\Im\Chat::getById($chatId);
$result = $chat->delete();

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::Delete($chatId);
```

### Message Management | Управление сообщениями

#### Send Message | Отправка сообщения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$message = \Bitrix\Im\Message::add([
    'CHAT_ID' => $chatId,
    'FROM_USER_ID' => $USER->GetID(),
    'MESSAGE' => 'Hello, team!',
    'PARAMS' => [
        'KEYBOARD' => [
            [
                'BOT_ID' => $botId,
                'COMMAND' => 'start',
                'TITLE' => 'Start'
            ]
        ]
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$message = CIMChat::AddMessage([
    'CHAT_ID' => $chatId,
    'FROM_USER_ID' => $USER->GetID(),
    'MESSAGE' => 'Hello, team!',
    'PARAMS' => [
        'KEYBOARD' => [
            [
                'BOT_ID' => $botId,
                'COMMAND' => 'start',
                'TITLE' => 'Start'
            ]
        ]
    ]
]);
```

#### Get Message | Получение сообщения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$message = \Bitrix\Im\Message::getById($messageId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$message = CIMChat::GetMessage($messageId);
```

#### Get Message List | Получение списка сообщений

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$messages = \Bitrix\Im\Message::getList([
    'select' => ['*'],
    'filter' => [
        'CHAT_ID' => $chatId
    ],
    'order' => ['DATE_CREATE' => 'DESC'],
    'limit' => 50
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$messages = CIMChat::GetMessageList([
    'CHAT_ID' => $chatId
], ['DATE_CREATE' => 'DESC'], 50);
```

#### Update Message | Обновление сообщения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$message = \Bitrix\Im\Message::getById($messageId);
$result = $message->update([
    'MESSAGE' => 'Updated message text'
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::UpdateMessage($messageId, [
    'MESSAGE' => 'Updated message text'
]);
```

#### Delete Message | Удаление сообщения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$message = \Bitrix\Im\Message::getById($messageId);
$result = $message->delete();

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::DeleteMessage($messageId);
```

### User Management | Управление пользователями

#### Add User to Chat | Добавление пользователя в чат

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$chat = \Bitrix\Im\Chat::getById($chatId);
$result = $chat->addUser($userId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::AddUser($chatId, $userId);
```

#### Remove User from Chat | Удаление пользователя из чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$chat = \Bitrix\Im\Chat::getById($chatId);
$result = $chat->removeUser($userId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::RemoveUser($chatId, $userId);
```

#### Get Chat Users | Получение пользователей чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$chat = \Bitrix\Im\Chat::getById($chatId);
$users = $chat->getUsers();

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$users = CIMChat::GetUsers($chatId);
```

#### Set Chat Admin | Назначение администратора чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$chat = \Bitrix\Im\Chat::getById($chatId);
$result = $chat->setAdmin($userId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::SetAdmin($chatId, $userId);
```

### File Management | Управление файлами

#### Upload File | Загрузка файла

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$file = \Bitrix\Im\File::upload([
    'CHAT_ID' => $chatId,
    'USER_ID' => $USER->GetID(),
    'FILE_ID' => $fileId,
    'NAME' => 'document.pdf',
    'DESCRIPTION' => 'Project documentation'
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$file = CIMDisk::UploadFile($chatId, $USER->GetID(), $fileId, [
    'NAME' => 'document.pdf',
    'DESCRIPTION' => 'Project documentation'
]);
```

#### Get File | Получение файла

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$file = \Bitrix\Im\File::getById($fileId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$file = CIMDisk::GetFile($fileId);
```

#### Get Chat Files | Получение файлов чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$files = \Bitrix\Im\File::getList([
    'select' => ['*'],
    'filter' => [
        'CHAT_ID' => $chatId
    ],
    'order' => ['DATE_CREATE' => 'DESC']
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$files = CIMDisk::GetFiles($chatId, ['DATE_CREATE' => 'DESC']);
```

#### Delete File | Удаление файла

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$file = \Bitrix\Im\File::getById($fileId);
$result = $file->delete();

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMDisk::DeleteFile($fileId);
```

### Notifications | Уведомления

#### Send Notification | Отправка уведомления

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$notification = \Bitrix\Im\Notify::add([
    'TO_USER_ID' => $userId,
    'FROM_USER_ID' => $USER->GetID(),
    'NOTIFY_TYPE' => 'IM',
    'NOTIFY_MODULE' => 'im',
    'NOTIFY_EVENT' => 'message',
    'NOTIFY_TITLE' => 'New message',
    'NOTIFY_MESSAGE' => 'You have a new message in chat',
    'NOTIFY_DATA' => [
        'CHAT_ID' => $chatId,
        'MESSAGE_ID' => $messageId
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$notification = CIMNotify::Add([
    'TO_USER_ID' => $userId,
    'FROM_USER_ID' => $USER->GetID(),
    'NOTIFY_TYPE' => 'IM',
    'NOTIFY_MODULE' => 'im',
    'NOTIFY_EVENT' => 'message',
    'NOTIFY_TITLE' => 'New message',
    'NOTIFY_MESSAGE' => 'You have a new message in chat',
    'NOTIFY_DATA' => [
        'CHAT_ID' => $chatId,
        'MESSAGE_ID' => $messageId
    ]
]);
```

#### Get Notifications | Получение уведомлений

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$notifications = \Bitrix\Im\Notify::getList([
    'select' => ['*'],
    'filter' => [
        'TO_USER_ID' => $USER->GetID(),
        'NOTIFY_TYPE' => 'IM'
    ],
    'order' => ['DATE_CREATE' => 'DESC'],
    'limit' => 50
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$notifications = CIMNotify::GetList([
    'TO_USER_ID' => $USER->GetID(),
    'NOTIFY_TYPE' => 'IM'
], ['DATE_CREATE' => 'DESC'], 50);
```

#### Mark Notification as Read | Отметка уведомления как прочитанного

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$notification = \Bitrix\Im\Notify::getById($notificationId);
$result = $notification->markAsRead();

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMNotify::MarkAsRead($notificationId);
```

#### Delete Notification | Удаление уведомления

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$notification = \Bitrix\Im\Notify::getById($notificationId);
$result = $notification->delete();

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMNotify::Delete($notificationId);
```

### Bot Management | Управление ботами

#### Create Bot | Создание бота

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$bot = \Bitrix\Im\Bot::add([
    'NAME' => 'Assistant Bot',
    'DESCRIPTION' => 'Bot for answering common questions',
    'TYPE' => 'HUMAN',
    'CLASS' => '\\Bitrix\\Im\\Bot\\Assistant',
    'METHOD_MESSAGE' => 'onMessage',
    'METHOD_WELCOME' => 'onWelcome',
    'METHOD_BOT_DELETE' => 'onBotDelete',
    'METHOD_LANGUAGE' => 'onLanguage',
    'LANG' => ['ru', 'en'],
    'PROPERTIES' => [
        'LOGIN' => 'assistant_bot',
        'NAME' => 'Assistant',
        'WORK_POSITION' => 'Bot',
        'PERSONAL_GENDER' => 'M',
        'PERSONAL_PROFESSION' => 'Assistant',
        'PERSONAL_WWW' => '',
        'PERSONAL_BIRTHDAY' => '',
        'PERSONAL_PHOTO' => '',
        'PERSONAL_ICQ' => '',
        'PERSONAL_PHONE' => '',
        'PERSONAL_FAX' => '',
        'PERSONAL_MOBILE' => '',
        'PERSONAL_CITY' => '',
        'WORK_COMPANY' => 'Bitrix24',
        'WORK_POSITION' => 'Bot',
        'WORK_PHONE' => '',
        'WORK_FAX' => '',
        'WORK_MAILBOX' => '',
        'WORK_CITY' => '',
        'WORK_STATE' => '',
        'WORK_ZIP' => '',
        'WORK_COUNTRY' => '',
        'WORK_PROFILE' => '',
        'WORK_LOGO' => '',
        'WORK_NOTES' => '',
        'WORK_WWW' => ''
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$bot = CIMBot::Add([
    'NAME' => 'Assistant Bot',
    'DESCRIPTION' => 'Bot for answering common questions',
    'TYPE' => 'HUMAN',
    'CLASS' => '\\Bitrix\\Im\\Bot\\Assistant',
    'METHOD_MESSAGE' => 'onMessage',
    'METHOD_WELCOME' => 'onWelcome',
    'METHOD_BOT_DELETE' => 'onBotDelete',
    'METHOD_LANGUAGE' => 'onLanguage',
    'LANG' => ['ru', 'en'],
    'PROPERTIES' => [
        'LOGIN' => 'assistant_bot',
        'NAME' => 'Assistant',
        'WORK_POSITION' => 'Bot',
        'PERSONAL_GENDER' => 'M',
        'PERSONAL_PROFESSION' => 'Assistant',
        'PERSONAL_WWW' => '',
        'PERSONAL_BIRTHDAY' => '',
        'PERSONAL_PHOTO' => '',
        'PERSONAL_ICQ' => '',
        'PERSONAL_PHONE' => '',
        'PERSONAL_FAX' => '',
        'PERSONAL_MOBILE' => '',
        'PERSONAL_CITY' => '',
        'WORK_COMPANY' => 'Bitrix24',
        'WORK_POSITION' => 'Bot',
        'WORK_PHONE' => '',
        'WORK_FAX' => '',
        'WORK_MAILBOX' => '',
        'WORK_CITY' => '',
        'WORK_STATE' => '',
        'WORK_ZIP' => '',
        'WORK_COUNTRY' => '',
        'WORK_PROFILE' => '',
        'WORK_LOGO' => '',
        'WORK_NOTES' => '',
        'WORK_WWW' => ''
    ]
]);
```

#### Get Bot | Получение бота

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$bot = \Bitrix\Im\Bot::getById($botId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$bot = CIMBot::GetByID($botId);
```

#### Get Bot List | Получение списка ботов

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$bots = \Bitrix\Im\Bot::getList([
    'select' => ['*'],
    'filter' => [
        'TYPE' => 'HUMAN'
    ],
    'order' => ['NAME' => 'ASC']
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$bots = CIMBot::GetList([], ['TYPE' => 'HUMAN'], ['NAME' => 'ASC']);
```

#### Update Bot | Обновление бота

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$bot = \Bitrix\Im\Bot::getById($botId);
$result = $bot->update([
    'NAME' => 'Updated Assistant Bot',
    'DESCRIPTION' => 'Updated bot for answering common questions'
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMBot::Update($botId, [
    'NAME' => 'Updated Assistant Bot',
    'DESCRIPTION' => 'Updated bot for answering common questions'
]);
```

#### Delete Bot | Удаление бота

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$bot = \Bitrix\Im\Bot::getById($botId);
$result = $bot->delete();

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMBot::Delete($botId);
```

### Command Management | Управление командами

#### Register Command | Регистрация команды

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$command = \Bitrix\Im\Command::register([
    'BOT_ID' => $botId,
    'COMMAND' => 'start',
    'COMMAND_ID' => 'start',
    'TITLE' => 'Start',
    'DESCRIPTION' => 'Start the bot',
    'PARAMS' => [
        'COMMAND' => 'start',
        'HIDDEN' => 'N'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$command = CIMBot::RegisterCommand($botId, [
    'COMMAND' => 'start',
    'COMMAND_ID' => 'start',
    'TITLE' => 'Start',
    'DESCRIPTION' => 'Start the bot',
    'PARAMS' => [
        'COMMAND' => 'start',
        'HIDDEN' => 'N'
    ]
]);
```

#### Get Command | Получение команды

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$command = \Bitrix\Im\Command::getById($commandId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$command = CIMBot::GetCommand($commandId);
```

#### Get Command List | Получение списка команд

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$commands = \Bitrix\Im\Command::getList([
    'select' => ['*'],
    'filter' => [
        'BOT_ID' => $botId
    ],
    'order' => ['TITLE' => 'ASC']
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$commands = CIMBot::GetCommandList($botId, ['TITLE' => 'ASC']);
```

#### Update Command | Обновление команды

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$command = \Bitrix\Im\Command::getById($commandId);
$result = $command->update([
    'TITLE' => 'Updated Start',
    'DESCRIPTION' => 'Updated start the bot'
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMBot::UpdateCommand($commandId, [
    'TITLE' => 'Updated Start',
    'DESCRIPTION' => 'Updated start the bot'
]);
```

#### Delete Command | Удаление команды

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$command = \Bitrix\Im\Command::getById($commandId);
$result = $command->delete();

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMBot::DeleteCommand($commandId);
```

### Integration with Other Modules | Интеграция с другими модулями

#### Create Task from Chat | Создание задачи из чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Requires: Bitrix\Main\Loader::includeModule('tasks')
// Требуется: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('tasks')
$task = \Bitrix\Im\Integration\Tasks::createFromChat([
    'CHAT_ID' => $chatId,
    'TITLE' => 'New task from chat',
    'DESCRIPTION' => 'Task description',
    'RESPONSIBLE_ID' => $userId,
    'CREATOR_ID' => $USER->GetID(),
    'GROUP_ID' => $groupId
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Requires: CModule::IncludeModule('tasks')
// Требуется: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('tasks')
$task = CIMTask::CreateFromChat([
    'CHAT_ID' => $chatId,
    'TITLE' => 'New task from chat',
    'DESCRIPTION' => 'Task description',
    'RESPONSIBLE_ID' => $userId,
    'CREATOR_ID' => $USER->GetID(),
    'GROUP_ID' => $groupId
]);
```

#### Create Calendar Event from Chat | Создание события календаря из чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
$event = \Bitrix\Im\Integration\Calendar::createFromChat([
    'CHAT_ID' => $chatId,
    'NAME' => 'Meeting from chat',
    'DESCRIPTION' => 'Meeting description',
    'FROM' => new \Bitrix\Main\Type\DateTime('2023-12-01 10:00:00'),
    'TO' => new \Bitrix\Main\Type\DateTime('2023-12-01 11:00:00'),
    'TZ_FROM' => 'Europe/Moscow',
    'TZ_TO' => 'Europe/Moscow',
    'ACCESSIBILITY' => 'busy',
    'IMPORTANCE' => 'normal',
    'EVENT_TYPE' => 'meeting',
    'COLOR' => '#FF0000',
    'TEXT_COLOR' => '#FFFFFF',
    'LOCATION' => 'Conference Room',
    'ATTENDEES' => [
        [
            'USER_ID' => $userId1,
            'STATUS' => 'accepted'
        ],
        [
            'USER_ID' => $userId2,
            'STATUS' => 'pending'
        ]
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('calendar')
$event = CIMCalendar::CreateFromChat([
    'CHAT_ID' => $chatId,
    'NAME' => 'Meeting from chat',
    'DESCRIPTION' => 'Meeting description',
    'FROM' => '2023-12-01 10:00:00',
    'TO' => '2023-12-01 11:00:00',
    'TZ_FROM' => 'Europe/Moscow',
    'TZ_TO' => 'Europe/Moscow',
    'ACCESSIBILITY' => 'busy',
    'IMPORTANCE' => 'normal',
    'EVENT_TYPE' => 'meeting',
    'COLOR' => '#FF0000',
    'TEXT_COLOR' => '#FFFFFF',
    'LOCATION' => 'Conference Room',
    'ATTENDEES' => [
        [
            'USER_ID' => $userId1,
            'STATUS' => 'accepted'
        ],
        [
            'USER_ID' => $userId2,
            'STATUS' => 'pending'
        ]
    ]
]);
```

#### Create CRM Activity from Chat | Создание активности CRM из чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Requires: Bitrix\Main\Loader::includeModule('crm')
// Требуется: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('crm')
$activity = \Bitrix\Im\Integration\Crm::createFromChat([
    'CHAT_ID' => $chatId,
    'ENTITY_TYPE' => 'LEAD',
    'ENTITY_ID' => $leadId,
    'SUBJECT' => 'Activity from chat',
    'DESCRIPTION' => 'Activity description',
    'RESPONSIBLE_ID' => $USER->GetID(),
    'DIRECTION' => 'INCOMING',
    'TYPE_ID' => 'CALL',
    'PRIORITY' => 'NORMAL',
    'COMPLETED' => 'N'
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Requires: CModule::IncludeModule('crm')
// Требуется: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('crm')
$activity = CIMCrm::CreateFromChat([
    'CHAT_ID' => $chatId,
    'ENTITY_TYPE' => 'LEAD',
    'ENTITY_ID' => $leadId,
    'SUBJECT' => 'Activity from chat',
    'DESCRIPTION' => 'Activity description',
    'RESPONSIBLE_ID' => $USER->GetID(),
    'DIRECTION' => 'INCOMING',
    'TYPE_ID' => 'CALL',
    'PRIORITY' => 'NORMAL',
    'COMPLETED' => 'N'
]);
```

### Client Integration | Интеграция с клиентом

#### Get Client Script | Получение клиентского скрипта

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$script = \Bitrix\Im\Client::getScript([
    'USER_ID' => $USER->GetID(),
    'LANGUAGE_ID' => LANGUAGE_ID,
    'DEVICE_TYPE' => 'desktop'
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$script = CIMClient::GetScript([
    'USER_ID' => $USER->GetID(),
    'LANGUAGE_ID' => LANGUAGE_ID,
    'DEVICE_TYPE' => 'desktop'
]);
```

#### Initialize Client | Инициализация клиента

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$client = \Bitrix\Im\Client::initialize([
    'USER_ID' => $USER->GetID(),
    'DEVICE_TYPE' => 'desktop'
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$client = CIMClient::Initialize([
    'USER_ID' => $USER->GetID(),
    'DEVICE_TYPE' => 'desktop'
]);
```

#### Get Client Settings | Получение настроек клиента

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$settings = \Bitrix\Im\Client::getSettings($USER->GetID());

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$settings = CIMClient::GetSettings($USER->GetID());
```

#### Update Client Settings | Обновление настроек клиента

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\Client::updateSettings($USER->GetID(), [
    'DEVICE_TYPE' => 'mobile',
    'ENABLE_NOTIFICATIONS' => 'Y',
    'ENABLE_SOUND' => 'Y',
    'ENABLE_DESKTOP' => 'N'
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMClient::UpdateSettings($USER->GetID(), [
    'DEVICE_TYPE' => 'mobile',
    'ENABLE_NOTIFICATIONS' => 'Y',
    'ENABLE_SOUND' => 'Y',
    'ENABLE_DESKTOP' => 'N'
]);
```

## Handlers | Обработчики

### Message Handlers | Обработчики сообщений

#### Message Handler | Обработчик сообщения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
class CustomMessageHandler extends \Bitrix\Im\Message\Handler
{
    public function onBeforeMessageCreate($params)
    {
        // Code executed before message is created
        // Код, выполняемый перед созданием сообщения
        return $params;
    }
    
    public function onAfterMessageCreate($params, $result)
    {
        // Code executed after message is created
        // Код, выполняемый после создания сообщения
        return $result;
    }
    
    public function onBeforeMessageUpdate($params)
    {
        // Code executed before message is updated
        // Код, выполняемый перед обновлением сообщения
        return $params;
    }
    
    public function onAfterMessageUpdate($params, $result)
    {
        // Code executed after message is updated
        // Код, выполняемый после обновления сообщения
        return $result;
    }
    
    public function onBeforeMessageDelete($params)
    {
        // Code executed before message is deleted
        // Код, выполняемый перед удалением сообщения
        return $params;
    }
    
    public function onAfterMessageDelete($params, $result)
    {
        // Code executed after message is deleted
        // Код, выполняемый после удаления сообщения
        return $result;
    }
    
    public function onBeforeMessageRead($params)
    {
        // Code executed before message is read
        // Код, выполняемый перед прочтением сообщения
        return $params;
    }
    
    public function onAfterMessageRead($params, $result)
    {
        // Code executed after message is read
        // Код, выполняемый после прочтения сообщения
        return $result;
    }
    
    public function onBeforeMessageLike($params)
    {
        // Code executed before message is liked
        // Код, выполняемый перед добавлением лайка к сообщению
        return $params;
    }
    
    public function onAfterMessageLike($params, $result)
    {
        // Code executed after message is liked
        // Код, выполняемый после добавления лайка к сообщению
        return $result;
    }
    
    public function onBeforeMessageUnlike($params)
    {
        // Code executed before message is unliked
        // Код, выполняемый перед удалением лайка с сообщения
        return $params;
    }
    
    public function onAfterMessageUnlike($params, $result)
    {
        // Code executed after message is unliked
        // Код, выполняемый после удаления лайка с сообщения
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Im\Message\Handler::register('custom_message', CustomMessageHandler::class);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
class CCustomMessageHandler extends CIMMessageHandler
{
    public function OnBeforeMessageCreate($params)
    {
        // Code executed before message is created
        // Код, выполняемый перед созданием сообщения
        return $params;
    }
    
    public function OnAfterMessageCreate($params, $result)
    {
        // Code executed after message is created
        // Код, выполняемый после создания сообщения
        return $result;
    }
    
    public function OnBeforeMessageUpdate($params)
    {
        // Code executed before message is updated
        // Код, выполняемый перед обновлением сообщения
        return $params;
    }
    
    public function OnAfterMessageUpdate($params, $result)
    {
        // Code executed after message is updated
        // Код, выполняемый после обновления сообщения
        return $result;
    }
    
    public function OnBeforeMessageDelete($params)
    {
        // Code executed before message is deleted
        // Код, выполняемый перед удалением сообщения
        return $params;
    }
    
    public function OnAfterMessageDelete($params, $result)
    {
        // Code executed after message is deleted
        // Код, выполняемый после удаления сообщения
        return $result;
    }
    
    public function OnBeforeMessageRead($params)
    {
        // Code executed before message is read
        // Код, выполняемый перед прочтением сообщения
        return $params;
    }
    
    public function OnAfterMessageRead($params, $result)
    {
        // Code executed after message is read
        // Код, выполняемый после прочтения сообщения
        return $result;
    }
    
    public function OnBeforeMessageLike($params)
    {
        // Code executed before message is liked
        // Код, выполняемый перед добавлением лайка к сообщению
        return $params;
    }
    
    public function OnAfterMessageLike($params, $result)
    {
        // Code executed after message is liked
        // Код, выполняемый после добавления лайка к сообщению
        return $result;
    }
    
    public function OnBeforeMessageUnlike($params)
    {
        // Code executed before message is unliked
        // Код, выполняемый перед удалением лайка с сообщения
        return $params;
    }
    
    public function OnAfterMessageUnlike($params, $result)
    {
        // Code executed after message is unliked
        // Код, выполняемый после удаления лайка с сообщения
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CIMMessageHandler::Register('custom_message', 'CCustomMessageHandler');
```

### Chat Handlers | Обработчики чатов

#### Chat Handler | Обработчик чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
class CustomChatHandler extends \Bitrix\Im\Chat\Handler
{
    public function onBeforeChatCreate($params)
    {
        // Code executed before chat is created
        // Код, выполняемый перед созданием чата
        return $params;
    }
    
    public function onAfterChatCreate($params, $result)
    {
        // Code executed after chat is created
        // Код, выполняемый после создания чата
        return $result;
    }
    
    public function onBeforeChatUpdate($params)
    {
        // Code executed before chat is updated
        // Код, выполняемый перед обновлением чата
        return $params;
    }
    
    public function onAfterChatUpdate($params, $result)
    {
        // Code executed after chat is updated
        // Код, выполняемый после обновления чата
        return $result;
    }
    
    public function onBeforeChatDelete($params)
    {
        // Code executed before chat is deleted
        // Код, выполняемый перед удалением чата
        return $params;
    }
    
    public function onAfterChatDelete($params, $result)
    {
        // Code executed after chat is deleted
        // Код, выполняемый после удаления чата
        return $result;
    }
    
    public function onBeforeChatJoin($params)
    {
        // Code executed before user joins chat
        // Код, выполняемый перед присоединением пользователя к чату
        return $params;
    }
    
    public function onAfterChatJoin($params, $result)
    {
        // Code executed after user joins chat
        // Код, выполняемый после присоединения пользователя к чату
        return $result;
    }
    
    public function onBeforeChatLeave($params)
    {
        // Code executed before user leaves chat
        // Код, выполняемый перед выходом пользователя из чата
        return $params;
    }
    
    public function onAfterChatLeave($params, $result)
    {
        // Code executed after user leaves chat
        // Код, выполняемый после выхода пользователя из чата
        return $result;
    }
    
    public function onBeforeChatInvite($params)
    {
        // Code executed before user is invited to chat
        // Код, выполняемый перед приглашением пользователя в чат
        return $params;
    }
    
    public function onAfterChatInvite($params, $result)
    {
        // Code executed after user is invited to chat
        // Код, выполняемый после приглашения пользователя в чат
        return $result;
    }
    
    public function onBeforeChatKick($params)
    {
        // Code executed before user is kicked from chat
        // Код, выполняемый перед исключением пользователя из чата
        return $params;
    }
    
    public function onAfterChatKick($params, $result)
    {
        // Code executed after user is kicked from chat
        // Код, выполняемый после исключения пользователя из чата
        return $result;
    }
    
    public function onBeforeChatMute($params)
    {
        // Code executed before chat is muted
        // Код, выполняемый перед отключением уведомлений чата
        return $params;
    }
    
    public function onAfterChatMute($params, $result)
    {
        // Code executed after chat is muted
        // Код, выполняемый после отключения уведомлений чата
        return $result;
    }
    
    public function onBeforeChatUnmute($params)
    {
        // Code executed before chat is unmuted
        // Код, выполняемый перед включением уведомлений чата
        return $params;
    }
    
    public function onAfterChatUnmute($params, $result)
    {
        // Code executed after chat is unmuted
        // Код, выполняемый после включения уведомлений чата
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Im\Chat\Handler::register('custom_chat', CustomChatHandler::class);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
class CCustomChatHandler extends CIMChatHandler
{
    public function OnBeforeChatCreate($params)
    {
        // Code executed before chat is created
        // Код, выполняемый перед созданием чата
        return $params;
    }
    
    public function OnAfterChatCreate($params, $result)
    {
        // Code executed after chat is created
        // Код, выполняемый после создания чата
        return $result;
    }
    
    public function OnBeforeChatUpdate($params)
    {
        // Code executed before chat is updated
        // Код, выполняемый перед обновлением чата
        return $params;
    }
    
    public function OnAfterChatUpdate($params, $result)
    {
        // Code executed after chat is updated
        // Код, выполняемый после обновления чата
        return $result;
    }
    
    public function OnBeforeChatDelete($params)
    {
        // Code executed before chat is deleted
        // Код, выполняемый перед удалением чата
        return $params;
    }
    
    public function OnAfterChatDelete($params, $result)
    {
        // Code executed after chat is deleted
        // Код, выполняемый после удаления чата
        return $result;
    }
    
    public function OnBeforeChatJoin($params)
    {
        // Code executed before user joins chat
        // Код, выполняемый перед присоединением пользователя к чату
        return $params;
    }
    
    public function OnAfterChatJoin($params, $result)
    {
        // Code executed after user joins chat
        // Код, выполняемый после присоединения пользователя к чату
        return $result;
    }
    
    public function OnBeforeChatLeave($params)
    {
        // Code executed before user leaves chat
        // Код, выполняемый перед выходом пользователя из чата
        return $params;
    }
    
    public function OnAfterChatLeave($params, $result)
    {
        // Code executed after user leaves chat
        // Код, выполняемый после выхода пользователя из чата
        return $result;
    }
    
    public function OnBeforeChatInvite($params)
    {
        // Code executed before user is invited to chat
        // Код, выполняемый перед приглашением пользователя в чат
        return $params;
    }
    
    public function OnAfterChatInvite($params, $result)
    {
        // Code executed after user is invited to chat
        // Код, выполняемый после приглашения пользователя в чат
        return $result;
    }
    
    public function OnBeforeChatKick($params)
    {
        // Code executed before user is kicked from chat
        // Код, выполняемый перед исключением пользователя из чата
        return $params;
    }
    
    public function OnAfterChatKick($params, $result)
    {
        // Code executed after user is kicked from chat
        // Код, выполняемый после исключения пользователя из чата
        return $result;
    }
    
    public function OnBeforeChatMute($params)
    {
        // Code executed before chat is muted
        // Код, выполняемый перед отключением уведомлений чата
        return $params;
    }
    
    public function OnAfterChatMute($params, $result)
    {
        // Code executed after chat is muted
        // Код, выполняемый после отключения уведомлений чата
        return $result;
    }
    
    public function OnBeforeChatUnmute($params)
    {
        // Code executed before chat is unmuted
        // Код, выполняемый перед включением уведомлений чата
        return $params;
    }
    
    public function OnAfterChatUnmute($params, $result)
    {
        // Code executed after chat is unmuted
        // Код, выполняемый после включения уведомлений чата
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CIMChatHandler::Register('custom_chat', 'CCustomChatHandler');
```

### User Handlers | Обработчики пользователей

#### User Handler | Обработчик пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
class CustomUserHandler extends \Bitrix\Im\User\Handler
{
    public function onBeforeUserCreate($params)
    {
        // Code executed before user is created
        // Код, выполняемый перед созданием пользователя
        return $params;
    }
    
    public function onAfterUserCreate($params, $result)
    {
        // Code executed after user is created
        // Код, выполняемый после создания пользователя
        return $result;
    }
    
    public function onBeforeUserUpdate($params)
    {
        // Code executed before user is updated
        // Код, выполняемый перед обновлением пользователя
        return $params;
    }
    
    public function onAfterUserUpdate($params, $result)
    {
        // Code executed after user is updated
        // Код, выполняемый после обновления пользователя
        return $result;
    }
    
    public function onBeforeUserDelete($params)
    {
        // Code executed before user is deleted
        // Код, выполняемый перед удалением пользователя
        return $params;
    }
    
    public function onAfterUserDelete($params, $result)
    {
        // Code executed after user is deleted
        // Код, выполняемый после удаления пользователя
        return $result;
    }
    
    public function onBeforeUserStatusUpdate($params)
    {
        // Code executed before user status is updated
        // Код, выполняемый перед обновлением статуса пользователя
        return $params;
    }
    
    public function onAfterUserStatusUpdate($params, $result)
    {
        // Code executed after user status is updated
        // Код, выполняемый после обновления статуса пользователя
        return $result;
    }
    
    public function onBeforeUserAvatarUpdate($params)
    {
        // Code executed before user avatar is updated
        // Код, выполняемый перед обновлением аватара пользователя
        return $params;
    }
    
    public function onAfterUserAvatarUpdate($params, $result)
    {
        // Code executed after user avatar is updated
        // Код, выполняемый после обновления аватара пользователя
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Im\User\Handler::register('custom_user', CustomUserHandler::class);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
class CCustomUserHandler extends CIMUserHandler
{
    public function OnBeforeUserCreate($params)
    {
        // Code executed before user is created
        // Код, выполняемый перед созданием пользователя
        return $params;
    }
    
    public function OnAfterUserCreate($params, $result)
    {
        // Code executed after user is created
        // Код, выполняемый после создания пользователя
        return $result;
    }
    
    public function OnBeforeUserUpdate($params)
    {
        // Code executed before user is updated
        // Код, выполняемый перед обновлением пользователя
        return $params;
    }
    
    public function OnAfterUserUpdate($params, $result)
    {
        // Code executed after user is updated
        // Код, выполняемый после обновления пользователя
        return $result;
    }
    
    public function OnBeforeUserDelete($params)
    {
        // Code executed before user is deleted
        // Код, выполняемый перед удалением пользователя
        return $params;
    }
    
    public function OnAfterUserDelete($params, $result)
    {
        // Code executed after user is deleted
        // Код, выполняемый после удаления пользователя
        return $result;
    }
    
    public function OnBeforeUserStatusUpdate($params)
    {
        // Code executed before user status is updated
        // Код, выполняемый перед обновлением статуса пользователя
        return $params;
    }
    
    public function OnAfterUserStatusUpdate($params, $result)
    {
        // Code executed after user status is updated
        // Код, выполняемый после обновления статуса пользователя
        return $result;
    }
    
    public function OnBeforeUserAvatarUpdate($params)
    {
        // Code executed before user avatar is updated
        // Код, выполняемый перед обновлением аватара пользователя
        return $params;
    }
    
    public function OnAfterUserAvatarUpdate($params, $result)
    {
        // Code executed after user avatar is updated
        // Код, выполняемый после обновления аватара пользователя
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CIMUserHandler::Register('custom_user', 'CCustomUserHandler');
```

### File Handlers | Обработчики файлов

#### File Handler | Обработчик файла

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
class CustomFileHandler extends \Bitrix\Im\File\Handler
{
    public function onBeforeFileUpload($params)
    {
        // Code executed before file is uploaded
        // Код, выполняемый перед загрузкой файла
        return $params;
    }
    
    public function onAfterFileUpload($params, $result)
    {
        // Code executed after file is uploaded
        // Код, выполняемый после загрузки файла
        return $result;
    }
    
    public function onBeforeFileDelete($params)
    {
        // Code executed before file is deleted
        // Код, выполняемый перед удалением файла
        return $params;
    }
    
    public function onAfterFileDelete($params, $result)
    {
        // Code executed after file is deleted
        // Код, выполняемый после удаления файла
        return $result;
    }
    
    public function onBeforeFileDownload($params)
    {
        // Code executed before file is downloaded
        // Код, выполняемый перед скачиванием файла
        return $params;
    }
    
    public function onAfterFileDownload($params, $result)
    {
        // Code executed after file is downloaded
        // Код, выполняемый после скачивания файла
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Im\File\Handler::register('custom_file', CustomFileHandler::class);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
class CCustomFileHandler extends CIMFileHandler
{
    public function OnBeforeFileUpload($params)
    {
        // Code executed before file is uploaded
        // Код, выполняемый перед загрузкой файла
        return $params;
    }
    
    public function OnAfterFileUpload($params, $result)
    {
        // Code executed after file is uploaded
        // Код, выполняемый после загрузки файла
        return $result;
    }
    
    public function OnBeforeFileDelete($params)
    {
        // Code executed before file is deleted
        // Код, выполняемый перед удалением файла
        return $params;
    }
    
    public function OnAfterFileDelete($params, $result)
    {
        // Code executed after file is deleted
        // Код, выполняемый после удаления файла
        return $result;
    }
    
    public function OnBeforeFileDownload($params)
    {
        // Code executed before file is downloaded
        // Код, выполняемый перед скачиванием файла
        return $params;
    }
    
    public function OnAfterFileDownload($params, $result)
    {
        // Code executed after file is downloaded
        // Код, выполняемый после скачивания файла
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CIMFileHandler::Register('custom_file', 'CCustomFileHandler');
```

### Notification Handlers | Обработчики уведомлений

#### Notification Handler | Обработчик уведомлений

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
class CustomNotificationHandler extends \Bitrix\Im\Notification\Handler
{
    public function onBeforeNotificationCreate($params)
    {
        // Code executed before notification is created
        // Код, выполняемый перед созданием уведомления
        return $params;
    }
    
    public function onAfterNotificationCreate($params, $result)
    {
        // Code executed after notification is created
        // Код, выполняемый после создания уведомления
        return $result;
    }
    
    public function onBeforeNotificationUpdate($params)
    {
        // Code executed before notification is updated
        // Код, выполняемый перед обновлением уведомления
        return $params;
    }
    
    public function onAfterNotificationUpdate($params, $result)
    {
        // Code executed after notification is updated
        // Код, выполняемый после обновления уведомления
        return $result;
    }
    
    public function onBeforeNotificationDelete($params)
    {
        // Code executed before notification is deleted
        // Код, выполняемый перед удалением уведомления
        return $params;
    }
    
    public function onAfterNotificationDelete($params, $result)
    {
        // Code executed after notification is deleted
        // Код, выполняемый после удаления уведомления
        return $result;
    }
    
    public function onBeforeNotificationRead($params)
    {
        // Code executed before notification is read
        // Код, выполняемый перед прочтением уведомления
        return $params;
    }
    
    public function onAfterNotificationRead($params, $result)
    {
        // Code executed after notification is read
        // Код, выполняемый после прочтения уведомления
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Im\Notification\Handler::register('custom_notification', CustomNotificationHandler::class);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
class CCustomNotificationHandler extends CIMNotificationHandler
{
    public function OnBeforeNotificationCreate($params)
    {
        // Code executed before notification is created
        // Код, выполняемый перед созданием уведомления
        return $params;
    }
    
    public function OnAfterNotificationCreate($params, $result)
    {
        // Code executed after notification is created
        // Код, выполняемый после создания уведомления
        return $result;
    }
    
    public function OnBeforeNotificationUpdate($params)
    {
        // Code executed before notification is updated
        // Код, выполняемый перед обновлением уведомления
        return $params;
    }
    
    public function OnAfterNotificationUpdate($params, $result)
    {
        // Code executed after notification is updated
        // Код, выполняемый после обновления уведомления
        return $result;
    }
    
    public function OnBeforeNotificationDelete($params)
    {
        // Code executed before notification is deleted
        // Код, выполняемый перед удалением уведомления
        return $params;
    }
    
    public function OnAfterNotificationDelete($params, $result)
    {
        // Code executed after notification is deleted
        // Код, выполняемый после удаления уведомления
        return $result;
    }
    
    public function OnBeforeNotificationRead($params)
    {
        // Code executed before notification is read
        // Код, выполняемый перед прочтением уведомления
        return $params;
    }
    
    public function OnAfterNotificationRead($params, $result)
    {
        // Code executed after notification is read
        // Код, выполняемый после прочтения уведомления
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CIMNotificationHandler::Register('custom_notification', 'CCustomNotificationHandler');
```

## REST API | REST API

### Message Management | Управление сообщениями

#### Send Message | Отправка сообщения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\Message::add([
    'CHAT_ID' => $chatId,
    'FROM_USER_ID' => $USER->GetID(),
    'TO_USER_ID' => $userId,
    'MESSAGE' => 'Hello, this is a test message',
    'SYSTEM' => 'N',
    'AUTHOR_ID' => $USER->GetID(),
    'PARAMS' => [
        'KEYBOARD' => [
            'BOT_ID' => $botId,
            'BUTTONS' => [
                [
                    'TEXT' => 'Button 1',
                    'ACTION' => 'callback',
                    'DATA' => 'action1'
                ],
                [
                    'TEXT' => 'Button 2',
                    'ACTION' => 'callback',
                    'DATA' => 'action2'
                ]
            ]
        ]
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::AddMessage([
    'CHAT_ID' => $chatId,
    'FROM_USER_ID' => $USER->GetID(),
    'TO_USER_ID' => $userId,
    'MESSAGE' => 'Hello, this is a test message',
    'SYSTEM' => 'N',
    'AUTHOR_ID' => $USER->GetID(),
    'PARAMS' => [
        'KEYBOARD' => [
            'BOT_ID' => $botId,
            'BUTTONS' => [
                [
                    'TEXT' => 'Button 1',
                    'ACTION' => 'callback',
                    'DATA' => 'action1'
                ],
                [
                    'TEXT' => 'Button 2',
                    'ACTION' => 'callback',
                    'DATA' => 'action2'
                ]
            ]
        ]
    ]
]);
```

#### Update Message | Обновление сообщения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\Message::update($messageId, [
    'MESSAGE' => 'Updated message text',
    'EDIT_FLAG' => 'Y'
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::UpdateMessage($messageId, [
    'MESSAGE' => 'Updated message text',
    'EDIT_FLAG' => 'Y'
]);
```

#### Delete Message | Удаление сообщения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\Message::delete($messageId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::DeleteMessage($messageId);
```

#### Get Message | Получение сообщения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$message = \Bitrix\Im\Message::getById($messageId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$message = CIMChat::GetMessage($messageId);
```

### Chat Management | Управление чатами

#### Create Chat | Создание чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\Chat::add([
    'TITLE' => 'Group Chat',
    'DESCRIPTION' => 'This is a group chat',
    'TYPE' => 'GROUP',
    'USERS' => [$userId1, $userId2, $userId3],
    'OWNER_ID' => $USER->GetID(),
    'COLOR' => '#FF0000',
    'AVATAR' => $avatarId
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::Add([
    'TITLE' => 'Group Chat',
    'DESCRIPTION' => 'This is a group chat',
    'TYPE' => 'GROUP',
    'USERS' => [$userId1, $userId2, $userId3],
    'OWNER_ID' => $USER->GetID(),
    'COLOR' => '#FF0000',
    'AVATAR' => $avatarId
]);
```

#### Update Chat | Обновление чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\Chat::update($chatId, [
    'TITLE' => 'Updated Group Chat',
    'DESCRIPTION' => 'This is an updated group chat',
    'COLOR' => '#00FF00'
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::Update($chatId, [
    'TITLE' => 'Updated Group Chat',
    'DESCRIPTION' => 'This is an updated group chat',
    'COLOR' => '#00FF00'
]);
```

#### Delete Chat | Удаление чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\Chat::delete($chatId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::Delete($chatId);
```

#### Get Chat | Получение чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$chat = \Bitrix\Im\Chat::getById($chatId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$chat = CIMChat::GetByID($chatId);
```

#### Join Chat | Присоединение к чату

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\Chat::join($chatId, $userId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::Join($chatId, $userId);
```

#### Leave Chat | Выход из чата

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\Chat::leave($chatId, $userId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::Leave($chatId, $userId);
```

#### Invite to Chat | Приглашение в чат

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\Chat::invite($chatId, [$userId1, $userId2]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMChat::Invite($chatId, [$userId1, $userId2]);
```

### User Management | Управление пользователями

#### Update User Status | Обновление статуса пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\User::updateStatus($userId, 'online');

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMStatus::Set($userId, 'online');
```

#### Update User Avatar | Обновление аватара пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\User::updateAvatar($userId, $avatarId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMUser::SetAvatar($userId, $avatarId);
```

### File Management | Управление файлами

#### Upload File | Загрузка файла

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\File::upload([
    'CHAT_ID' => $chatId,
    'USER_ID' => $USER->GetID(),
    'FILE_ID' => $fileId,
    'NAME' => 'document.pdf',
    'DESCRIPTION' => 'This is a document'
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMDisk::UploadFile($chatId, $USER->GetID(), $fileId, 'document.pdf', 'This is a document');
```

#### Delete File | Удаление файла

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\File::delete($fileId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMDisk::DeleteFile($fileId);
```

### Notification Management | Управление уведомлениями

#### Create Notification | Создание уведомления

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\Notification::add([
    'USER_ID' => $userId,
    'TYPE' => 'SYSTEM',
    'TITLE' => 'Notification Title',
    'MESSAGE' => 'This is a notification message',
    'LINK' => '/path/to/page',
    'PARAMS' => [
        'KEY1' => 'VALUE1',
        'KEY2' => 'VALUE2'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMNotify::Add([
    'USER_ID' => $userId,
    'TYPE' => 'SYSTEM',
    'TITLE' => 'Notification Title',
    'MESSAGE' => 'This is a notification message',
    'LINK' => '/path/to/page',
    'PARAMS' => [
        'KEY1' => 'VALUE1',
        'KEY2' => 'VALUE2'
    ]
]);
```

#### Delete Notification | Удаление уведомления

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\Notification::delete($notificationId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMNotify::Delete($notificationId);
```

#### Mark Notification as Read | Отметка уведомления как прочитанного

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('im')
// Требуется: Bitrix\Main\Loader::includeModule('im')
$result = \Bitrix\Im\Notification::markAsRead($notificationId);

// Legacy
// Requires: CModule::IncludeModule('im')
// Требуется: CModule::IncludeModule('im')
$result = CIMNotify::MarkAsRead($notificationId);
``` 