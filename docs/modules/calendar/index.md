# Calendar Module | Модуль Calendar

## Overview | Обзор

The Calendar module provides functionality for managing events, meetings, and schedules in Bitrix24. It enables users to create, edit, and manage calendar events, set reminders, and coordinate with other users. The module supports various types of events, including personal, group, and company-wide events. | Модуль Calendar предоставляет функциональность для управления событиями, встречами и расписаниями в Bitrix24. Он позволяет пользователям создавать, редактировать и управлять событиями календаря, устанавливать напоминания и координировать действия с другими пользователями. Модуль поддерживает различные типы событий, включая личные, групповые и общеорганизационные события.

## Methods | Методы

### Event Management | Управление событиями

#### Create Event | Создание события

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
$event = \Bitrix\Calendar\Event::add([
    'NAME' => 'Meeting with Client',
    'DESCRIPTION' => 'Discuss project requirements',
    'DATE_FROM' => new \Bitrix\Main\Type\DateTime('2024-03-20 10:00:00'),
    'DATE_TO' => new \Bitrix\Main\Type\DateTime('2024-03-20 11:00:00'),
    'TZ_FROM' => 'Europe/Moscow',
    'TZ_TO' => 'Europe/Moscow',
    'ACCESSIBILITY' => 'busy',
    'IMPORTANCE' => 'normal',
    'EVENT_TYPE' => 'meeting',
    'COLOR' => '#FF0000',
    'REMIND' => [
        [
            'TYPE' => 'min',
            'COUNT' => 15
        ]
    ],
    'ATTENDEES' => [
        [
            'USER_ID' => 1,
            'STATUS' => 'Y'
        ]
    ],
    'LOCATION' => 'Conference Room A',
    'CALENDAR_TYPE' => 'user',
    'OWNER_ID' => $USER->GetID(),
    'CREATED_BY' => $USER->GetID()
]);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
$event = CCalendarEvent::Add([
    'NAME' => 'Meeting with Client',
    'DESCRIPTION' => 'Discuss project requirements',
    'DATE_FROM' => '2024-03-20 10:00:00',
    'DATE_TO' => '2024-03-20 11:00:00',
    'TZ_FROM' => 'Europe/Moscow',
    'TZ_TO' => 'Europe/Moscow',
    'ACCESSIBILITY' => 'busy',
    'IMPORTANCE' => 'normal',
    'EVENT_TYPE' => 'meeting',
    'COLOR' => '#FF0000',
    'REMIND' => [
        [
            'TYPE' => 'min',
            'COUNT' => 15
        ]
    ],
    'ATTENDEES' => [
        [
            'USER_ID' => 1,
            'STATUS' => 'Y'
        ]
    ],
    'LOCATION' => 'Conference Room A',
    'CALENDAR_TYPE' => 'user',
    'OWNER_ID' => $USER->GetID(),
    'CREATED_BY' => $USER->GetID()
]);
```

#### Get Event | Получение события

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
$event = \Bitrix\Calendar\Event::getById($eventId);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
$event = CCalendarEvent::GetByID($eventId);
```

#### Update Event | Обновление события

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
$result = \Bitrix\Calendar\Event::update($eventId, [
    'NAME' => 'Updated Meeting with Client',
    'DESCRIPTION' => 'Updated project requirements discussion',
    'DATE_FROM' => new \Bitrix\Main\Type\DateTime('2024-03-20 11:00:00'),
    'DATE_TO' => new \Bitrix\Main\Type\DateTime('2024-03-20 12:00:00'),
    'LOCATION' => 'Conference Room B'
]);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
$result = CCalendarEvent::Update($eventId, [
    'NAME' => 'Updated Meeting with Client',
    'DESCRIPTION' => 'Updated project requirements discussion',
    'DATE_FROM' => '2024-03-20 11:00:00',
    'DATE_TO' => '2024-03-20 12:00:00',
    'LOCATION' => 'Conference Room B'
]);
```

#### Delete Event | Удаление события

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
$result = \Bitrix\Calendar\Event::delete($eventId);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
$result = CCalendarEvent::Delete($eventId);
```

