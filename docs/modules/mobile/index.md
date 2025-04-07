# Mobile Module | Модуль Mobile

## Overview | Обзор

The Mobile module provides functionality for developing and managing mobile applications in Bitrix24. It enables developers to create mobile interfaces, handle push notifications, manage mobile settings, and integrate with native device features. The module supports both iOS and Android platforms, offering a comprehensive set of tools for mobile app development within the Bitrix24 ecosystem. | Модуль Mobile предоставляет функциональность для разработки и управления мобильными приложениями в Bitrix24. Он позволяет разработчикам создавать мобильные интерфейсы, обрабатывать push-уведомления, управлять мобильными настройками и интегрироваться с нативными функциями устройств. Модуль поддерживает как iOS, так и Android платформы, предлагая комплексный набор инструментов для разработки мобильных приложений в экосистеме Bitrix24.

## Methods | Методы

### Application Management | Управление приложениями

#### Get Application | Получение приложения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$app = \Bitrix\Mobile\App::getById($appId);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$app = CMobile::GetApp($appId);
```

#### Get Application List | Получение списка приложений

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$apps = \Bitrix\Mobile\App::getList([
    'select' => ['*'],
    'filter' => [
        'ACTIVE' => 'Y'
    ],
    'order' => ['NAME' => 'ASC']
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$apps = CMobile::GetAppList(['ACTIVE' => 'Y'], ['NAME' => 'ASC']);
```

