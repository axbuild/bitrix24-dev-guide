# Socialnetwork Module | Модуль Socialnetwork

## Overview | Обзор

The Socialnetwork module provides functionality for social collaboration in Bitrix24. It enables users to create and manage workgroups, share information, communicate with colleagues, and collaborate on projects. The module includes features for activity streams, workgroups, tasks, and social interactions. | Модуль Socialnetwork предоставляет функциональность для социального взаимодействия в Bitrix24. Он позволяет пользователям создавать и управлять рабочими группами, делиться информацией, общаться с коллегами и сотрудничать над проектами. Модуль включает функции для лент активности, рабочих групп, задач и социального взаимодействия.

## Methods | Методы

### Group Management | Управление группами

#### Create Group | Создание группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$group = \Bitrix\Socialnetwork\Group::add([
    'NAME' => 'My Group',
    'DESCRIPTION' => 'Group description',
    'INITIATE_PERMS' => 'A', // All users can invite
    'SPAM_PERMS' => 'A', // All users can post
    'VISIBLE' => 'Y',
    'OPENED' => 'Y',
    'CLOSED' => 'N',
    'SUBJECT_ID' => 1,
    'OWNER_ID' => $USER->GetID(),
    'KEYWORDS' => 'keywords',
    'IMAGE_ID' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$group = CSocNetGroup::Add([
    'NAME' => 'My Group',
    'DESCRIPTION' => 'Group description',
    'INITIATE_PERMS' => 'A', // All users can invite
    'SPAM_PERMS' => 'A', // All users can post
    'VISIBLE' => 'Y',
    'OPENED' => 'Y',
    'CLOSED' => 'N',
    'SUBJECT_ID' => 1,
    'OWNER_ID' => $USER->GetID(),
    'KEYWORDS' => 'keywords',
    'IMAGE_ID' => 0
]);
```

#### Get Group | Получение группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$group = \Bitrix\Socialnetwork\Group::getById($groupId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$group = CSocNetGroup::GetByID($groupId);
```