### Section Management | Управление разделами

#### Create Section | Создание раздела

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
$section = \Bitrix\Calendar\Section::add([
    'NAME' => 'Work Meetings',
    'DESCRIPTION' => 'Section for work-related meetings',
    'COLOR' => '#00FF00',
    'CALENDAR_TYPE' => 'user',
    'OWNER_ID' => $USER->GetID(),
    'CREATED_BY' => $USER->GetID()
]);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
$section = CCalendarSection::Add([
    'NAME' => 'Work Meetings',
    'DESCRIPTION' => 'Section for work-related meetings',
    'COLOR' => '#00FF00',
    'CALENDAR_TYPE' => 'user',
    'OWNER_ID' => $USER->GetID(),
    'CREATED_BY' => $USER->GetID()
]);
```

#### Get Section | Получение раздела

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
$section = \Bitrix\Calendar\Section::getById($sectionId);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
$section = CCalendarSection::GetByID($sectionId);
```

#### Update Section | Обновление раздела

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
$result = \Bitrix\Calendar\Section::update($sectionId, [
    'NAME' => 'Updated Work Meetings',
    'DESCRIPTION' => 'Updated section for work-related meetings',
    'COLOR' => '#0000FF'
]);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
$result = CCalendarSection::Update($sectionId, [
    'NAME' => 'Updated Work Meetings',
    'DESCRIPTION' => 'Updated section for work-related meetings',
    'COLOR' => '#0000FF'
]);
```

#### Delete Section | Удаление раздела

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
$result = \Bitrix\Calendar\Section::delete($sectionId);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
$result = CCalendarSection::Delete($sectionId);
```

### Access Management | Управление доступом