#### Create Application | Создание приложения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$app = \Bitrix\Mobile\App::add([
    'NAME' => 'Custom Mobile App',
    'CODE' => 'custom_app',
    'DESCRIPTION' => 'Custom mobile application',
    'ICON' => '/bitrix/images/mobile/custom_app_icon.png',
    'ACTIVE' => 'Y',
    'SETTINGS' => [
        'ENABLE_PUSH' => 'Y',
        'ENABLE_OFFLINE' => 'Y',
        'ENABLE_LOCATION' => 'Y'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$app = CMobile::AddApp([
    'NAME' => 'Custom Mobile App',
    'CODE' => 'custom_app',
    'DESCRIPTION' => 'Custom mobile application',
    'ICON' => '/bitrix/images/mobile/custom_app_icon.png',
    'ACTIVE' => 'Y',
    'SETTINGS' => [
        'ENABLE_PUSH' => 'Y',
        'ENABLE_OFFLINE' => 'Y',
        'ENABLE_LOCATION' => 'Y'
    ]
]);
```

#### Update Application | Обновление приложения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$app = \Bitrix\Mobile\App::getById($appId);
$result = $app->update([
    'NAME' => 'Updated Custom Mobile App',
    'DESCRIPTION' => 'Updated custom mobile application',
    'SETTINGS' => [
        'ENABLE_PUSH' => 'N',
        'ENABLE_OFFLINE' => 'Y',
        'ENABLE_LOCATION' => 'N'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobile::UpdateApp($appId, [
    'NAME' => 'Updated Custom Mobile App',
    'DESCRIPTION' => 'Updated custom mobile application',
    'SETTINGS' => [
        'ENABLE_PUSH' => 'N',
        'ENABLE_OFFLINE' => 'Y',
        'ENABLE_LOCATION' => 'N'
    ]
]);
```

#### Delete Application | Удаление приложения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$app = \Bitrix\Mobile\App::getById($appId);
$result = $app->delete();

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobile::DeleteApp($appId);
```

### Push Notifications | Push-уведомления

#### Register Device | Регистрация устройства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$device = \Bitrix\Mobile\Push::registerDevice([
    'USER_ID' => $USER->GetID(),
    'DEVICE_ID' => 'device123',
    'DEVICE_TOKEN' => 'push_token_123',
    'DEVICE_TYPE' => 'ios',
    'APP_ID' => $appId,
    'DEVICE_NAME' => 'iPhone 12',
    'DEVICE_MODEL' => 'iPhone',
    'DEVICE_VERSION' => '14.5',
    'DEVICE_LANG' => 'en',
    'DEVICE_TIMEZONE' => 'America/New_York'
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$device = CMobilePush::RegisterDevice([
    'USER_ID' => $USER->GetID(),
    'DEVICE_ID' => 'device123',
    'DEVICE_TOKEN' => 'push_token_123',
    'DEVICE_TYPE' => 'ios',
    'APP_ID' => $appId,
    'DEVICE_NAME' => 'iPhone 12',
    'DEVICE_MODEL' => 'iPhone',
    'DEVICE_VERSION' => '14.5',
    'DEVICE_LANG' => 'en',
    'DEVICE_TIMEZONE' => 'America/New_York'
]);
```

#### Get Device | Получение устройства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$device = \Bitrix\Mobile\Push::getDevice($deviceId);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$device = CMobilePush::GetDevice($deviceId);
```

#### Get User Devices | Получение устройств пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$devices = \Bitrix\Mobile\Push::getUserDevices($USER->GetID());

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$devices = CMobilePush::GetUserDevices($USER->GetID());
```

#### Update Device | Обновление устройства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$device = \Bitrix\Mobile\Push::getDevice($deviceId);
$result = $device->update([
    'DEVICE_TOKEN' => 'new_push_token_123',
    'DEVICE_VERSION' => '14.6',
    'DEVICE_TIMEZONE' => 'Europe/Moscow'
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobilePush::UpdateDevice($deviceId, [
    'DEVICE_TOKEN' => 'new_push_token_123',
    'DEVICE_VERSION' => '14.6',
    'DEVICE_TIMEZONE' => 'Europe/Moscow'
]);
```

#### Delete Device | Удаление устройства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$device = \Bitrix\Mobile\Push::getDevice($deviceId);
$result = $device->delete();

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobilePush::DeleteDevice($deviceId);
```

#### Send Push Notification | Отправка push-уведомления

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$notification = \Bitrix\Mobile\Push::send([
    'USER_ID' => $userId,
    'MESSAGE' => 'New task assigned to you',
    'TITLE' => 'Task Notification',
    'SOUND' => 'default',
    'BADGE' => 1,
    'PARAMS' => [
        'TASK_ID' => $taskId,
        'ACTION' => 'open_task'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$notification = CMobilePush::Send([
    'USER_ID' => $userId,
    'MESSAGE' => 'New task assigned to you',
    'TITLE' => 'Task Notification',
    'SOUND' => 'default',
    'BADGE' => 1,
    'PARAMS' => [
        'TASK_ID' => $taskId,
        'ACTION' => 'open_task'
    ]
]);
```

#### Send Push Notification to Multiple Users | Отправка push-уведомления нескольким пользователям

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$notification = \Bitrix\Mobile\Push::sendToUsers([
    'USER_IDS' => [$userId1, $userId2, $userId3],
    'MESSAGE' => 'Team meeting in 5 minutes',
    'TITLE' => 'Meeting Reminder',
    'SOUND' => 'default',
    'BADGE' => 1,
    'PARAMS' => [
        'MEETING_ID' => $meetingId,
        'ACTION' => 'join_meeting'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$notification = CMobilePush::SendToUsers([
    'USER_IDS' => [$userId1, $userId2, $userId3],
    'MESSAGE' => 'Team meeting in 5 minutes',
    'TITLE' => 'Meeting Reminder',
    'SOUND' => 'default',
    'BADGE' => 1,
    'PARAMS' => [
        'MEETING_ID' => $meetingId,
        'ACTION' => 'join_meeting'
    ]
]);
```

#### Send Push Notification to Group | Отправка push-уведомления группе

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$notification = \Bitrix\Mobile\Push::sendToGroup([
    'GROUP_ID' => $groupId,
    'MESSAGE' => 'New document available',
    'TITLE' => 'Document Notification',
    'SOUND' => 'default',
    'BADGE' => 1,
    'PARAMS' => [
        'DOCUMENT_ID' => $documentId,
        'ACTION' => 'view_document'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$notification = CMobilePush::SendToGroup([
    'GROUP_ID' => $groupId,
    'MESSAGE' => 'New document available',
    'TITLE' => 'Document Notification',
    'SOUND' => 'default',
    'BADGE' => 1,
    'PARAMS' => [
        'DOCUMENT_ID' => $documentId,
        'ACTION' => 'view_document'
    ]
]);
```

### Mobile Settings | Мобильные настройки

#### Get Mobile Settings | Получение мобильных настроек

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$settings = \Bitrix\Mobile\Settings::get();

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$settings = CMobile::GetSettings();
```

#### Update Mobile Settings | Обновление мобильных настроек

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\Settings::update([
    'ENABLE_PUSH' => 'Y',
    'ENABLE_OFFLINE' => 'Y',
    'ENABLE_LOCATION' => 'Y',
    'ENABLE_CAMERA' => 'Y',
    'ENABLE_CONTACTS' => 'Y',
    'ENABLE_CALENDAR' => 'Y',
    'ENABLE_NOTIFICATIONS' => 'Y',
    'ENABLE_BACKGROUND_SYNC' => 'Y',
    'BACKGROUND_SYNC_INTERVAL' => 15,
    'MAX_OFFLINE_DAYS' => 7,
    'MAX_OFFLINE_SIZE' => 100,
    'DEFAULT_LANGUAGE' => 'en',
    'DEFAULT_TIMEZONE' => 'UTC'
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobile::UpdateSettings([
    'ENABLE_PUSH' => 'Y',
    'ENABLE_OFFLINE' => 'Y',
    'ENABLE_LOCATION' => 'Y',
    'ENABLE_CAMERA' => 'Y',
    'ENABLE_CONTACTS' => 'Y',
    'ENABLE_CALENDAR' => 'Y',
    'ENABLE_NOTIFICATIONS' => 'Y',
    'ENABLE_BACKGROUND_SYNC' => 'Y',
    'BACKGROUND_SYNC_INTERVAL' => 15,
    'MAX_OFFLINE_DAYS' => 7,
    'MAX_OFFLINE_SIZE' => 100,
    'DEFAULT_LANGUAGE' => 'en',
    'DEFAULT_TIMEZONE' => 'UTC'
]);
```

#### Get User Mobile Settings | Получение мобильных настроек пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$settings = \Bitrix\Mobile\Settings::getUserSettings($USER->GetID());

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$settings = CMobile::GetUserSettings($USER->GetID());
```

#### Update User Mobile Settings | Обновление мобильных настроек пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\Settings::updateUserSettings($USER->GetID(), [
    'ENABLE_PUSH' => 'Y',
    'ENABLE_OFFLINE' => 'Y',
    'ENABLE_LOCATION' => 'N',
    'ENABLE_CAMERA' => 'Y',
    'ENABLE_CONTACTS' => 'Y',
    'ENABLE_CALENDAR' => 'Y',
    'ENABLE_NOTIFICATIONS' => 'Y',
    'BACKGROUND_SYNC_INTERVAL' => 30,
    'LANGUAGE' => 'ru',
    'TIMEZONE' => 'Europe/Moscow'
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobile::UpdateUserSettings($USER->GetID(), [
    'ENABLE_PUSH' => 'Y',
    'ENABLE_OFFLINE' => 'Y',
    'ENABLE_LOCATION' => 'N',
    'ENABLE_CAMERA' => 'Y',
    'ENABLE_CONTACTS' => 'Y',
    'ENABLE_CALENDAR' => 'Y',
    'ENABLE_NOTIFICATIONS' => 'Y',
    'BACKGROUND_SYNC_INTERVAL' => 30,
    'LANGUAGE' => 'ru',
    'TIMEZONE' => 'Europe/Moscow'
]);
```

### Mobile UI | Мобильный интерфейс

#### Get Mobile Menu | Получение мобильного меню

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$menu = \Bitrix\Mobile\UI::getMenu([
    'USER_ID' => $USER->GetID(),
    'APP_ID' => $appId
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$menu = CMobile::GetMenu([
    'USER_ID' => $USER->GetID(),
    'APP_ID' => $appId
]);
```

#### Get Mobile Page | Получение мобильной страницы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$page = \Bitrix\Mobile\UI::getPage([
    'PAGE' => 'tasks',
    'USER_ID' => $USER->GetID(),
    'APP_ID' => $appId
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$page = CMobile::GetPage([
    'PAGE' => 'tasks',
    'USER_ID' => $USER->GetID(),
    'APP_ID' => $appId
]);
```

#### Get Mobile Component | Получение мобильного компонента

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$component = \Bitrix\Mobile\UI::getComponent([
    'COMPONENT' => 'bitrix:mobile.tasks.list',
    'PARAMS' => [
        'USER_ID' => $USER->GetID(),
        'FILTER' => 'active',
        'SORT' => 'deadline'
    ],
    'USER_ID' => $USER->GetID(),
    'APP_ID' => $appId
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$component = CMobile::GetComponent([
    'COMPONENT' => 'bitrix:mobile.tasks.list',
    'PARAMS' => [
        'USER_ID' => $USER->GetID(),
        'FILTER' => 'active',
        'SORT' => 'deadline'
    ],
    'USER_ID' => $USER->GetID(),
    'APP_ID' => $appId
]);
```

#### Get Mobile Template | Получение мобильного шаблона

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$template = \Bitrix\Mobile\UI::getTemplate([
    'TEMPLATE' => 'modern',
    'USER_ID' => $USER->GetID(),
    'APP_ID' => $appId
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$template = CMobile::GetTemplate([
    'TEMPLATE' => 'modern',
    'USER_ID' => $USER->GetID(),
    'APP_ID' => $appId
]);
```

### Mobile API | Мобильный API

#### Get Mobile API | Получение мобильного API

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$api = \Bitrix\Mobile\API::get([
    'USER_ID' => $USER->GetID(),
    'APP_ID' => $appId
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$api = CMobile::GetAPI([
    'USER_ID' => $USER->GetID(),
    'APP_ID' => $appId
]);
```

#### Register Mobile API | Регистрация мобильного API

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$api = \Bitrix\Mobile\API::register([
    'NAME' => 'Custom API',
    'CODE' => 'custom_api',
    'DESCRIPTION' => 'Custom mobile API',
    'METHODS' => [
        'getData' => [
            'NAME' => 'Get Data',
            'DESCRIPTION' => 'Get custom data',
            'PARAMS' => [
                'id' => [
                    'NAME' => 'ID',
                    'DESCRIPTION' => 'Data ID',
                    'TYPE' => 'integer',
                    'REQUIRED' => 'Y'
                ]
            ],
            'RETURN' => [
                'NAME' => 'Data',
                'DESCRIPTION' => 'Custom data',
                'TYPE' => 'array'
            ]
        ]
    ],
    'APP_ID' => $appId
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$api = CMobile::RegisterAPI([
    'NAME' => 'Custom API',
    'CODE' => 'custom_api',
    'DESCRIPTION' => 'Custom mobile API',
    'METHODS' => [
        'getData' => [
            'NAME' => 'Get Data',
            'DESCRIPTION' => 'Get custom data',
            'PARAMS' => [
                'id' => [
                    'NAME' => 'ID',
                    'DESCRIPTION' => 'Data ID',
                    'TYPE' => 'integer',
                    'REQUIRED' => 'Y'
                ]
            ],
            'RETURN' => [
                'NAME' => 'Data',
                'DESCRIPTION' => 'Custom data',
                'TYPE' => 'array'
            ]
        ]
    ],
    'APP_ID' => $appId
]);
```

#### Update Mobile API | Обновление мобильного API

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$api = \Bitrix\Mobile\API::getById($apiId);
$result = $api->update([
    'NAME' => 'Updated Custom API',
    'DESCRIPTION' => 'Updated custom mobile API',
    'METHODS' => [
        'getData' => [
            'NAME' => 'Get Data',
            'DESCRIPTION' => 'Get updated custom data',
            'PARAMS' => [
                'id' => [
                    'NAME' => 'ID',
                    'DESCRIPTION' => 'Data ID',
                    'TYPE' => 'integer',
                    'REQUIRED' => 'Y'
                ],
                'filter' => [
                    'NAME' => 'Filter',
                    'DESCRIPTION' => 'Data filter',
                    'TYPE' => 'array',
                    'REQUIRED' => 'N'
                ]
            ],
            'RETURN' => [
                'NAME' => 'Data',
                'DESCRIPTION' => 'Updated custom data',
                'TYPE' => 'array'
            ]
        ]
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobile::UpdateAPI($apiId, [
    'NAME' => 'Updated Custom API',
    'DESCRIPTION' => 'Updated custom mobile API',
    'METHODS' => [
        'getData' => [
            'NAME' => 'Get Data',
            'DESCRIPTION' => 'Get updated custom data',
            'PARAMS' => [
                'id' => [
                    'NAME' => 'ID',
                    'DESCRIPTION' => 'Data ID',
                    'TYPE' => 'integer',
                    'REQUIRED' => 'Y'
                ],
                'filter' => [
                    'NAME' => 'Filter',
                    'DESCRIPTION' => 'Data filter',
                    'TYPE' => 'array',
                    'REQUIRED' => 'N'
                ]
            ],
            'RETURN' => [
                'NAME' => 'Data',
                'DESCRIPTION' => 'Updated custom data',
                'TYPE' => 'array'
            ]
        ]
    ]
]);
```

#### Delete Mobile API | Удаление мобильного API

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$api = \Bitrix\Mobile\API::getById($apiId);
$result = $api->delete();

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobile::DeleteAPI($apiId);
```

### Mobile Offline | Мобильный оффлайн-режим

#### Get Offline Data | Получение оффлайн-данных

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$data = \Bitrix\Mobile\Offline::getData([
    'USER_ID' => $USER->GetID(),
    'ENTITY_TYPE' => 'tasks',
    'ENTITY_ID' => $taskId
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$data = CMobileOffline::GetData([
    'USER_ID' => $USER->GetID(),
    'ENTITY_TYPE' => 'tasks',
    'ENTITY_ID' => $taskId
]);
```

#### Save Offline Data | Сохранение оффлайн-данных

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\Offline::saveData([
    'USER_ID' => $USER->GetID(),
    'ENTITY_TYPE' => 'tasks',
    'ENTITY_ID' => $taskId,
    'DATA' => [
        'TITLE' => 'Offline Task',
        'DESCRIPTION' => 'Task created in offline mode',
        'DEADLINE' => '2023-12-31 23:59:59',
        'PRIORITY' => 'high',
        'RESPONSIBLE_ID' => $userId
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobileOffline::SaveData([
    'USER_ID' => $USER->GetID(),
    'ENTITY_TYPE' => 'tasks',
    'ENTITY_ID' => $taskId,
    'DATA' => [
        'TITLE' => 'Offline Task',
        'DESCRIPTION' => 'Task created in offline mode',
        'DEADLINE' => '2023-12-31 23:59:59',
        'PRIORITY' => 'high',
        'RESPONSIBLE_ID' => $userId
    ]
]);
```

#### Delete Offline Data | Удаление оффлайн-данных

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\Offline::deleteData([
    'USER_ID' => $USER->GetID(),
    'ENTITY_TYPE' => 'tasks',
    'ENTITY_ID' => $taskId
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobileOffline::DeleteData([
    'USER_ID' => $USER->GetID(),
    'ENTITY_TYPE' => 'tasks',
    'ENTITY_ID' => $taskId
]);
```

#### Sync Offline Data | Синхронизация оффлайн-данных

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\Offline::syncData([
    'USER_ID' => $USER->GetID(),
    'ENTITY_TYPE' => 'tasks',
    'DEVICE_ID' => 'device123'
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobileOffline::SyncData([
    'USER_ID' => $USER->GetID(),
    'ENTITY_TYPE' => 'tasks',
    'DEVICE_ID' => 'device123'
]);
```

### Mobile Analytics | Мобильная аналитика

#### Track Event | Отслеживание события

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\Analytics::trackEvent([
    'USER_ID' => $USER->GetID(),
    'EVENT_NAME' => 'app_open',
    'EVENT_PARAMS' => [
        'app_id' => $appId,
        'device_type' => 'ios',
        'device_version' => '14.5',
        'screen_resolution' => '1920x1080'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobileAnalytics::TrackEvent([
    'USER_ID' => $USER->GetID(),
    'EVENT_NAME' => 'app_open',
    'EVENT_PARAMS' => [
        'app_id' => $appId,
        'device_type' => 'ios',
        'device_version' => '14.5',
        'screen_resolution' => '1920x1080'
    ]
]);
```

#### Get Analytics | Получение аналитики

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$analytics = \Bitrix\Mobile\Analytics::get([
    'APP_ID' => $appId,
    'START_DATE' => '2023-01-01',
    'END_DATE' => '2023-12-31',
    'EVENT_NAME' => 'app_open',
    'GROUP_BY' => 'day'
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$analytics = CMobileAnalytics::Get([
    'APP_ID' => $appId,
    'START_DATE' => '2023-01-01',
    'END_DATE' => '2023-12-31',
    'EVENT_NAME' => 'app_open',
    'GROUP_BY' => 'day'
]);
```

#### Get User Analytics | Получение аналитики пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$analytics = \Bitrix\Mobile\Analytics::getUserAnalytics([
    'USER_ID' => $USER->GetID(),
    'APP_ID' => $appId,
    'START_DATE' => '2023-01-01',
    'END_DATE' => '2023-12-31'
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$analytics = CMobileAnalytics::GetUserAnalytics([
    'USER_ID' => $USER->GetID(),
    'APP_ID' => $appId,
    'START_DATE' => '2023-01-01',
    'END_DATE' => '2023-12-31'
]);
```

### Mobile Integration | Мобильная интеграция

#### Get Mobile Integration | Получение мобильной интеграции

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$integration = \Bitrix\Mobile\Integration::get([
    'CODE' => 'crm',
    'APP_ID' => $appId
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$integration = CMobile::GetIntegration([
    'CODE' => 'crm',
    'APP_ID' => $appId
]);
```

#### Register Mobile Integration | Регистрация мобильной интеграции

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$integration = \Bitrix\Mobile\Integration::register([
    'NAME' => 'Custom Integration',
    'CODE' => 'custom_integration',
    'DESCRIPTION' => 'Custom mobile integration',
    'HANDLER' => '\\Bitrix\\Mobile\\Integration\\Custom',
    'APP_ID' => $appId,
    'SETTINGS' => [
        'ENABLE_OFFLINE' => 'Y',
        'ENABLE_PUSH' => 'Y',
        'ENABLE_LOCATION' => 'Y'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$integration = CMobile::RegisterIntegration([
    'NAME' => 'Custom Integration',
    'CODE' => 'custom_integration',
    'DESCRIPTION' => 'Custom mobile integration',
    'HANDLER' => '\\Bitrix\\Mobile\\Integration\\Custom',
    'APP_ID' => $appId,
    'SETTINGS' => [
        'ENABLE_OFFLINE' => 'Y',
        'ENABLE_PUSH' => 'Y',
        'ENABLE_LOCATION' => 'Y'
    ]
]);
```

#### Update Mobile Integration | Обновление мобильной интеграции

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$integration = \Bitrix\Mobile\Integration::getById($integrationId);
$result = $integration->update([
    'NAME' => 'Updated Custom Integration',
    'DESCRIPTION' => 'Updated custom mobile integration',
    'SETTINGS' => [
        'ENABLE_OFFLINE' => 'N',
        'ENABLE_PUSH' => 'Y',
        'ENABLE_LOCATION' => 'N'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobile::UpdateIntegration($integrationId, [
    'NAME' => 'Updated Custom Integration',
    'DESCRIPTION' => 'Updated custom mobile integration',
    'SETTINGS' => [
        'ENABLE_OFFLINE' => 'N',
        'ENABLE_PUSH' => 'Y',
        'ENABLE_LOCATION' => 'N'
    ]
]);
```

#### Delete Mobile Integration | Удаление мобильной интеграции

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$integration = \Bitrix\Mobile\Integration::getById($integrationId);
$result = $integration->delete();

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobile::DeleteIntegration($integrationId);
```

## Handlers | Обработчики

### Application Handlers | Обработчики приложений

#### Application Handler | Обработчик приложения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
class CustomApplicationHandler extends \Bitrix\Mobile\Application\Handler
{
    public function onBeforeApplicationCreate($params)
    {
        // Code executed before application is created
        // Код, выполняемый перед созданием приложения
        return $params;
    }
    
    public function onAfterApplicationCreate($params, $result)
    {
        // Code executed after application is created
        // Код, выполняемый после создания приложения
        return $result;
    }
    
    public function onBeforeApplicationUpdate($params)
    {
        // Code executed before application is updated
        // Код, выполняемый перед обновлением приложения
        return $params;
    }
    
    public function onAfterApplicationUpdate($params, $result)
    {
        // Code executed after application is updated
        // Код, выполняемый после обновления приложения
        return $result;
    }
    
    public function onBeforeApplicationDelete($params)
    {
        // Code executed before application is deleted
        // Код, выполняемый перед удалением приложения
        return $params;
    }
    
    public function onAfterApplicationDelete($params, $result)
    {
        // Code executed after application is deleted
        // Код, выполняемый после удаления приложения
        return $result;
    }
    
    public function onBeforeApplicationInstall($params)
    {
        // Code executed before application is installed
        // Код, выполняемый перед установкой приложения
        return $params;
    }
    
    public function onAfterApplicationInstall($params, $result)
    {
        // Code executed after application is installed
        // Код, выполняемый после установки приложения
        return $result;
    }
    
    public function onBeforeApplicationUninstall($params)
    {
        // Code executed before application is uninstalled
        // Код, выполняемый перед удалением приложения
        return $params;
    }
    
    public function onAfterApplicationUninstall($params, $result)
    {
        // Code executed after application is uninstalled
        // Код, выполняемый после удаления приложения
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Mobile\Application\Handler::register('custom_application', CustomApplicationHandler::class);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
class CCustomApplicationHandler extends CMobileApplicationHandler
{
    public function OnBeforeApplicationCreate($params)
    {
        // Code executed before application is created
        // Код, выполняемый перед созданием приложения
        return $params;
    }
    
    public function OnAfterApplicationCreate($params, $result)
    {
        // Code executed after application is created
        // Код, выполняемый после создания приложения
        return $result;
    }
    
    public function OnBeforeApplicationUpdate($params)
    {
        // Code executed before application is updated
        // Код, выполняемый перед обновлением приложения
        return $params;
    }
    
    public function OnAfterApplicationUpdate($params, $result)
    {
        // Code executed after application is updated
        // Код, выполняемый после обновления приложения
        return $result;
    }
    
    public function OnBeforeApplicationDelete($params)
    {
        // Code executed before application is deleted
        // Код, выполняемый перед удалением приложения
        return $params;
    }
    
    public function OnAfterApplicationDelete($params, $result)
    {
        // Code executed after application is deleted
        // Код, выполняемый после удаления приложения
        return $result;
    }
    
    public function OnBeforeApplicationInstall($params)
    {
        // Code executed before application is installed
        // Код, выполняемый перед установкой приложения
        return $params;
    }
    
    public function OnAfterApplicationInstall($params, $result)
    {
        // Code executed after application is installed
        // Код, выполняемый после установки приложения
        return $result;
    }
    
    public function OnBeforeApplicationUninstall($params)
    {
        // Code executed before application is uninstalled
        // Код, выполняемый перед удалением приложения
        return $params;
    }
    
    public function OnAfterApplicationUninstall($params, $result)
    {
        // Code executed after application is uninstalled
        // Код, выполняемый после удаления приложения
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CMobileApplicationHandler::Register('custom_application', 'CCustomApplicationHandler');
```

### Device Handlers | Обработчики устройств

#### Device Handler | Обработчик устройства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
class CustomDeviceHandler extends \Bitrix\Mobile\Device\Handler
{
    public function onBeforeDeviceRegister($params)
    {
        // Code executed before device is registered
        // Код, выполняемый перед регистрацией устройства
        return $params;
    }
    
    public function onAfterDeviceRegister($params, $result)
    {
        // Code executed after device is registered
        // Код, выполняемый после регистрации устройства
        return $result;
    }
    
    public function onBeforeDeviceUnregister($params)
    {
        // Code executed before device is unregistered
        // Код, выполняемый перед отменой регистрации устройства
        return $params;
    }
    
    public function onAfterDeviceUnregister($params, $result)
    {
        // Code executed after device is unregistered
        // Код, выполняемый после отмены регистрации устройства
        return $result;
    }
    
    public function onBeforeDeviceUpdate($params)
    {
        // Code executed before device is updated
        // Код, выполняемый перед обновлением устройства
        return $params;
    }
    
    public function onAfterDeviceUpdate($params, $result)
    {
        // Code executed after device is updated
        // Код, выполняемый после обновления устройства
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Mobile\Device\Handler::register('custom_device', CustomDeviceHandler::class);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
class CCustomDeviceHandler extends CMobileDeviceHandler
{
    public function OnBeforeDeviceRegister($params)
    {
        // Code executed before device is registered
        // Код, выполняемый перед регистрацией устройства
        return $params;
    }
    
    public function OnAfterDeviceRegister($params, $result)
    {
        // Code executed after device is registered
        // Код, выполняемый после регистрации устройства
        return $result;
    }
    
    public function OnBeforeDeviceUnregister($params)
    {
        // Code executed before device is unregistered
        // Код, выполняемый перед отменой регистрации устройства
        return $params;
    }
    
    public function OnAfterDeviceUnregister($params, $result)
    {
        // Code executed after device is unregistered
        // Код, выполняемый после отмены регистрации устройства
        return $result;
    }
    
    public function OnBeforeDeviceUpdate($params)
    {
        // Code executed before device is updated
        // Код, выполняемый перед обновлением устройства
        return $params;
    }
    
    public function OnAfterDeviceUpdate($params, $result)
    {
        // Code executed after device is updated
        // Код, выполняемый после обновления устройства
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CMobileDeviceHandler::Register('custom_device', 'CCustomDeviceHandler');
```

### Push Notification Handlers | Обработчики push-уведомлений

#### Push Notification Handler | Обработчик push-уведомлений

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
class CustomPushNotificationHandler extends \Bitrix\Mobile\PushNotification\Handler
{
    public function onBeforePushNotificationSend($params)
    {
        // Code executed before push notification is sent
        // Код, выполняемый перед отправкой push-уведомления
        return $params;
    }
    
    public function onAfterPushNotificationSend($params, $result)
    {
        // Code executed after push notification is sent
        // Код, выполняемый после отправки push-уведомления
        return $result;
    }
    
    public function onBeforePushNotificationUpdate($params)
    {
        // Code executed before push notification is updated
        // Код, выполняемый перед обновлением push-уведомления
        return $params;
    }
    
    public function onAfterPushNotificationUpdate($params, $result)
    {
        // Code executed after push notification is updated
        // Код, выполняемый после обновления push-уведомления
        return $result;
    }
    
    public function onBeforePushNotificationDelete($params)
    {
        // Code executed before push notification is deleted
        // Код, выполняемый перед удалением push-уведомления
        return $params;
    }
    
    public function onAfterPushNotificationDelete($params, $result)
    {
        // Code executed after push notification is deleted
        // Код, выполняемый после удаления push-уведомления
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Mobile\PushNotification\Handler::register('custom_push_notification', CustomPushNotificationHandler::class);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
class CCustomPushNotificationHandler extends CMobilePushNotificationHandler
{
    public function OnBeforePushNotificationSend($params)
    {
        // Code executed before push notification is sent
        // Код, выполняемый перед отправкой push-уведомления
        return $params;
    }
    
    public function OnAfterPushNotificationSend($params, $result)
    {
        // Code executed after push notification is sent
        // Код, выполняемый после отправки push-уведомления
        return $result;
    }
    
    public function OnBeforePushNotificationUpdate($params)
    {
        // Code executed before push notification is updated
        // Код, выполняемый перед обновлением push-уведомления
        return $params;
    }
    
    public function OnAfterPushNotificationUpdate($params, $result)
    {
        // Code executed after push notification is updated
        // Код, выполняемый после обновления push-уведомления
        return $result;
    }
    
    public function OnBeforePushNotificationDelete($params)
    {
        // Code executed before push notification is deleted
        // Код, выполняемый перед удалением push-уведомления
        return $params;
    }
    
    public function OnAfterPushNotificationDelete($params, $result)
    {
        // Code executed after push notification is deleted
        // Код, выполняемый после удаления push-уведомления
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CMobilePushNotificationHandler::Register('custom_push_notification', 'CCustomPushNotificationHandler');
```

## REST API | REST API

### Application Management | Управление приложениями

#### Create Application | Создание приложения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\Application::add([
    'NAME' => 'Custom Application',
    'DESCRIPTION' => 'This is a custom application',
    'TYPE' => 'CUSTOM',
    'PLATFORM' => 'ANDROID',
    'VERSION' => '1.0.0',
    'ICON' => $iconId,
    'SCREENSHOTS' => [$screenshotId1, $screenshotId2],
    'PARAMS' => [
        'KEY1' => 'VALUE1',
        'KEY2' => 'VALUE2'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobileApplication::Add([
    'NAME' => 'Custom Application',
    'DESCRIPTION' => 'This is a custom application',
    'TYPE' => 'CUSTOM',
    'PLATFORM' => 'ANDROID',
    'VERSION' => '1.0.0',
    'ICON' => $iconId,
    'SCREENSHOTS' => [$screenshotId1, $screenshotId2],
    'PARAMS' => [
        'KEY1' => 'VALUE1',
        'KEY2' => 'VALUE2'
    ]
]);
```

#### Update Application | Обновление приложения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\Application::update($applicationId, [
    'NAME' => 'Updated Custom Application',
    'DESCRIPTION' => 'This is an updated custom application',
    'VERSION' => '1.0.1',
    'ICON' => $newIconId,
    'SCREENSHOTS' => [$newScreenshotId1, $newScreenshotId2],
    'PARAMS' => [
        'KEY1' => 'NEW_VALUE1',
        'KEY2' => 'NEW_VALUE2'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobileApplication::Update($applicationId, [
    'NAME' => 'Updated Custom Application',
    'DESCRIPTION' => 'This is an updated custom application',
    'VERSION' => '1.0.1',
    'ICON' => $newIconId,
    'SCREENSHOTS' => [$newScreenshotId1, $newScreenshotId2],
    'PARAMS' => [
        'KEY1' => 'NEW_VALUE1',
        'KEY2' => 'NEW_VALUE2'
    ]
]);
```

#### Delete Application | Удаление приложения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\Application::delete($applicationId);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobileApplication::Delete($applicationId);
```

#### Get Application | Получение приложения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$application = \Bitrix\Mobile\Application::getById($applicationId);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$application = CMobileApplication::GetByID($applicationId);
```

#### Install Application | Установка приложения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\Application::install($applicationId, $userId);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobileApplication::Install($applicationId, $userId);
```

#### Uninstall Application | Удаление приложения

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\Application::uninstall($applicationId, $userId);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobileApplication::Uninstall($applicationId, $userId);
```

### Device Management | Управление устройствами

#### Register Device | Регистрация устройства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\Device::register([
    'USER_ID' => $userId,
    'DEVICE_ID' => $deviceId,
    'PLATFORM' => 'ANDROID',
    'VERSION' => '1.0.0',
    'PUSH_TOKEN' => $pushToken,
    'PARAMS' => [
        'KEY1' => 'VALUE1',
        'KEY2' => 'VALUE2'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobileDevice::Register([
    'USER_ID' => $userId,
    'DEVICE_ID' => $deviceId,
    'PLATFORM' => 'ANDROID',
    'VERSION' => '1.0.0',
    'PUSH_TOKEN' => $pushToken,
    'PARAMS' => [
        'KEY1' => 'VALUE1',
        'KEY2' => 'VALUE2'
    ]
]);
```

#### Unregister Device | Отмена регистрации устройства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\Device::unregister($deviceId);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobileDevice::Unregister($deviceId);
```

#### Update Device | Обновление устройства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\Device::update($deviceId, [
    'VERSION' => '1.0.1',
    'PUSH_TOKEN' => $newPushToken,
    'PARAMS' => [
        'KEY1' => 'NEW_VALUE1',
        'KEY2' => 'NEW_VALUE2'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobileDevice::Update($deviceId, [
    'VERSION' => '1.0.1',
    'PUSH_TOKEN' => $newPushToken,
    'PARAMS' => [
        'KEY1' => 'NEW_VALUE1',
        'KEY2' => 'NEW_VALUE2'
    ]
]);
```

#### Get Device | Получение устройства

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$device = \Bitrix\Mobile\Device::getById($deviceId);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$device = CMobileDevice::GetByID($deviceId);
```

### Push Notification Management | Управление push-уведомлениями

#### Send Push Notification | Отправка push-уведомления

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\PushNotification::send([
    'USER_ID' => $userId,
    'DEVICE_ID' => $deviceId,
    'TITLE' => 'Push Notification Title',
    'MESSAGE' => 'This is a push notification message',
    'DATA' => [
        'KEY1' => 'VALUE1',
        'KEY2' => 'VALUE2'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobilePushNotification::Send([
    'USER_ID' => $userId,
    'DEVICE_ID' => $deviceId,
    'TITLE' => 'Push Notification Title',
    'MESSAGE' => 'This is a push notification message',
    'DATA' => [
        'KEY1' => 'VALUE1',
        'KEY2' => 'VALUE2'
    ]
]);
```

#### Update Push Notification | Обновление push-уведомления

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\PushNotification::update($notificationId, [
    'TITLE' => 'Updated Push Notification Title',
    'MESSAGE' => 'This is an updated push notification message',
    'DATA' => [
        'KEY1' => 'NEW_VALUE1',
        'KEY2' => 'NEW_VALUE2'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobilePushNotification::Update($notificationId, [
    'TITLE' => 'Updated Push Notification Title',
    'MESSAGE' => 'This is an updated push notification message',
    'DATA' => [
        'KEY1' => 'NEW_VALUE1',
        'KEY2' => 'NEW_VALUE2'
    ]
]);
```

#### Delete Push Notification | Удаление push-уведомления

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$result = \Bitrix\Mobile\PushNotification::delete($notificationId);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$result = CMobilePushNotification::Delete($notificationId);
```

#### Get Push Notification | Получение push-уведомления

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('mobile')
// Требуется: Bitrix\Main\Loader::includeModule('mobile')
$notification = \Bitrix\Mobile\PushNotification::getById($notificationId);

// Legacy
// Requires: CModule::IncludeModule('mobile')
// Требуется: CModule::IncludeModule('mobile')
$notification = CMobilePushNotification::GetByID($notificationId);
``` 