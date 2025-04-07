# Tasks Module | Модуль Задачи

## Overview | Обзор

The Tasks module provides functionality for managing tasks, including creating, updating, and tracking task progress. | Модуль Задачи предоставляет функциональность для управления задачами, включая создание, обновление и отслеживание прогресса задач.

## Methods | Методы

### Tasks | Задачи

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'tasks.task.list',
    [
        'select' => ['*', 'UF_*'],
        'filter' => ['RESPONSIBLE_ID' => 1],
        'order' => ['DEADLINE' => 'ASC'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('tasks')
// Требуется: Bitrix\Main\Loader::includeModule('tasks')
$tasks = \Bitrix\Tasks\TaskTable::getList([
    'select' => ['*', 'UF_*'],
    'filter' => ['=RESPONSIBLE_ID' => 1],
    'order' => ['DEADLINE' => 'ASC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('tasks')
// Требуется: CModule::IncludeModule('tasks')
$tasks = CTasks::GetList(
    ['DEADLINE' => 'ASC'],
    ['RESPONSIBLE_ID' => 1],
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
    'tasks.task.add',
    [
        'fields' => [
            'TITLE' => 'New Task',
            'DESCRIPTION' => 'Task description',
            'RESPONSIBLE_ID' => 1,
            'CREATED_BY' => 1,
            'DEADLINE' => '2023-12-31',
            'PRIORITY' => 2
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('tasks')
// Требуется: Bitrix\Main\Loader::includeModule('tasks')
$result = \Bitrix\Tasks\Task::add([
    'TITLE' => 'New Task',
    'DESCRIPTION' => 'Task description',
    'RESPONSIBLE_ID' => 1,
    'CREATED_BY' => 1,
    'DEADLINE' => '2023-12-31',
    'PRIORITY' => 2
]);

// Legacy
// Requires: CModule::IncludeModule('tasks')
// Требуется: CModule::IncludeModule('tasks')
$taskFields = [
    'TITLE' => 'New Task',
    'DESCRIPTION' => 'Task description',
    'RESPONSIBLE_ID' => 1,
    'CREATED_BY' => 1,
    'DEADLINE' => '2023-12-31',
    'PRIORITY' => 2
];
$task = new CTasks();
$taskId = $task->Add($taskFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'tasks.task.update',
    [
        'taskId' => 123,
        'fields' => [
            'TITLE' => 'Updated Task',
            'STATUS' => 5,
            'DEADLINE' => '2024-01-15'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('tasks')
// Требуется: Bitrix\Main\Loader::includeModule('tasks')
$result = \Bitrix\Tasks\Task::update(123, [
    'TITLE' => 'Updated Task',
    'STATUS' => 5,
    'DEADLINE' => '2024-01-15'
]);

// Legacy
// Requires: CModule::IncludeModule('tasks')
// Требуется: CModule::IncludeModule('tasks')
$taskFields = [
    'TITLE' => 'Updated Task',
    'STATUS' => 5,
    'DEADLINE' => '2024-01-15'
];
$task = new CTasks();
$task->Update(123, $taskFields);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'tasks.task.delete',
    ['taskId' => 123]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('tasks')
// Требуется: Bitrix\Main\Loader::includeModule('tasks')
$result = \Bitrix\Tasks\Task::delete(123);

// Legacy
// Requires: CModule::IncludeModule('tasks')
// Требуется: CModule::IncludeModule('tasks')
$task = new CTasks();
$task->Delete(123);
```

### Task Comments | Комментарии к задачам

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'tasks.comment.list',
    [
        'taskId' => 123,
        'select' => ['*', 'UF_*'],
        'order' => ['POST_DATE' => 'DESC'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('tasks')
// Требуется: Bitrix\Main\Loader::includeModule('tasks')
$comments = \Bitrix\Tasks\CommentTable::getList([
    'select' => ['*', 'UF_*'],
    'filter' => ['=TASK_ID' => 123],
    'order' => ['POST_DATE' => 'DESC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('tasks')
// Требуется: CModule::IncludeModule('tasks')
$comments = CTaskComment::GetList(
    ['POST_DATE' => 'DESC'],
    ['TASK_ID' => 123],
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
    'tasks.comment.add',
    [
        'taskId' => 123,
        'fields' => [
            'POST_MESSAGE' => 'New comment',
            'AUTHOR_ID' => 1
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('tasks')
// Требуется: Bitrix\Main\Loader::includeModule('tasks')
$result = \Bitrix\Tasks\Comment::add([
    'TASK_ID' => 123,
    'POST_MESSAGE' => 'New comment',
    'AUTHOR_ID' => 1
]);

// Legacy
// Requires: CModule::IncludeModule('tasks')
// Требуется: CModule::IncludeModule('tasks')
$commentFields = [
    'TASK_ID' => 123,
    'POST_MESSAGE' => 'New comment',
    'AUTHOR_ID' => 1
];
$comment = new CTaskComment();
$commentId = $comment->Add($commentFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'tasks.comment.update',
    [
        'taskId' => 123,
        'commentId' => 456,
        'fields' => [
            'POST_MESSAGE' => 'Updated comment'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('tasks')
// Требуется: Bitrix\Main\Loader::includeModule('tasks')
$result = \Bitrix\Tasks\Comment::update(456, [
    'POST_MESSAGE' => 'Updated comment'
]);

// Legacy
// Requires: CModule::IncludeModule('tasks')
// Требуется: CModule::IncludeModule('tasks')
$commentFields = [
    'POST_MESSAGE' => 'Updated comment'
];
$comment = new CTaskComment();
$comment->Update(456, $commentFields);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'tasks.comment.delete',
    [
        'taskId' => 123,
        'commentId' => 456
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('tasks')
// Требуется: Bitrix\Main\Loader::includeModule('tasks')
$result = \Bitrix\Tasks\Comment::delete(456);

// Legacy
// Requires: CModule::IncludeModule('tasks')
// Требуется: CModule::IncludeModule('tasks')
$comment = new CTaskComment();
$comment->Delete(456);
```

### Task Checklists | Чек-листы задач

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'tasks.checklistitem.list',
    [
        'taskId' => 123,
        'select' => ['*', 'UF_*'],
        'order' => ['SORT_INDEX' => 'ASC'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('tasks')
// Требуется: Bitrix\Main\Loader::includeModule('tasks')
$checklistItems = \Bitrix\Tasks\CheckListTable::getList([
    'select' => ['*', 'UF_*'],
    'filter' => ['=TASK_ID' => 123],
    'order' => ['SORT_INDEX' => 'ASC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('tasks')
// Требуется: CModule::IncludeModule('tasks')
$checklistItems = CTaskCheckListItem::GetList(
    ['SORT_INDEX' => 'ASC'],
    ['TASK_ID' => 123],
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
    'tasks.checklistitem.add',
    [
        'taskId' => 123,
        'fields' => [
            'TITLE' => 'New checklist item',
            'IS_COMPLETE' => 'N',
            'SORT_INDEX' => 0
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('tasks')
// Требуется: Bitrix\Main\Loader::includeModule('tasks')
$result = \Bitrix\Tasks\CheckList::add([
    'TASK_ID' => 123,
    'TITLE' => 'New checklist item',
    'IS_COMPLETE' => 'N',
    'SORT_INDEX' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('tasks')
// Требуется: CModule::IncludeModule('tasks')
$checklistFields = [
    'TASK_ID' => 123,
    'TITLE' => 'New checklist item',
    'IS_COMPLETE' => 'N',
    'SORT_INDEX' => 0
];
$checklist = new CTaskCheckListItem();
$checklistId = $checklist->Add($checklistFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'tasks.checklistitem.update',
    [
        'taskId' => 123,
        'itemId' => 456,
        'fields' => [
            'TITLE' => 'Updated checklist item',
            'IS_COMPLETE' => 'Y'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('tasks')
// Требуется: Bitrix\Main\Loader::includeModule('tasks')
$result = \Bitrix\Tasks\CheckList::update(456, [
    'TITLE' => 'Updated checklist item',
    'IS_COMPLETE' => 'Y'
]);

// Legacy
// Requires: CModule::IncludeModule('tasks')
// Требуется: CModule::IncludeModule('tasks')
$checklistFields = [
    'TITLE' => 'Updated checklist item',
    'IS_COMPLETE' => 'Y'
];
$checklist = new CTaskCheckListItem();
$checklist->Update(456, $checklistFields);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'tasks.checklistitem.delete',
    [
        'taskId' => 123,
        'itemId' => 456
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('tasks')
// Требуется: Bitrix\Main\Loader::includeModule('tasks')
$result = \Bitrix\Tasks\CheckList::delete(456);

// Legacy
// Requires: CModule::IncludeModule('tasks')
// Требуется: CModule::IncludeModule('tasks')
$checklist = new CTaskCheckListItem();
$checklist->Delete(456);
``` 