#### Set Event Access | Установка доступа к событию

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
$result = \Bitrix\Calendar\Access::setEventAccess($eventId, [
    'ACCESS' => 'private',
    'ATTENDEES' => [
        [
            'USER_ID' => 1,
            'STATUS' => 'Y'
        ],
        [
            'USER_ID' => 2,
            'STATUS' => 'N'
        ]
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
$result = CCalendarEvent::SetAccess($eventId, [
    'ACCESS' => 'private',
    'ATTENDEES' => [
        [
            'USER_ID' => 1,
            'STATUS' => 'Y'
        ],
        [
            'USER_ID' => 2,
            'STATUS' => 'N'
        ]
    ]
]);
```

#### Set Section Access | Установка доступа к разделу

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
$result = \Bitrix\Calendar\Access::setSectionAccess($sectionId, [
    'ACCESS' => 'private',
    'USERS' => [1, 2, 3]
]);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
$result = CCalendarSection::SetAccess($sectionId, [
    'ACCESS' => 'private',
    'USERS' => [1, 2, 3]
]);
```

### Meeting Management | Управление встречами

#### Create Meeting | Создание встречи

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
$meeting = \Bitrix\Calendar\Meeting::add([
    'NAME' => 'Project Kickoff Meeting',
    'DESCRIPTION' => 'Initial project discussion',
    'DATE_FROM' => new \Bitrix\Main\Type\DateTime('2024-03-21 14:00:00'),
    'DATE_TO' => new \Bitrix\Main\Type\DateTime('2024-03-21 15:00:00'),
    'TZ_FROM' => 'Europe/Moscow',
    'TZ_TO' => 'Europe/Moscow',
    'ACCESSIBILITY' => 'busy',
    'IMPORTANCE' => 'high',
    'EVENT_TYPE' => 'meeting',
    'COLOR' => '#FF0000',
    'REMIND' => [
        [
            'TYPE' => 'min',
            'COUNT' => 30
        ]
    ],
    'ATTENDEES' => [
        [
            'USER_ID' => 1,
            'STATUS' => 'Y'
        ],
        [
            'USER_ID' => 2,
            'STATUS' => 'N'
        ]
    ],
    'LOCATION' => 'Conference Room A',
    'CALENDAR_TYPE' => 'group',
    'OWNER_ID' => $USER->GetID(),
    'CREATED_BY' => $USER->GetID(),
    'MEETING_HOST' => $USER->GetID(),
    'MEETING_STATUS' => 'N'
]);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
$meeting = CCalendarEvent::Add([
    'NAME' => 'Project Kickoff Meeting',
    'DESCRIPTION' => 'Initial project discussion',
    'DATE_FROM' => '2024-03-21 14:00:00',
    'DATE_TO' => '2024-03-21 15:00:00',
    'TZ_FROM' => 'Europe/Moscow',
    'TZ_TO' => 'Europe/Moscow',
    'ACCESSIBILITY' => 'busy',
    'IMPORTANCE' => 'high',
    'EVENT_TYPE' => 'meeting',
    'COLOR' => '#FF0000',
    'REMIND' => [
        [
            'TYPE' => 'min',
            'COUNT' => 30
        ]
    ],
    'ATTENDEES' => [
        [
            'USER_ID' => 1,
            'STATUS' => 'Y'
        ],
        [
            'USER_ID' => 2,
            'STATUS' => 'N'
        ]
    ],
    'LOCATION' => 'Conference Room A',
    'CALENDAR_TYPE' => 'group',
    'OWNER_ID' => $USER->GetID(),
    'CREATED_BY' => $USER->GetID(),
    'MEETING_HOST' => $USER->GetID(),
    'MEETING_STATUS' => 'N'
]);
```

#### Update Meeting Status | Обновление статуса встречи

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
$result = \Bitrix\Calendar\Meeting::updateStatus($meetingId, [
    'USER_ID' => $userId,
    'STATUS' => 'Y'
]);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
$result = CCalendarEvent::UpdateMeetingStatus($meetingId, [
    'USER_ID' => $userId,
    'STATUS' => 'Y'
]);
```

### Recurring Events | Повторяющиеся события

#### Create Recurring Event | Создание повторяющегося события

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
$event = \Bitrix\Calendar\Event::add([
    'NAME' => 'Weekly Team Meeting',
    'DESCRIPTION' => 'Regular team sync',
    'DATE_FROM' => new \Bitrix\Main\Type\DateTime('2024-03-22 10:00:00'),
    'DATE_TO' => new \Bitrix\Main\Type\DateTime('2024-03-22 11:00:00'),
    'TZ_FROM' => 'Europe/Moscow',
    'TZ_TO' => 'Europe/Moscow',
    'ACCESSIBILITY' => 'busy',
    'IMPORTANCE' => 'normal',
    'EVENT_TYPE' => 'meeting',
    'COLOR' => '#FF0000',
    'REMIND' => [
        [
            'TYPE' => 'min',
            'COUNT' => 15
        ]
    ],
    'ATTENDEES' => [
        [
            'USER_ID' => 1,
            'STATUS' => 'Y'
        ]
    ],
    'LOCATION' => 'Conference Room A',
    'CALENDAR_TYPE' => 'user',
    'OWNER_ID' => $USER->GetID(),
    'CREATED_BY' => $USER->GetID(),
    'RRULE' => [
        'FREQ' => 'WEEKLY',
        'INTERVAL' => 1,
        'BYDAY' => ['MO'],
        'COUNT' => 12,
        'UNTIL' => new \Bitrix\Main\Type\DateTime('2024-06-22 11:00:00')
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
$event = CCalendarEvent::Add([
    'NAME' => 'Weekly Team Meeting',
    'DESCRIPTION' => 'Regular team sync',
    'DATE_FROM' => '2024-03-22 10:00:00',
    'DATE_TO' => '2024-03-22 11:00:00',
    'TZ_FROM' => 'Europe/Moscow',
    'TZ_TO' => 'Europe/Moscow',
    'ACCESSIBILITY' => 'busy',
    'IMPORTANCE' => 'normal',
    'EVENT_TYPE' => 'meeting',
    'COLOR' => '#FF0000',
    'REMIND' => [
        [
            'TYPE' => 'min',
            'COUNT' => 15
        ]
    ],
    'ATTENDEES' => [
        [
            'USER_ID' => 1,
            'STATUS' => 'Y'
        ]
    ],
    'LOCATION' => 'Conference Room A',
    'CALENDAR_TYPE' => 'user',
    'OWNER_ID' => $USER->GetID(),
    'CREATED_BY' => $USER->GetID(),
    'RRULE' => [
        'FREQ' => 'WEEKLY',
        'INTERVAL' => 1,
        'BYDAY' => ['MO'],
        'COUNT' => 12,
        'UNTIL' => '2024-06-22 11:00:00'
    ]
]);
```

## Handlers | Обработчики

### Event Handlers | Обработчики событий

#### Event Handler | Обработчик событий

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
class CustomEventHandler extends \Bitrix\Calendar\Event\Handler
{
    public function onBeforeEventCreate($params)
    {
        // Code executed before event is created
        // Код, выполняемый перед созданием события
        return $params;
    }
    
    public function onAfterEventCreate($params, $result)
    {
        // Code executed after event is created
        // Код, выполняемый после создания события
        return $result;
    }
    
    public function onBeforeEventUpdate($params)
    {
        // Code executed before event is updated
        // Код, выполняемый перед обновлением события
        return $params;
    }
    
    public function onAfterEventUpdate($params, $result)
    {
        // Code executed after event is updated
        // Код, выполняемый после обновления события
        return $result;
    }
    
    public function onBeforeEventDelete($params)
    {
        // Code executed before event is deleted
        // Код, выполняемый перед удалением события
        return $params;
    }
    
    public function onAfterEventDelete($params, $result)
    {
        // Code executed after event is deleted
        // Код, выполняемый после удаления события
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Calendar\Event\Handler::register('custom_event', CustomEventHandler::class);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
class CCustomEventHandler extends CCalendarEvent
{
    public function OnBeforeEventCreate($params)
    {
        // Code executed before event is created
        // Код, выполняемый перед созданием события
        return $params;
    }
    
    public function OnAfterEventCreate($params, $result)
    {
        // Code executed after event is created
        // Код, выполняемый после создания события
        return $result;
    }
    
    public function OnBeforeEventUpdate($params)
    {
        // Code executed before event is updated
        // Код, выполняемый перед обновлением события
        return $params;
    }
    
    public function OnAfterEventUpdate($params, $result)
    {
        // Code executed after event is updated
        // Код, выполняемый после обновления события
        return $result;
    }
    
    public function OnBeforeEventDelete($params)
    {
        // Code executed before event is deleted
        // Код, выполняемый перед удалением события
        return $params;
    }
    
    public function OnAfterEventDelete($params, $result)
    {
        // Code executed after event is deleted
        // Код, выполняемый после удаления события
        return $result;
    }
}

// Register handler
// Регистрация обработчика
AddEventHandler('calendar', 'OnBeforeEventCreate', ['CCustomEventHandler', 'OnBeforeEventCreate']);
AddEventHandler('calendar', 'OnAfterEventCreate', ['CCustomEventHandler', 'OnAfterEventCreate']);
AddEventHandler('calendar', 'OnBeforeEventUpdate', ['CCustomEventHandler', 'OnBeforeEventUpdate']);
AddEventHandler('calendar', 'OnAfterEventUpdate', ['CCustomEventHandler', 'OnAfterEventUpdate']);
AddEventHandler('calendar', 'OnBeforeEventDelete', ['CCustomEventHandler', 'OnBeforeEventDelete']);
AddEventHandler('calendar', 'OnAfterEventDelete', ['CCustomEventHandler', 'OnAfterEventDelete']);
```

### Section Handlers | Обработчики разделов

#### Section Handler | Обработчик разделов

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
class CustomSectionHandler extends \Bitrix\Calendar\Section\Handler
{
    public function onBeforeSectionCreate($params)
    {
        // Code executed before section is created
        // Код, выполняемый перед созданием раздела
        return $params;
    }
    
    public function onAfterSectionCreate($params, $result)
    {
        // Code executed after section is created
        // Код, выполняемый после создания раздела
        return $result;
    }
    
    public function onBeforeSectionUpdate($params)
    {
        // Code executed before section is updated
        // Код, выполняемый перед обновлением раздела
        return $params;
    }
    
    public function onAfterSectionUpdate($params, $result)
    {
        // Code executed after section is updated
        // Код, выполняемый после обновления раздела
        return $result;
    }
    
    public function onBeforeSectionDelete($params)
    {
        // Code executed before section is deleted
        // Код, выполняемый перед удалением раздела
        return $params;
    }
    
    public function onAfterSectionDelete($params, $result)
    {
        // Code executed after section is deleted
        // Код, выполняемый после удаления раздела
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Calendar\Section\Handler::register('custom_section', CustomSectionHandler::class);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
class CCustomSectionHandler extends CCalendarSection
{
    public function OnBeforeSectionCreate($params)
    {
        // Code executed before section is created
        // Код, выполняемый перед созданием раздела
        return $params;
    }
    
    public function OnAfterSectionCreate($params, $result)
    {
        // Code executed after section is created
        // Код, выполняемый после создания раздела
        return $result;
    }
    
    public function OnBeforeSectionUpdate($params)
    {
        // Code executed before section is updated
        // Код, выполняемый перед обновлением раздела
        return $params;
    }
    
    public function OnAfterSectionUpdate($params, $result)
    {
        // Code executed after section is updated
        // Код, выполняемый после обновления раздела
        return $result;
    }
    
    public function OnBeforeSectionDelete($params)
    {
        // Code executed before section is deleted
        // Код, выполняемый перед удалением раздела
        return $params;
    }
    
    public function OnAfterSectionDelete($params, $result)
    {
        // Code executed after section is deleted
        // Код, выполняемый после удаления раздела
        return $result;
    }
}

// Register handler
// Регистрация обработчика
AddEventHandler('calendar', 'OnBeforeSectionCreate', ['CCustomSectionHandler', 'OnBeforeSectionCreate']);
AddEventHandler('calendar', 'OnAfterSectionCreate', ['CCustomSectionHandler', 'OnAfterSectionCreate']);
AddEventHandler('calendar', 'OnBeforeSectionUpdate', ['CCustomSectionHandler', 'OnBeforeSectionUpdate']);
AddEventHandler('calendar', 'OnAfterSectionUpdate', ['CCustomSectionHandler', 'OnAfterSectionUpdate']);
AddEventHandler('calendar', 'OnBeforeSectionDelete', ['CCustomSectionHandler', 'OnBeforeSectionDelete']);
AddEventHandler('calendar', 'OnAfterSectionDelete', ['CCustomSectionHandler', 'OnAfterSectionDelete']);
```

### Meeting Handlers | Обработчики встреч

#### Meeting Handler | Обработчик встреч

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('calendar')
// Требуется: Bitrix\Main\Loader::includeModule('calendar')
class CustomMeetingHandler extends \Bitrix\Calendar\Meeting\Handler
{
    public function onBeforeMeetingCreate($params)
    {
        // Code executed before meeting is created
        // Код, выполняемый перед созданием встречи
        return $params;
    }
    
    public function onAfterMeetingCreate($params, $result)
    {
        // Code executed after meeting is created
        // Код, выполняемый после создания встречи
        return $result;
    }
    
    public function onBeforeMeetingUpdate($params)
    {
        // Code executed before meeting is updated
        // Код, выполняемый перед обновлением встречи
        return $params;
    }
    
    public function onAfterMeetingUpdate($params, $result)
    {
        // Code executed after meeting is updated
        // Код, выполняемый после обновления встречи
        return $result;
    }
    
    public function onBeforeMeetingDelete($params)
    {
        // Code executed before meeting is deleted
        // Код, выполняемый перед удалением встречи
        return $params;
    }
    
    public function onAfterMeetingDelete($params, $result)
    {
        // Code executed after meeting is deleted
        // Код, выполняемый после удаления встречи
        return $result;
    }
    
    public function onBeforeMeetingStatusUpdate($params)
    {
        // Code executed before meeting status is updated
        // Код, выполняемый перед обновлением статуса встречи
        return $params;
    }
    
    public function onAfterMeetingStatusUpdate($params, $result)
    {
        // Code executed after meeting status is updated
        // Код, выполняемый после обновления статуса встречи
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Calendar\Meeting\Handler::register('custom_meeting', CustomMeetingHandler::class);

// Legacy
// Requires: CModule::IncludeModule('calendar')
// Требуется: CModule::IncludeModule('calendar')
class CCustomMeetingHandler extends CCalendarEvent
{
    public function OnBeforeMeetingCreate($params)
    {
        // Code executed before meeting is created
        // Код, выполняемый перед созданием встречи
        return $params;
    }
    
    public function OnAfterMeetingCreate($params, $result)
    {
        // Code executed after meeting is created
        // Код, выполняемый после создания встречи
        return $result;
    }
    
    public function OnBeforeMeetingUpdate($params)
    {
        // Code executed before meeting is updated
        // Код, выполняемый перед обновлением встречи
        return $params;
    }
    
    public function OnAfterMeetingUpdate($params, $result)
    {
        // Code executed after meeting is updated
        // Код, выполняемый после обновления встречи
        return $result;
    }
    
    public function OnBeforeMeetingDelete($params)
    {
        // Code executed before meeting is deleted
        // Код, выполняемый перед удалением встречи
        return $params;
    }
    
    public function OnAfterMeetingDelete($params, $result)
    {
        // Code executed after meeting is deleted
        // Код, выполняемый после удаления встречи
        return $result;
    }
    
    public function OnBeforeMeetingStatusUpdate($params)
    {
        // Code executed before meeting status is updated
        // Код, выполняемый перед обновлением статуса встречи
        return $params;
    }
    
    public function OnAfterMeetingStatusUpdate($params, $result)
    {
        // Code executed after meeting status is updated
        // Код, выполняемый после обновления статуса встречи
        return $result;
    }
}

// Register handler
// Регистрация обработчика
AddEventHandler('calendar', 'OnBeforeMeetingCreate', ['CCustomMeetingHandler', 'OnBeforeMeetingCreate']);
AddEventHandler('calendar', 'OnAfterMeetingCreate', ['CCustomMeetingHandler', 'OnAfterMeetingCreate']);
AddEventHandler('calendar', 'OnBeforeMeetingUpdate', ['CCustomMeetingHandler', 'OnBeforeMeetingUpdate']);
AddEventHandler('calendar', 'OnAfterMeetingUpdate', ['CCustomMeetingHandler', 'OnAfterMeetingUpdate']);
AddEventHandler('calendar', 'OnBeforeMeetingDelete', ['CCustomMeetingHandler', 'OnBeforeMeetingDelete']);
AddEventHandler('calendar', 'OnAfterMeetingDelete', ['CCustomMeetingHandler', 'OnAfterMeetingDelete']);
AddEventHandler('calendar', 'OnBeforeMeetingStatusUpdate', ['CCustomMeetingHandler', 'OnBeforeMeetingStatusUpdate']);
AddEventHandler('calendar', 'OnAfterMeetingStatusUpdate', ['CCustomMeetingHandler', 'OnAfterMeetingStatusUpdate']);
``` 