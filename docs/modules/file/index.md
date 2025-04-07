# File Module | Модуль Файлы

## Overview | Обзор

The File module provides functionality for managing files, including uploading, downloading, and manipulating files in the Bitrix24 system. | Модуль Файлы предоставляет функциональность для управления файлами, включая загрузку, скачивание и манипуляции с файлами в системе Bitrix24.

## Methods | Методы

### Files | Файлы

#### Upload | Загрузка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'disk.storage.uploadfile',
    [
        'id' => 1,
        'data' => base64_encode(file_get_contents('path/to/file.pdf')),
        'filename' => 'document.pdf',
        'contentType' => 'application/pdf'
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$storage = \Bitrix\Disk\Storage::loadById(1);
$file = $storage->uploadFile(
    \Bitrix\Main\Application::getInstance()->getContext()->getRequest()->getFile('file'),
    [
        'NAME' => 'document.pdf',
        'CONTENT_TYPE' => 'application/pdf'
    ],
    [],
    true
);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$fileArray = CFile::MakeFileArray('path/to/file.pdf');
$fileId = CFile::SaveFile($fileArray, 'disk');
```

#### Download | Скачивание

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'disk.file.get',
    [
        'id' => 123
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$file = \Bitrix\Disk\File::loadById(123);
$downloadUrl = $file->createExternalLink([
    'type' => \Bitrix\Disk\DownloadController::class,
    'action' => 'default',
    'time' => 3600
]);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
$filePath = CFile::GetPath($fileId);
$fileArray = CFile::GetFileArray($fileId);
$downloadUrl = CFile::GetFileSRC($fileArray);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'disk.file.delete',
    [
        'id' => 123
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$file = \Bitrix\Disk\File::loadById(123);
$file->delete($userId);

// Legacy
// Requires: CModule::IncludeModule('main')
// Требуется: CModule::IncludeModule('main')
CFile::Delete($fileId);
```

### File Storage | Хранилище файлов

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'disk.storage.getlist',
    [
        'filter' => ['ENTITY_TYPE' => 'user'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$storages = \Bitrix\Disk\Storage::getList([
    'filter' => ['=ENTITY_TYPE' => 'user'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$storages = CDiskStorage::GetList(
    ['ID' => 'DESC'],
    ['ENTITY_TYPE' => 'user'],
    false,
    ['nTopCount' => 50],
    ['*']
);
```

#### Create | Создание

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'disk.storage.add',
    [
        'fields' => [
            'NAME' => 'New Storage',
            'ENTITY_TYPE' => 'group',
            'ENTITY_ID' => 1
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$result = \Bitrix\Disk\Storage::add([
    'NAME' => 'New Storage',
    'ENTITY_TYPE' => 'group',
    'ENTITY_ID' => 1
]);

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$storageFields = [
    'NAME' => 'New Storage',
    'ENTITY_TYPE' => 'group',
    'ENTITY_ID' => 1
];
$storage = new CDiskStorage();
$storageId = $storage->Add($storageFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'disk.storage.update',
    [
        'id' => 123,
        'fields' => [
            'NAME' => 'Updated Storage'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$storage = \Bitrix\Disk\Storage::loadById(123);
$storage->update([
    'NAME' => 'Updated Storage'
]);

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$storageFields = [
    'NAME' => 'Updated Storage'
];
$storage = new CDiskStorage();
$storage->Update(123, $storageFields);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'disk.storage.delete',
    [
        'id' => 123
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$storage = \Bitrix\Disk\Storage::loadById(123);
$storage->delete($userId);

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$storage = new CDiskStorage();
$storage->Delete(123);
```

### File Folders | Папки файлов

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'disk.folder.getlist',
    [
        'id' => 1,
        'filter' => ['TYPE' => 'folder'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$folders = \Bitrix\Disk\Folder::getList([
    'filter' => ['=STORAGE_ID' => 1, '=TYPE' => 'folder'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$folders = CDiskFolder::GetList(
    ['ID' => 'DESC'],
    ['STORAGE_ID' => 1, 'TYPE' => 'folder'],
    false,
    ['nTopCount' => 50],
    ['*']
);
```

#### Create | Создание

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'disk.folder.add',
    [
        'id' => 1,
        'fields' => [
            'NAME' => 'New Folder',
            'PARENT_ID' => 0
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$storage = \Bitrix\Disk\Storage::loadById(1);
$folder = $storage->addFolder([
    'NAME' => 'New Folder',
    'PARENT_ID' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$folderFields = [
    'NAME' => 'New Folder',
    'STORAGE_ID' => 1,
    'PARENT_ID' => 0
];
$folder = new CDiskFolder();
$folderId = $folder->Add($folderFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'disk.folder.update',
    [
        'id' => 123,
        'fields' => [
            'NAME' => 'Updated Folder'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$folder = \Bitrix\Disk\Folder::loadById(123);
$folder->update([
    'NAME' => 'Updated Folder'
]);

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$folderFields = [
    'NAME' => 'Updated Folder'
];
$folder = new CDiskFolder();
$folder->Update(123, $folderFields);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'disk.folder.delete',
    [
        'id' => 123
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$folder = \Bitrix\Disk\Folder::loadById(123);
$folder->delete($userId);

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$folder = new CDiskFolder();
$folder->Delete(123);
``` 