#### Update Group | Обновление группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$group = \Bitrix\Socialnetwork\Group::getById($groupId);
$result = $group->update([
    'NAME' => 'Updated Group Name',
    'DESCRIPTION' => 'Updated description'
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetGroup::Update($groupId, [
    'NAME' => 'Updated Group Name',
    'DESCRIPTION' => 'Updated description'
]);
```

#### Delete Group | Удаление группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$group = \Bitrix\Socialnetwork\Group::getById($groupId);
$result = $group->delete();

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetGroup::Delete($groupId);
```

### User Relations | Отношения пользователей

#### Follow User | Подписаться на пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\Follow::add([
    'USER_ID' => $USER->GetID(),
    'FOLLOW_USER_ID' => $followUserId
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetUserRelations::SetRelation($USER->GetID(), $followUserId, SONET_RELATIONS_FOLLOW);
```

#### Unfollow User | Отписаться от пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\Follow::delete([
    'USER_ID' => $USER->GetID(),
    'FOLLOW_USER_ID' => $followUserId
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetUserRelations::DeleteRelation($USER->GetID(), $followUserId, SONET_RELATIONS_FOLLOW);
```

#### Get Followers | Получение подписчиков

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$followers = \Bitrix\Socialnetwork\Follow::getFollowers($userId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$followers = CSocNetUserRelations::GetFollowers($userId);
```

### Group Membership | Членство в группах

#### Join Group | Присоединиться к группе

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\GroupMember::add([
    'GROUP_ID' => $groupId,
    'USER_ID' => $USER->GetID(),
    'ROLE' => 'U' // User role
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetUserToGroup::Add([
    'GROUP_ID' => $groupId,
    'USER_ID' => $USER->GetID(),
    'ROLE' => 'U' // User role
]);
```

#### Leave Group | Покинуть группу

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\GroupMember::delete([
    'GROUP_ID' => $groupId,
    'USER_ID' => $USER->GetID()
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetUserToGroup::Delete($USER->GetID(), $groupId);
```

#### Get Group Members | Получение участников группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$members = \Bitrix\Socialnetwork\GroupMember::getList([
    'GROUP_ID' => $groupId,
    'ROLE' => 'U' // User role
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$members = CSocNetUserToGroup::GetList(
    ['USER_ID' => 'ASC'],
    ['GROUP_ID' => $groupId, 'ROLE' => 'U']
);
```

### Activity Stream | Лента активности

#### Add Activity | Добавление активности

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$activity = \Bitrix\Socialnetwork\Log::add([
    'ENTITY_TYPE' => 'group',
    'ENTITY_ID' => $groupId,
    'EVENT_ID' => 'group_join',
    'USER_ID' => $USER->GetID(),
    'TITLE' => 'User joined the group',
    'MESSAGE' => 'User has joined the group',
    'TEXT_MESSAGE' => 'User has joined the group',
    'URL' => '/groups/' . $groupId . '/',
    'MODULE_ID' => 'socialnetwork'
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$activity = CSocNetLog::Add([
    'ENTITY_TYPE' => 'group',
    'ENTITY_ID' => $groupId,
    'EVENT_ID' => 'group_join',
    'USER_ID' => $USER->GetID(),
    'TITLE' => 'User joined the group',
    'MESSAGE' => 'User has joined the group',
    'TEXT_MESSAGE' => 'User has joined the group',
    'URL' => '/groups/' . $groupId . '/',
    'MODULE_ID' => 'socialnetwork'
]);
```

#### Get Activity Stream | Получение ленты активности

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$activities = \Bitrix\Socialnetwork\Log::getList([
    'USER_ID' => $USER->GetID(),
    'ENTITY_TYPE' => ['group', 'user'],
    'EVENT_ID' => ['group_join', 'user_follow'],
    'LIMIT' => 50
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$activities = CSocNetLog::GetList(
    ['DATE_CREATE' => 'DESC'],
    ['USER_ID' => $USER->GetID(), 'ENTITY_TYPE' => ['group', 'user']],
    false,
    ['nTopCount' => 50],
    ['ID', 'ENTITY_TYPE', 'ENTITY_ID', 'EVENT_ID', 'USER_ID', 'TITLE', 'MESSAGE', 'TEXT_MESSAGE', 'URL', 'MODULE_ID']
);
```

### Comments | Комментарии

#### Add Comment | Добавление комментария

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$comment = \Bitrix\Socialnetwork\Comment::add([
    'ENTITY_TYPE' => 'group',
    'ENTITY_ID' => $groupId,
    'EVENT_ID' => 'group_join',
    'USER_ID' => $USER->GetID(),
    'MESSAGE' => 'This is a comment',
    'SOURCE_ID' => $activityId
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$comment = CSocNetLogComments::Add([
    'ENTITY_TYPE' => 'group',
    'ENTITY_ID' => $groupId,
    'EVENT_ID' => 'group_join',
    'USER_ID' => $USER->GetID(),
    'MESSAGE' => 'This is a comment',
    'SOURCE_ID' => $activityId
]);
```

#### Get Comments | Получение комментариев

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$comments = \Bitrix\Socialnetwork\Comment::getList([
    'ENTITY_TYPE' => 'group',
    'ENTITY_ID' => $groupId,
    'EVENT_ID' => 'group_join',
    'SOURCE_ID' => $activityId,
    'LIMIT' => 50
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$comments = CSocNetLogComments::GetList(
    ['DATE_CREATE' => 'DESC'],
    ['ENTITY_TYPE' => 'group', 'ENTITY_ID' => $groupId, 'EVENT_ID' => 'group_join', 'SOURCE_ID' => $activityId],
    false,
    ['nTopCount' => 50],
    ['ID', 'ENTITY_TYPE', 'ENTITY_ID', 'EVENT_ID', 'USER_ID', 'MESSAGE', 'SOURCE_ID']
);
```

### Workgroups | Рабочие группы

#### Create Workgroup | Создание рабочей группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$workgroup = \Bitrix\Socialnetwork\Workgroup::add([
    'NAME' => 'My Workgroup',
    'DESCRIPTION' => 'Workgroup description',
    'INITIATE_PERMS' => 'A', // All users can invite
    'SPAM_PERMS' => 'A', // All users can post
    'VISIBLE' => 'Y',
    'OPENED' => 'Y',
    'CLOSED' => 'N',
    'SUBJECT_ID' => 1,
    'OWNER_ID' => $USER->GetID(),
    'KEYWORDS' => 'keywords',
    'IMAGE_ID' => 0,
    'PROJECT' => 'Y' // This is a project workgroup
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$workgroup = CSocNetGroup::Add([
    'NAME' => 'My Workgroup',
    'DESCRIPTION' => 'Workgroup description',
    'INITIATE_PERMS' => 'A', // All users can invite
    'SPAM_PERMS' => 'A', // All users can post
    'VISIBLE' => 'Y',
    'OPENED' => 'Y',
    'CLOSED' => 'N',
    'SUBJECT_ID' => 1,
    'OWNER_ID' => $USER->GetID(),
    'KEYWORDS' => 'keywords',
    'IMAGE_ID' => 0,
    'PROJECT' => 'Y' // This is a project workgroup
]);
```

#### Get Workgroup | Получение рабочей группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$workgroup = \Bitrix\Socialnetwork\Workgroup::getById($workgroupId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$workgroup = CSocNetGroup::GetByID($workgroupId);
```

#### Get User Workgroups | Получение рабочих групп пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$workgroups = \Bitrix\Socialnetwork\Workgroup::getUserWorkgroups($USER->GetID());

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$workgroups = CSocNetUserToGroup::GetList(
    ['GROUP_NAME' => 'ASC'],
    ['USER_ID' => $USER->GetID(), 'PROJECT' => 'Y'],
    false,
    false,
    ['GROUP_ID', 'GROUP_NAME', 'GROUP_DESCRIPTION', 'GROUP_IMAGE_ID']
);
```

### Tasks Integration | Интеграция с задачами

#### Add Task to Workgroup | Добавление задачи в рабочую группу

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Requires: Bitrix\Main\Loader::includeModule('tasks')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('tasks')
$task = \Bitrix\Tasks\Task::add([
    'TITLE' => 'Task Title',
    'DESCRIPTION' => 'Task Description',
    'RESPONSIBLE_ID' => $responsibleId,
    'CREATED_BY' => $USER->GetID(),
    'GROUP_ID' => $workgroupId,
    'STATUS' => 2, // In Progress
    'PRIORITY' => 1, // Normal
    'DEADLINE' => new \Bitrix\Main\Type\DateTime('2023-12-31 23:59:59')
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Requires: CModule::IncludeModule('tasks')
// Требуется: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('tasks')
$task = CTasks::Add([
    'TITLE' => 'Task Title',
    'DESCRIPTION' => 'Task Description',
    'RESPONSIBLE_ID' => $responsibleId,
    'CREATED_BY' => $USER->GetID(),
    'GROUP_ID' => $workgroupId,
    'STATUS' => 2, // In Progress
    'PRIORITY' => 1, // Normal
    'DEADLINE' => '2023-12-31 23:59:59'
]);
```

#### Get Workgroup Tasks | Получение задач рабочей группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Requires: Bitrix\Main\Loader::includeModule('tasks')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('tasks')
$tasks = \Bitrix\Tasks\Task::getList([
    'GROUP_ID' => $workgroupId,
    'STATUS' => [1, 2, 3], // New, In Progress, Waiting
    'LIMIT' => 50
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Requires: CModule::IncludeModule('tasks')
// Требуется: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('tasks')
$tasks = CTasks::GetList(
    ['DEADLINE' => 'ASC'],
    ['GROUP_ID' => $workgroupId, 'STATUS' => [1, 2, 3]],
    false,
    ['nTopCount' => 50],
    ['ID', 'TITLE', 'DESCRIPTION', 'STATUS', 'PRIORITY', 'DEADLINE', 'RESPONSIBLE_ID', 'CREATED_BY']
);
```

## Handlers | Обработчики

### Workgroup Handlers | Обработчики рабочих групп

#### Workgroup Handler | Обработчик рабочей группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
class CustomWorkgroupHandler extends \Bitrix\Socialnetwork\Workgroup\Handler
{
    public function onBeforeWorkgroupCreate($params)
    {
        // Code executed before workgroup is created
        // Код, выполняемый перед созданием рабочей группы
        return $params;
    }
    
    public function onAfterWorkgroupCreate($params, $result)
    {
        // Code executed after workgroup is created
        // Код, выполняемый после создания рабочей группы
        return $result;
    }
    
    public function onBeforeWorkgroupUpdate($params)
    {
        // Code executed before workgroup is updated
        // Код, выполняемый перед обновлением рабочей группы
        return $params;
    }
    
    public function onAfterWorkgroupUpdate($params, $result)
    {
        // Code executed after workgroup is updated
        // Код, выполняемый после обновления рабочей группы
        return $result;
    }
    
    public function onBeforeWorkgroupDelete($params)
    {
        // Code executed before workgroup is deleted
        // Код, выполняемый перед удалением рабочей группы
        return $params;
    }
    
    public function onAfterWorkgroupDelete($params, $result)
    {
        // Code executed after workgroup is deleted
        // Код, выполняемый после удаления рабочей группы
        return $result;
    }
    
    public function onBeforeWorkgroupJoin($params)
    {
        // Code executed before user joins workgroup
        // Код, выполняемый перед присоединением пользователя к рабочей группе
        return $params;
    }
    
    public function onAfterWorkgroupJoin($params, $result)
    {
        // Code executed after user joins workgroup
        // Код, выполняемый после присоединения пользователя к рабочей группе
        return $result;
    }
    
    public function onBeforeWorkgroupLeave($params)
    {
        // Code executed before user leaves workgroup
        // Код, выполняемый перед выходом пользователя из рабочей группы
        return $params;
    }
    
    public function onAfterWorkgroupLeave($params, $result)
    {
        // Code executed after user leaves workgroup
        // Код, выполняемый после выхода пользователя из рабочей группы
        return $result;
    }
    
    public function onBeforeWorkgroupInvite($params)
    {
        // Code executed before user is invited to workgroup
        // Код, выполняемый перед приглашением пользователя в рабочую группу
        return $params;
    }
    
    public function onAfterWorkgroupInvite($params, $result)
    {
        // Code executed after user is invited to workgroup
        // Код, выполняемый после приглашения пользователя в рабочую группу
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Socialnetwork\Workgroup\Handler::register('custom_workgroup', CustomWorkgroupHandler::class);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
class CCustomWorkgroupHandler extends CSocialnetworkWorkgroupHandler
{
    public function OnBeforeWorkgroupCreate($params)
    {
        // Code executed before workgroup is created
        // Код, выполняемый перед созданием рабочей группы
        return $params;
    }
    
    public function OnAfterWorkgroupCreate($params, $result)
    {
        // Code executed after workgroup is created
        // Код, выполняемый после создания рабочей группы
        return $result;
    }
    
    public function OnBeforeWorkgroupUpdate($params)
    {
        // Code executed before workgroup is updated
        // Код, выполняемый перед обновлением рабочей группы
        return $params;
    }
    
    public function OnAfterWorkgroupUpdate($params, $result)
    {
        // Code executed after workgroup is updated
        // Код, выполняемый после обновления рабочей группы
        return $result;
    }
    
    public function OnBeforeWorkgroupDelete($params)
    {
        // Code executed before workgroup is deleted
        // Код, выполняемый перед удалением рабочей группы
        return $params;
    }
    
    public function OnAfterWorkgroupDelete($params, $result)
    {
        // Code executed after workgroup is deleted
        // Код, выполняемый после удаления рабочей группы
        return $result;
    }
    
    public function OnBeforeWorkgroupJoin($params)
    {
        // Code executed before user joins workgroup
        // Код, выполняемый перед присоединением пользователя к рабочей группе
        return $params;
    }
    
    public function OnAfterWorkgroupJoin($params, $result)
    {
        // Code executed after user joins workgroup
        // Код, выполняемый после присоединения пользователя к рабочей группе
        return $result;
    }
    
    public function OnBeforeWorkgroupLeave($params)
    {
        // Code executed before user leaves workgroup
        // Код, выполняемый перед выходом пользователя из рабочей группы
        return $params;
    }
    
    public function OnAfterWorkgroupLeave($params, $result)
    {
        // Code executed after user leaves workgroup
        // Код, выполняемый после выхода пользователя из рабочей группы
        return $result;
    }
    
    public function OnBeforeWorkgroupInvite($params)
    {
        // Code executed before user is invited to workgroup
        // Код, выполняемый перед приглашением пользователя в рабочую группу
        return $params;
    }
    
    public function OnAfterWorkgroupInvite($params, $result)
    {
        // Code executed after user is invited to workgroup
        // Код, выполняемый после приглашения пользователя в рабочую группу
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CSocialnetworkWorkgroupHandler::Register('custom_workgroup', 'CCustomWorkgroupHandler');
```

### Activity Stream Handlers | Обработчики лент активности

#### Activity Stream Handler | Обработчик ленты активности

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
class CustomActivityStreamHandler extends \Bitrix\Socialnetwork\ActivityStream\Handler
{
    public function onBeforeActivityCreate($params)
    {
        // Code executed before activity is created
        // Код, выполняемый перед созданием активности
        return $params;
    }
    
    public function onAfterActivityCreate($params, $result)
    {
        // Code executed after activity is created
        // Код, выполняемый после создания активности
        return $result;
    }
    
    public function onBeforeActivityUpdate($params)
    {
        // Code executed before activity is updated
        // Код, выполняемый перед обновлением активности
        return $params;
    }
    
    public function onAfterActivityUpdate($params, $result)
    {
        // Code executed after activity is updated
        // Код, выполняемый после обновления активности
        return $result;
    }
    
    public function onBeforeActivityDelete($params)
    {
        // Code executed before activity is deleted
        // Код, выполняемый перед удалением активности
        return $params;
    }
    
    public function onAfterActivityDelete($params, $result)
    {
        // Code executed after activity is deleted
        // Код, выполняемый после удаления активности
        return $result;
    }
    
    public function onBeforeActivityComment($params)
    {
        // Code executed before activity is commented
        // Код, выполняемый перед комментированием активности
        return $params;
    }
    
    public function onAfterActivityComment($params, $result)
    {
        // Code executed after activity is commented
        // Код, выполняемый после комментирования активности
        return $result;
    }
    
    public function onBeforeActivityLike($params)
    {
        // Code executed before activity is liked
        // Код, выполняемый перед лайком активности
        return $params;
    }
    
    public function onAfterActivityLike($params, $result)
    {
        // Code executed after activity is liked
        // Код, выполняемый после лайка активности
        return $result;
    }
    
    public function onBeforeActivityUnlike($params)
    {
        // Code executed before activity is unliked
        // Код, выполняемый перед отменой лайка активности
        return $params;
    }
    
    public function onAfterActivityUnlike($params, $result)
    {
        // Code executed after activity is unliked
        // Код, выполняемый после отмены лайка активности
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Socialnetwork\ActivityStream\Handler::register('custom_activity_stream', CustomActivityStreamHandler::class);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
class CCustomActivityStreamHandler extends CSocialnetworkActivityStreamHandler
{
    public function OnBeforeActivityCreate($params)
    {
        // Code executed before activity is created
        // Код, выполняемый перед созданием активности
        return $params;
    }
    
    public function OnAfterActivityCreate($params, $result)
    {
        // Code executed after activity is created
        // Код, выполняемый после создания активности
        return $result;
    }
    
    public function OnBeforeActivityUpdate($params)
    {
        // Code executed before activity is updated
        // Код, выполняемый перед обновлением активности
        return $params;
    }
    
    public function OnAfterActivityUpdate($params, $result)
    {
        // Code executed after activity is updated
        // Код, выполняемый после обновления активности
        return $result;
    }
    
    public function OnBeforeActivityDelete($params)
    {
        // Code executed before activity is deleted
        // Код, выполняемый перед удалением активности
        return $params;
    }
    
    public function OnAfterActivityDelete($params, $result)
    {
        // Code executed after activity is deleted
        // Код, выполняемый после удаления активности
        return $result;
    }
    
    public function OnBeforeActivityComment($params)
    {
        // Code executed before activity is commented
        // Код, выполняемый перед комментированием активности
        return $params;
    }
    
    public function OnAfterActivityComment($params, $result)
    {
        // Code executed after activity is commented
        // Код, выполняемый после комментирования активности
        return $result;
    }
    
    public function OnBeforeActivityLike($params)
    {
        // Code executed before activity is liked
        // Код, выполняемый перед лайком активности
        return $params;
    }
    
    public function OnAfterActivityLike($params, $result)
    {
        // Code executed after activity is liked
        // Код, выполняемый после лайка активности
        return $result;
    }
    
    public function OnBeforeActivityUnlike($params)
    {
        // Code executed before activity is unliked
        // Код, выполняемый перед отменой лайка активности
        return $params;
    }
    
    public function OnAfterActivityUnlike($params, $result)
    {
        // Code executed after activity is unliked
        // Код, выполняемый после отмены лайка активности
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CSocialnetworkActivityStreamHandler::Register('custom_activity_stream', 'CCustomActivityStreamHandler');
```

### Comment Handlers | Обработчики комментариев

#### Comment Handler | Обработчик комментариев

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
class CustomCommentHandler extends \Bitrix\Socialnetwork\Comment\Handler
{
    public function onBeforeCommentCreate($params)
    {
        // Code executed before comment is created
        // Код, выполняемый перед созданием комментария
        return $params;
    }
    
    public function onAfterCommentCreate($params, $result)
    {
        // Code executed after comment is created
        // Код, выполняемый после создания комментария
        return $result;
    }
    
    public function onBeforeCommentUpdate($params)
    {
        // Code executed before comment is updated
        // Код, выполняемый перед обновлением комментария
        return $params;
    }
    
    public function onAfterCommentUpdate($params, $result)
    {
        // Code executed after comment is updated
        // Код, выполняемый после обновления комментария
        return $result;
    }
    
    public function onBeforeCommentDelete($params)
    {
        // Code executed before comment is deleted
        // Код, выполняемый перед удалением комментария
        return $params;
    }
    
    public function onAfterCommentDelete($params, $result)
    {
        // Code executed after comment is deleted
        // Код, выполняемый после удаления комментария
        return $result;
    }
    
    public function onBeforeCommentLike($params)
    {
        // Code executed before comment is liked
        // Код, выполняемый перед лайком комментария
        return $params;
    }
    
    public function onAfterCommentLike($params, $result)
    {
        // Code executed after comment is liked
        // Код, выполняемый после лайка комментария
        return $result;
    }
    
    public function onBeforeCommentUnlike($params)
    {
        // Code executed before comment is unliked
        // Код, выполняемый перед отменой лайка комментария
        return $params;
    }
    
    public function onAfterCommentUnlike($params, $result)
    {
        // Code executed after comment is unliked
        // Код, выполняемый после отмены лайка комментария
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Socialnetwork\Comment\Handler::register('custom_comment', CustomCommentHandler::class);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
class CCustomCommentHandler extends CSocialnetworkCommentHandler
{
    public function OnBeforeCommentCreate($params)
    {
        // Code executed before comment is created
        // Код, выполняемый перед созданием комментария
        return $params;
    }
    
    public function OnAfterCommentCreate($params, $result)
    {
        // Code executed after comment is created
        // Код, выполняемый после создания комментария
        return $result;
    }
    
    public function OnBeforeCommentUpdate($params)
    {
        // Code executed before comment is updated
        // Код, выполняемый перед обновлением комментария
        return $params;
    }
    
    public function OnAfterCommentUpdate($params, $result)
    {
        // Code executed after comment is updated
        // Код, выполняемый после обновления комментария
        return $result;
    }
    
    public function OnBeforeCommentDelete($params)
    {
        // Code executed before comment is deleted
        // Код, выполняемый перед удалением комментария
        return $params;
    }
    
    public function OnAfterCommentDelete($params, $result)
    {
        // Code executed after comment is deleted
        // Код, выполняемый после удаления комментария
        return $result;
    }
    
    public function OnBeforeCommentLike($params)
    {
        // Code executed before comment is liked
        // Код, выполняемый перед лайком комментария
        return $params;
    }
    
    public function OnAfterCommentLike($params, $result)
    {
        // Code executed after comment is liked
        // Код, выполняемый после лайка комментария
        return $result;
    }
    
    public function OnBeforeCommentUnlike($params)
    {
        // Code executed before comment is unliked
        // Код, выполняемый перед отменой лайка комментария
        return $params;
    }
    
    public function OnAfterCommentUnlike($params, $result)
    {
        // Code executed after comment is unliked
        // Код, выполняемый после отмены лайка комментария
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CSocialnetworkCommentHandler::Register('custom_comment', 'CCustomCommentHandler');
```

### User Handlers | Обработчики пользователей

#### User Handler | Обработчик пользователей

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
class CustomUserHandler extends \Bitrix\Socialnetwork\User\Handler
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
    
    public function onBeforeUserFollow($params)
    {
        // Code executed before user follows another user
        // Код, выполняемый перед подпиской пользователя на другого пользователя
        return $params;
    }
    
    public function onAfterUserFollow($params, $result)
    {
        // Code executed after user follows another user
        // Код, выполняемый после подписки пользователя на другого пользователя
        return $result;
    }
    
    public function onBeforeUserUnfollow($params)
    {
        // Code executed before user unfollows another user
        // Код, выполняемый перед отпиской пользователя от другого пользователя
        return $params;
    }
    
    public function onAfterUserUnfollow($params, $result)
    {
        // Code executed after user unfollows another user
        // Код, выполняемый после отписки пользователя от другого пользователя
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Socialnetwork\User\Handler::register('custom_user', CustomUserHandler::class);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
class CCustomUserHandler extends CSocialnetworkUserHandler
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
    
    public function OnBeforeUserFollow($params)
    {
        // Code executed before user follows another user
        // Код, выполняемый перед подпиской пользователя на другого пользователя
        return $params;
    }
    
    public function OnAfterUserFollow($params, $result)
    {
        // Code executed after user follows another user
        // Код, выполняемый после подписки пользователя на другого пользователя
        return $result;
    }
    
    public function OnBeforeUserUnfollow($params)
    {
        // Code executed before user unfollows another user
        // Код, выполняемый перед отпиской пользователя от другого пользователя
        return $params;
    }
    
    public function OnAfterUserUnfollow($params, $result)
    {
        // Code executed after user unfollows another user
        // Код, выполняемый после отписки пользователя от другого пользователя
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CSocialnetworkUserHandler::Register('custom_user', 'CCustomUserHandler');
```

## REST API | REST API

### Workgroup Management | Управление рабочими группами

#### Create Workgroup | Создание рабочей группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\Workgroup::add([
    'NAME' => 'Custom Workgroup',
    'DESCRIPTION' => 'This is a custom workgroup',
    'VISIBLE' => 'Y',
    'OPENED' => 'Y',
    'CLOSED' => 'N',
    'KEYWORDS' => 'custom, workgroup',
    'OWNER_ID' => $userId,
    'IMAGE_ID' => $imageId,
    'PARAMS' => [
        'KEY1' => 'VALUE1',
        'KEY2' => 'VALUE2'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocialnetworkGroup::Add([
    'NAME' => 'Custom Workgroup',
    'DESCRIPTION' => 'This is a custom workgroup',
    'VISIBLE' => 'Y',
    'OPENED' => 'Y',
    'CLOSED' => 'N',
    'KEYWORDS' => 'custom, workgroup',
    'OWNER_ID' => $userId,
    'IMAGE_ID' => $imageId,
    'PARAMS' => [
        'KEY1' => 'VALUE1',
        'KEY2' => 'VALUE2'
    ]
]);
```

#### Update Workgroup | Обновление рабочей группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\Workgroup::update($workgroupId, [
    'NAME' => 'Updated Custom Workgroup',
    'DESCRIPTION' => 'This is an updated custom workgroup',
    'VISIBLE' => 'Y',
    'OPENED' => 'N',
    'CLOSED' => 'N',
    'KEYWORDS' => 'updated, custom, workgroup',
    'IMAGE_ID' => $newImageId,
    'PARAMS' => [
        'KEY1' => 'NEW_VALUE1',
        'KEY2' => 'NEW_VALUE2'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocialnetworkGroup::Update($workgroupId, [
    'NAME' => 'Updated Custom Workgroup',
    'DESCRIPTION' => 'This is an updated custom workgroup',
    'VISIBLE' => 'Y',
    'OPENED' => 'N',
    'CLOSED' => 'N',
    'KEYWORDS' => 'updated, custom, workgroup',
    'IMAGE_ID' => $newImageId,
    'PARAMS' => [
        'KEY1' => 'NEW_VALUE1',
        'KEY2' => 'NEW_VALUE2'
    ]
]);
```

#### Delete Workgroup | Удаление рабочей группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\Workgroup::delete($workgroupId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocialnetworkGroup::Delete($workgroupId);
```

#### Get Workgroup | Получение рабочей группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$workgroup = \Bitrix\Socialnetwork\Workgroup::getById($workgroupId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$workgroup = CSocialnetworkGroup::GetByID($workgroupId);
```

#### Join Workgroup | Присоединение к рабочей группе

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\Workgroup::join($workgroupId, $userId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocialnetworkGroup::UserJoin($workgroupId, $userId);
```

#### Leave Workgroup | Выход из рабочей группы

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\Workgroup::leave($workgroupId, $userId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocialnetworkGroup::UserLeave($workgroupId, $userId);
```

#### Invite to Workgroup | Приглашение в рабочую группу

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\Workgroup::invite($workgroupId, $userId, $inviterId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocialnetworkGroup::UserInvite($workgroupId, $userId, $inviterId);
```

### Activity Stream Management | Управление лентой активности

#### Create Activity | Создание активности

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\ActivityStream::add([
    'USER_ID' => $userId,
    'ENTITY_TYPE' => 'TASK',
    'ENTITY_ID' => $taskId,
    'EVENT_ID' => 'task_created',
    'TITLE' => 'New task created',
    'MESSAGE' => 'User created a new task',
    'TEXT_MESSAGE' => 'User created a new task',
    'URL' => '/company/personal/user/' . $userId . '/tasks/task/view/' . $taskId . '/',
    'MODULE_ID' => 'tasks',
    'PARAMS' => [
        'TASK_ID' => $taskId,
        'TASK_TITLE' => 'Task title',
        'TASK_DESCRIPTION' => 'Task description',
        'TASK_DEADLINE' => '2023-12-31 23:59:59',
        'TASK_PRIORITY' => 'high',
        'TASK_RESPONSIBLE_ID' => $responsibleId
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetLog::Add([
    'USER_ID' => $userId,
    'ENTITY_TYPE' => 'TASK',
    'ENTITY_ID' => $taskId,
    'EVENT_ID' => 'task_created',
    'TITLE' => 'New task created',
    'MESSAGE' => 'User created a new task',
    'TEXT_MESSAGE' => 'User created a new task',
    'URL' => '/company/personal/user/' . $userId . '/tasks/task/view/' . $taskId . '/',
    'MODULE_ID' => 'tasks',
    'PARAMS' => [
        'TASK_ID' => $taskId,
        'TASK_TITLE' => 'Task title',
        'TASK_DESCRIPTION' => 'Task description',
        'TASK_DEADLINE' => '2023-12-31 23:59:59',
        'TASK_PRIORITY' => 'high',
        'TASK_RESPONSIBLE_ID' => $responsibleId
    ]
]);
```

#### Update Activity | Обновление активности

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\ActivityStream::update($activityId, [
    'TITLE' => 'Updated task',
    'MESSAGE' => 'User updated a task',
    'TEXT_MESSAGE' => 'User updated a task',
    'PARAMS' => [
        'TASK_ID' => $taskId,
        'TASK_TITLE' => 'Updated task title',
        'TASK_DESCRIPTION' => 'Updated task description',
        'TASK_DEADLINE' => '2023-12-31 23:59:59',
        'TASK_PRIORITY' => 'medium',
        'TASK_RESPONSIBLE_ID' => $responsibleId
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetLog::Update($activityId, [
    'TITLE' => 'Updated task',
    'MESSAGE' => 'User updated a task',
    'TEXT_MESSAGE' => 'User updated a task',
    'PARAMS' => [
        'TASK_ID' => $taskId,
        'TASK_TITLE' => 'Updated task title',
        'TASK_DESCRIPTION' => 'Updated task description',
        'TASK_DEADLINE' => '2023-12-31 23:59:59',
        'TASK_PRIORITY' => 'medium',
        'TASK_RESPONSIBLE_ID' => $responsibleId
    ]
]);
```

#### Delete Activity | Удаление активности

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\ActivityStream::delete($activityId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetLog::Delete($activityId);
```

#### Get Activity | Получение активности

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$activity = \Bitrix\Socialnetwork\ActivityStream::getById($activityId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$activity = CSocNetLog::GetByID($activityId);
```

#### Comment Activity | Комментирование активности

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\ActivityStream::comment($activityId, [
    'USER_ID' => $userId,
    'MESSAGE' => 'This is a comment',
    'TEXT_MESSAGE' => 'This is a comment',
    'PARAMS' => [
        'KEY1' => 'VALUE1',
        'KEY2' => 'VALUE2'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetLog::Comment($activityId, [
    'USER_ID' => $userId,
    'MESSAGE' => 'This is a comment',
    'TEXT_MESSAGE' => 'This is a comment',
    'PARAMS' => [
        'KEY1' => 'VALUE1',
        'KEY2' => 'VALUE2'
    ]
]);
```

#### Like Activity | Лайк активности

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\ActivityStream::like($activityId, $userId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetLog::Like($activityId, $userId);
```

#### Unlike Activity | Отмена лайка активности

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\ActivityStream::unlike($activityId, $userId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetLog::Unlike($activityId, $userId);
```

### Comment Management | Управление комментариями

#### Create Comment | Создание комментария

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\Comment::add([
    'ENTITY_TYPE' => 'TASK',
    'ENTITY_ID' => $taskId,
    'USER_ID' => $userId,
    'MESSAGE' => 'This is a comment',
    'TEXT_MESSAGE' => 'This is a comment',
    'PARAMS' => [
        'KEY1' => 'VALUE1',
        'KEY2' => 'VALUE2'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetLogComments::Add([
    'ENTITY_TYPE' => 'TASK',
    'ENTITY_ID' => $taskId,
    'USER_ID' => $userId,
    'MESSAGE' => 'This is a comment',
    'TEXT_MESSAGE' => 'This is a comment',
    'PARAMS' => [
        'KEY1' => 'VALUE1',
        'KEY2' => 'VALUE2'
    ]
]);
```

#### Update Comment | Обновление комментария

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\Comment::update($commentId, [
    'MESSAGE' => 'This is an updated comment',
    'TEXT_MESSAGE' => 'This is an updated comment',
    'PARAMS' => [
        'KEY1' => 'NEW_VALUE1',
        'KEY2' => 'NEW_VALUE2'
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetLogComments::Update($commentId, [
    'MESSAGE' => 'This is an updated comment',
    'TEXT_MESSAGE' => 'This is an updated comment',
    'PARAMS' => [
        'KEY1' => 'NEW_VALUE1',
        'KEY2' => 'NEW_VALUE2'
    ]
]);
```

#### Delete Comment | Удаление комментария

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\Comment::delete($commentId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetLogComments::Delete($commentId);
```

#### Get Comment | Получение комментария

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$comment = \Bitrix\Socialnetwork\Comment::getById($commentId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$comment = CSocNetLogComments::GetByID($commentId);
```

#### Like Comment | Лайк комментария

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\Comment::like($commentId, $userId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetLogComments::Like($commentId, $userId);
```

#### Unlike Comment | Отмена лайка комментария

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\Comment::unlike($commentId, $userId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetLogComments::Unlike($commentId, $userId);
```

### User Management | Управление пользователями

#### Follow User | Подписка на пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\User::follow($userId, $followerId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetUser::Follow($userId, $followerId);
```

#### Unfollow User | Отписка от пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$result = \Bitrix\Socialnetwork\User::unfollow($userId, $followerId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$result = CSocNetUser::Unfollow($userId, $followerId);
```

#### Get User Followers | Получение подписчиков пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$followers = \Bitrix\Socialnetwork\User::getFollowers($userId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$followers = CSocNetUser::GetFollowers($userId);
```

#### Get User Following | Получение подписок пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('socialnetwork')
// Требуется: Bitrix\Main\Loader::includeModule('socialnetwork')
$following = \Bitrix\Socialnetwork\User::getFollowing($userId);

// Legacy
// Requires: CModule::IncludeModule('socialnetwork')
// Требуется: CModule::IncludeModule('socialnetwork')
$following = CSocNetUser::GetFollowing($userId);
``` 