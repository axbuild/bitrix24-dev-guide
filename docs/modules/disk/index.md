# Disk Module | Модуль Disk

## Overview | Обзор

The Disk module provides functionality for managing files and documents in Bitrix24. It enables users to store, share, and collaborate on files within the platform. | Модуль Disk предоставляет функциональность для управления файлами и документами в Bitrix24. Он позволяет пользователям хранить, делиться и совместно работать с файлами в рамках платформы.

## Methods | Методы

### Storage Management | Управление хранилищем

#### Get Storage | Получение хранилища

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$storage = \Bitrix\Disk\Storage::getById($storageId);

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$storage = CDiskStorage::GetById($storageId);
```

#### Create Storage | Создание хранилища

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$storage = \Bitrix\Disk\Storage::add([
    'NAME' => 'My Storage',
    'ENTITY_TYPE' => 'user',
    'ENTITY_ID' => $USER->GetID(),
    'MODULE_ID' => 'disk'
]);

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$storage = CDiskStorage::Add([
    'NAME' => 'My Storage',
    'ENTITY_TYPE' => 'user',
    'ENTITY_ID' => $USER->GetID(),
    'MODULE_ID' => 'disk'
]);
```

### File Operations | Операции с файлами

#### Upload File | Загрузка файла

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$file = \Bitrix\Disk\File::add([
    'NAME' => 'document.pdf',
    'CONTENT' => file_get_contents('path/to/file.pdf'),
    'SIZE' => filesize('path/to/file.pdf'),
    'STORAGE_ID' => $storageId,
    'CREATED_BY' => $USER->GetID()
]);

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$file = CDiskFile::Add([
    'NAME' => 'document.pdf',
    'CONTENT' => file_get_contents('path/to/file.pdf'),
    'SIZE' => filesize('path/to/file.pdf'),
    'STORAGE_ID' => $storageId,
    'CREATED_BY' => $USER->GetID()
]);
```

#### Download File | Скачивание файла

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$file = \Bitrix\Disk\File::getById($fileId);
$content = $file->getContent();

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$file = CDiskFile::GetById($fileId);
$content = $file->GetContent();
```

#### Delete File | Удаление файла

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$file = \Bitrix\Disk\File::getById($fileId);
$result = $file->delete($USER->GetID());

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$file = CDiskFile::GetById($fileId);
$result = $file->Delete($USER->GetID());
```

### Folder Operations | Операции с папками

#### Create Folder | Создание папки

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$folder = \Bitrix\Disk\Folder::add([
    'NAME' => 'My Folder',
    'STORAGE_ID' => $storageId,
    'CREATED_BY' => $USER->GetID()
]);

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$folder = CDiskFolder::Add([
    'NAME' => 'My Folder',
    'STORAGE_ID' => $storageId,
    'CREATED_BY' => $USER->GetID()
]);
```

#### Get Folder Contents | Получение содержимого папки

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$folder = \Bitrix\Disk\Folder::getById($folderId);
$items = $folder->getChildren();

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$folder = CDiskFolder::GetById($folderId);
$items = $folder->GetChildren();
```

### Sharing | Общий доступ

#### Share File | Предоставление доступа к файлу

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$file = \Bitrix\Disk\File::getById($fileId);
$sharing = $file->addSharing([
    'ENTITY_TYPE' => 'user',
    'ENTITY_ID' => $userId,
    'ACCESS_CODE' => 'full'
]);

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$file = CDiskFile::GetById($fileId);
$sharing = $file->AddSharing([
    'ENTITY_TYPE' => 'user',
    'ENTITY_ID' => $userId,
    'ACCESS_CODE' => 'full'
]);
```

#### Get Shared Items | Получение общих элементов

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$sharedItems = \Bitrix\Disk\Sharing::getSharedWithMe($USER->GetID());

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$sharedItems = CDiskSharing::GetSharedWithMe($USER->GetID());
```

### Version Control | Контроль версий

#### Create Version | Создание версии

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$file = \Bitrix\Disk\File::getById($fileId);
$version = $file->createVersion([
    'CONTENT' => file_get_contents('path/to/new_version.pdf'),
    'SIZE' => filesize('path/to/new_version.pdf'),
    'CREATED_BY' => $USER->GetID()
]);

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$file = CDiskFile::GetById($fileId);
$version = $file->CreateVersion([
    'CONTENT' => file_get_contents('path/to/new_version.pdf'),
    'SIZE' => filesize('path/to/new_version.pdf'),
    'CREATED_BY' => $USER->GetID()
]);
```

#### Get Versions | Получение версий

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$file = \Bitrix\Disk\File::getById($fileId);
$versions = $file->getVersions();

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$file = CDiskFile::GetById($fileId);
$versions = $file->GetVersions();
```

### External Links | Внешние ссылки

#### Create External Link | Создание внешней ссылки

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$file = \Bitrix\Disk\File::getById($fileId);
$link = $file->addExternalLink([
    'CREATED_BY' => $USER->GetID(),
    'TYPE' => 'file',
    'OBJECT_ID' => $fileId,
    'DESCRIPTION' => 'External link description'
]);

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$file = CDiskFile::GetById($fileId);
$link = $file->AddExternalLink([
    'CREATED_BY' => $USER->GetID(),
    'TYPE' => 'file',
    'OBJECT_ID' => $fileId,
    'DESCRIPTION' => 'External link description'
]);
```

#### Get External Links | Получение внешних ссылок

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('disk')
// Требуется: Bitrix\Main\Loader::includeModule('disk')
$file = \Bitrix\Disk\File::getById($fileId);
$links = $file->getExternalLinks();

// Legacy
// Requires: CModule::IncludeModule('disk')
// Требуется: CModule::IncludeModule('disk')
$file = CDiskFile::GetById($fileId);
$links = $file->GetExternalLinks();
``` 