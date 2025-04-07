# Voximplant Module | Модуль Voximplant

## Overview | Обзор

The Voximplant module provides functionality for telephony integration in Bitrix24. It enables users to make and receive calls, manage call flows, record calls, and integrate with CRM and other modules. | Модуль Voximplant предоставляет функциональность для интеграции телефонии в Bitrix24. Он позволяет пользователям совершать и принимать звонки, управлять потоками звонков, записывать звонки и интегрироваться с CRM и другими модулями.

## Methods | Методы

### Phone Number Management | Управление телефонными номерами

#### Get Phone Numbers | Получение телефонных номеров

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$phoneNumbers = \Bitrix\Voximplant\Phone::getList([
    'select' => ['*'],
    'filter' => ['ACTIVE' => 'Y']
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$phoneNumbers = CVoxImplantPhone::GetList([], ['ACTIVE' => 'Y']);
```

#### Add Phone Number | Добавление телефонного номера

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Phone::add([
    'PHONE_NUMBER' => '+74951234567',
    'NAME' => 'Main Office',
    'ACTIVE' => 'Y',
    'DESCRIPTION' => 'Main office phone number'
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoxImplantPhone::Add([
    'PHONE_NUMBER' => '+74951234567',
    'NAME' => 'Main Office',
    'ACTIVE' => 'Y',
    'DESCRIPTION' => 'Main office phone number'
]);
```

#### Update Phone Number | Обновление телефонного номера

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Phone::update($phoneId, [
    'NAME' => 'Updated Main Office',
    'DESCRIPTION' => 'Updated main office phone number'
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoxImplantPhone::Update($phoneId, [
    'NAME' => 'Updated Main Office',
    'DESCRIPTION' => 'Updated main office phone number'
]);
```

#### Delete Phone Number | Удаление телефонного номера

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Phone::delete($phoneId);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoxImplantPhone::Delete($phoneId);
```

### Call Management | Управление звонками

#### Make Call | Совершение звонка

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$call = \Bitrix\Voximplant\Call::make([
    'PHONE_NUMBER' => '+74951234567',
    'USER_ID' => $USER->GetID(),
    'CALLER_ID' => '+74951234567',
    'CRM_ENTITY_TYPE' => 'LEAD',
    'CRM_ENTITY_ID' => $leadId
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$call = CVoxImplant::MakeCall([
    'PHONE_NUMBER' => '+74951234567',
    'USER_ID' => $USER->GetID(),
    'CALLER_ID' => '+74951234567',
    'CRM_ENTITY_TYPE' => 'LEAD',
    'CRM_ENTITY_ID' => $leadId
]);
```

#### Get Call | Получение информации о звонке

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$call = \Bitrix\Voximplant\Call::getById($callId);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$call = CVoxImplant::GetCall($callId);
```

#### Get Call List | Получение списка звонков

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$calls = \Bitrix\Voximplant\Call::getList([
    'select' => ['*'],
    'filter' => [
        'USER_ID' => $USER->GetID(),
        '>=CALL_START_DATE' => new \Bitrix\Main\Type\DateTime('2023-01-01 00:00:00')
    ],
    'order' => ['CALL_START_DATE' => 'DESC']
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$calls = CVoxImplant::GetCallList([
    'USER_ID' => $USER->GetID(),
    '>=CALL_START_DATE' => '2023-01-01 00:00:00'
], ['CALL_START_DATE' => 'DESC']);
```

#### End Call | Завершение звонка

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$call = \Bitrix\Voximplant\Call::getById($callId);
$result = $call->end();

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoxImplant::EndCall($callId);
```

### Call Routing | Маршрутизация звонков

#### Get Routing Rules | Получение правил маршрутизации

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$rules = \Bitrix\Voximplant\Routing::getRules([
    'select' => ['*'],
    'filter' => ['ACTIVE' => 'Y']
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$rules = CVoxImplantRouting::GetList([], ['ACTIVE' => 'Y']);
```

#### Add Routing Rule | Добавление правила маршрутизации

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Routing::addRule([
    'NAME' => 'Sales Department',
    'PHONE_NUMBER' => '+74951234567',
    'QUEUE_ID' => $queueId,
    'ACTIVE' => 'Y',
    'DESCRIPTION' => 'Route calls to sales department'
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoxImplantRouting::Add([
    'NAME' => 'Sales Department',
    'PHONE_NUMBER' => '+74951234567',
    'QUEUE_ID' => $queueId,
    'ACTIVE' => 'Y',
    'DESCRIPTION' => 'Route calls to sales department'
]);
```

#### Update Routing Rule | Обновление правила маршрутизации

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Routing::updateRule($ruleId, [
    'NAME' => 'Updated Sales Department',
    'DESCRIPTION' => 'Updated route calls to sales department'
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoxImplantRouting::Update($ruleId, [
    'NAME' => 'Updated Sales Department',
    'DESCRIPTION' => 'Updated route calls to sales department'
]);
```

#### Delete Routing Rule | Удаление правила маршрутизации

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Routing::deleteRule($ruleId);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoxImplantRouting::Delete($ruleId);
```

### Queue Management | Управление очередями

#### Get Queues | Получение очередей

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$queues = \Bitrix\Voximplant\Queue::getList([
    'select' => ['*'],
    'filter' => ['ACTIVE' => 'Y']
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$queues = CVoxImplantQueue::GetList([], ['ACTIVE' => 'Y']);
```

#### Add Queue | Добавление очереди

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Queue::add([
    'NAME' => 'Sales Queue',
    'ACTIVE' => 'Y',
    'DESCRIPTION' => 'Queue for sales department',
    'USERS' => [$userId1, $userId2, $userId3]
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoxImplantQueue::Add([
    'NAME' => 'Sales Queue',
    'ACTIVE' => 'Y',
    'DESCRIPTION' => 'Queue for sales department',
    'USERS' => [$userId1, $userId2, $userId3]
]);
```

#### Update Queue | Обновление очереди

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Queue::update($queueId, [
    'NAME' => 'Updated Sales Queue',
    'DESCRIPTION' => 'Updated queue for sales department',
    'USERS' => [$userId1, $userId2, $userId3, $userId4]
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoxImplantQueue::Update($queueId, [
    'NAME' => 'Updated Sales Queue',
    'DESCRIPTION' => 'Updated queue for sales department',
    'USERS' => [$userId1, $userId2, $userId3, $userId4]
]);
```

#### Delete Queue | Удаление очереди

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Queue::delete($queueId);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoxImplantQueue::Delete($queueId);
```

### CRM Integration | Интеграция с CRM

#### Link Call to CRM | Привязка звонка к CRM

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$call = \Bitrix\Voximplant\Call::getById($callId);
$result = $call->linkToCrm([
    'ENTITY_TYPE' => 'LEAD',
    'ENTITY_ID' => $leadId
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoxImplant::LinkCallToCrm($callId, 'LEAD', $leadId);
```

#### Get CRM Calls | Получение звонков из CRM

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$calls = \Bitrix\Voximplant\Call::getCrmCalls([
    'ENTITY_TYPE' => 'LEAD',
    'ENTITY_ID' => $leadId
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$calls = CVoxImplant::GetCrmCalls('LEAD', $leadId);
```

#### Create CRM Activity | Создание активности в CRM

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$call = \Bitrix\Voximplant\Call::getById($callId);
$result = $call->createCrmActivity([
    'ENTITY_TYPE' => 'LEAD',
    'ENTITY_ID' => $leadId,
    'SUBJECT' => 'Phone call',
    'DESCRIPTION' => 'Call with client',
    'RESPONSIBLE_ID' => $USER->GetID()
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoxImplant::CreateCrmActivity($callId, 'LEAD', $leadId, [
    'SUBJECT' => 'Phone call',
    'DESCRIPTION' => 'Call with client',
    'RESPONSIBLE_ID' => $USER->GetID()
]);
```

### Call Recording | Запись звонков

#### Start Recording | Начало записи звонка

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$call = \Bitrix\Voximplant\Call::getById($callId);
$result = $call->startRecording();

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoxImplant::StartRecording($callId);
```

#### Stop Recording | Остановка записи звонка

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$call = \Bitrix\Voximplant\Call::getById($callId);
$result = $call->stopRecording();

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoxImplant::StopRecording($callId);
```

#### Get Recording | Получение записи звонка

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$call = \Bitrix\Voximplant\Call::getById($callId);
$recording = $call->getRecording();

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$recording = CVoxImplant::GetRecording($callId);
```

### Statistics | Статистика

#### Get Call Statistics | Получение статистики звонков

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$statistics = \Bitrix\Voximplant\Statistics::getCallStatistics([
    'USER_ID' => $USER->GetID(),
    'FROM' => new \Bitrix\Main\Type\DateTime('2023-01-01 00:00:00'),
    'TO' => new \Bitrix\Main\Type\DateTime('2023-01-31 23:59:59')
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$statistics = CVoxImplant::GetCallStatistics([
    'USER_ID' => $USER->GetID(),
    'FROM' => '2023-01-01 00:00:00',
    'TO' => '2023-01-31 23:59:59'
]);
```

#### Get Queue Statistics | Получение статистики очередей

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$statistics = \Bitrix\Voximplant\Statistics::getQueueStatistics([
    'QUEUE_ID' => $queueId,
    'FROM' => new \Bitrix\Main\Type\DateTime('2023-01-01 00:00:00'),
    'TO' => new \Bitrix\Main\Type\DateTime('2023-01-31 23:59:59')
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$statistics = CVoxImplant::GetQueueStatistics([
    'QUEUE_ID' => $queueId,
    'FROM' => '2023-01-01 00:00:00',
    'TO' => '2023-01-31 23:59:59'
]);
```

### WebRTC Integration | Интеграция с WebRTC

#### Initialize WebRTC | Инициализация WebRTC

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$webrtc = \Bitrix\Voximplant\WebRTC::initialize([
    'USER_ID' => $USER->GetID(),
    'DEVICE_TYPE' => 'desktop'
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$webrtc = CVoxImplantWebRTC::Initialize([
    'USER_ID' => $USER->GetID(),
    'DEVICE_TYPE' => 'desktop'
]);
```

#### Get WebRTC Settings | Получение настроек WebRTC

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$settings = \Bitrix\Voximplant\WebRTC::getSettings($USER->GetID());

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$settings = CVoxImplantWebRTC::GetSettings($USER->GetID());
```

#### Update WebRTC Settings | Обновление настроек WebRTC

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\WebRTC::updateSettings($USER->GetID(), [
    'DEVICE_TYPE' => 'mobile',
    'ENABLE_NOTIFICATIONS' => 'Y'
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoxImplantWebRTC::UpdateSettings($USER->GetID(), [
    'DEVICE_TYPE' => 'mobile',
    'ENABLE_NOTIFICATIONS' => 'Y'
]);
```

## Handlers | Обработчики

### Call Handlers | Обработчики звонков

#### Call Handler | Обработчик звонка

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
class CustomCallHandler extends \Bitrix\Voximplant\Call\Handler
{
    public function onBeforeCallStart($params)
    {
        // Code executed before call is started
        // Код, выполняемый перед началом звонка
        return $params;
    }
    
    public function onAfterCallStart($params, $result)
    {
        // Code executed after call is started
        // Код, выполняемый после начала звонка
        return $result;
    }
    
    public function onBeforeCallEnd($params)
    {
        // Code executed before call is ended
        // Код, выполняемый перед завершением звонка
        return $params;
    }
    
    public function onAfterCallEnd($params, $result)
    {
        // Code executed after call is ended
        // Код, выполняемый после завершения звонка
        return $result;
    }
    
    public function onBeforeCallTransfer($params)
    {
        // Code executed before call is transferred
        // Код, выполняемый перед перенаправлением звонка
        return $params;
    }
    
    public function onAfterCallTransfer($params, $result)
    {
        // Code executed after call is transferred
        // Код, выполняемый после перенаправления звонка
        return $result;
    }
    
    public function onBeforeCallRecord($params)
    {
        // Code executed before call is recorded
        // Код, выполняемый перед записью звонка
        return $params;
    }
    
    public function onAfterCallRecord($params, $result)
    {
        // Code executed after call is recorded
        // Код, выполняемый после записи звонка
        return $result;
    }
    
    public function onBeforeCallAnswer($params)
    {
        // Code executed before call is answered
        // Код, выполняемый перед ответом на звонок
        return $params;
    }
    
    public function onAfterCallAnswer($params, $result)
    {
        // Code executed after call is answered
        // Код, выполняемый после ответа на звонок
        return $result;
    }
    
    public function onBeforeCallReject($params)
    {
        // Code executed before call is rejected
        // Код, выполняемый перед отклонением звонка
        return $params;
    }
    
    public function onAfterCallReject($params, $result)
    {
        // Code executed after call is rejected
        // Код, выполняемый после отклонения звонка
        return $result;
    }
    
    public function onBeforeCallHold($params)
    {
        // Code executed before call is held
        // Код, выполняемый перед постановкой звонка на удержание
        return $params;
    }
    
    public function onAfterCallHold($params, $result)
    {
        // Code executed after call is held
        // Код, выполняемый после постановки звонка на удержание
        return $result;
    }
    
    public function onBeforeCallUnhold($params)
    {
        // Code executed before call is unheld
        // Код, выполняемый перед снятием звонка с удержания
        return $params;
    }
    
    public function onAfterCallUnhold($params, $result)
    {
        // Code executed after call is unheld
        // Код, выполняемый после снятия звонка с удержания
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Voximplant\Call\Handler::register('custom_call', CustomCallHandler::class);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
class CCustomCallHandler extends CVoximplantCallHandler
{
    public function OnBeforeCallStart($params)
    {
        // Code executed before call is started
        // Код, выполняемый перед началом звонка
        return $params;
    }
    
    public function OnAfterCallStart($params, $result)
    {
        // Code executed after call is started
        // Код, выполняемый после начала звонка
        return $result;
    }
    
    public function OnBeforeCallEnd($params)
    {
        // Code executed before call is ended
        // Код, выполняемый перед завершением звонка
        return $params;
    }
    
    public function OnAfterCallEnd($params, $result)
    {
        // Code executed after call is ended
        // Код, выполняемый после завершения звонка
        return $result;
    }
    
    public function OnBeforeCallTransfer($params)
    {
        // Code executed before call is transferred
        // Код, выполняемый перед перенаправлением звонка
        return $params;
    }
    
    public function OnAfterCallTransfer($params, $result)
    {
        // Code executed after call is transferred
        // Код, выполняемый после перенаправления звонка
        return $result;
    }
    
    public function OnBeforeCallRecord($params)
    {
        // Code executed before call is recorded
        // Код, выполняемый перед записью звонка
        return $params;
    }
    
    public function OnAfterCallRecord($params, $result)
    {
        // Code executed after call is recorded
        // Код, выполняемый после записи звонка
        return $result;
    }
    
    public function OnBeforeCallAnswer($params)
    {
        // Code executed before call is answered
        // Код, выполняемый перед ответом на звонок
        return $params;
    }
    
    public function OnAfterCallAnswer($params, $result)
    {
        // Code executed after call is answered
        // Код, выполняемый после ответа на звонок
        return $result;
    }
    
    public function OnBeforeCallReject($params)
    {
        // Code executed before call is rejected
        // Код, выполняемый перед отклонением звонка
        return $params;
    }
    
    public function OnAfterCallReject($params, $result)
    {
        // Code executed after call is rejected
        // Код, выполняемый после отклонения звонка
        return $result;
    }
    
    public function OnBeforeCallHold($params)
    {
        // Code executed before call is held
        // Код, выполняемый перед постановкой звонка на удержание
        return $params;
    }
    
    public function OnAfterCallHold($params, $result)
    {
        // Code executed after call is held
        // Код, выполняемый после постановки звонка на удержание
        return $result;
    }
    
    public function OnBeforeCallUnhold($params)
    {
        // Code executed before call is unheld
        // Код, выполняемый перед снятием звонка с удержания
        return $params;
    }
    
    public function OnAfterCallUnhold($params, $result)
    {
        // Code executed after call is unheld
        // Код, выполняемый после снятия звонка с удержания
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CVoximplantCallHandler::Register('custom_call', 'CCustomCallHandler');
```

### Line Handlers | Обработчики линий

#### Line Handler | Обработчик линии

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
class CustomLineHandler extends \Bitrix\Voximplant\Line\Handler
{
    public function onBeforeLineCreate($params)
    {
        // Code executed before line is created
        // Код, выполняемый перед созданием линии
        return $params;
    }
    
    public function onAfterLineCreate($params, $result)
    {
        // Code executed after line is created
        // Код, выполняемый после создания линии
        return $result;
    }
    
    public function onBeforeLineUpdate($params)
    {
        // Code executed before line is updated
        // Код, выполняемый перед обновлением линии
        return $params;
    }
    
    public function onAfterLineUpdate($params, $result)
    {
        // Code executed after line is updated
        // Код, выполняемый после обновления линии
        return $result;
    }
    
    public function onBeforeLineDelete($params)
    {
        // Code executed before line is deleted
        // Код, выполняемый перед удалением линии
        return $params;
    }
    
    public function onAfterLineDelete($params, $result)
    {
        // Code executed after line is deleted
        // Код, выполняемый после удаления линии
        return $result;
    }
    
    public function onBeforeLineAssign($params)
    {
        // Code executed before line is assigned
        // Код, выполняемый перед назначением линии
        return $params;
    }
    
    public function onAfterLineAssign($params, $result)
    {
        // Code executed after line is assigned
        // Код, выполняемый после назначения линии
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Voximplant\Line\Handler::register('custom_line', CustomLineHandler::class);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
class CCustomLineHandler extends CVoximplantLineHandler
{
    public function OnBeforeLineCreate($params)
    {
        // Code executed before line is created
        // Код, выполняемый перед созданием линии
        return $params;
    }
    
    public function OnAfterLineCreate($params, $result)
    {
        // Code executed after line is created
        // Код, выполняемый после создания линии
        return $result;
    }
    
    public function OnBeforeLineUpdate($params)
    {
        // Code executed before line is updated
        // Код, выполняемый перед обновлением линии
        return $params;
    }
    
    public function OnAfterLineUpdate($params, $result)
    {
        // Code executed after line is updated
        // Код, выполняемый после обновления линии
        return $result;
    }
    
    public function OnBeforeLineDelete($params)
    {
        // Code executed before line is deleted
        // Код, выполняемый перед удалением линии
        return $params;
    }
    
    public function OnAfterLineDelete($params, $result)
    {
        // Code executed after line is deleted
        // Код, выполняемый после удаления линии
        return $result;
    }
    
    public function OnBeforeLineAssign($params)
    {
        // Code executed before line is assigned
        // Код, выполняемый перед назначением линии
        return $params;
    }
    
    public function OnAfterLineAssign($params, $result)
    {
        // Code executed after line is assigned
        // Код, выполняемый после назначения линии
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CVoximplantLineHandler::Register('custom_line', 'CCustomLineHandler');
```

### User Handlers | Обработчики пользователей

#### User Handler | Обработчик пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
class CustomUserHandler extends \Bitrix\Voximplant\User\Handler
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
    
    public function onBeforeUserAssign($params)
    {
        // Code executed before user is assigned
        // Код, выполняемый перед назначением пользователя
        return $params;
    }
    
    public function onAfterUserAssign($params, $result)
    {
        // Code executed after user is assigned
        // Код, выполняемый после назначения пользователя
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Voximplant\User\Handler::register('custom_user', CustomUserHandler::class);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
class CCustomUserHandler extends CVoximplantUserHandler
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
    
    public function OnBeforeUserAssign($params)
    {
        // Code executed before user is assigned
        // Код, выполняемый перед назначением пользователя
        return $params;
    }
    
    public function OnAfterUserAssign($params, $result)
    {
        // Code executed after user is assigned
        // Код, выполняемый после назначения пользователя
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CVoximplantUserHandler::Register('custom_user', 'CCustomUserHandler');
```

### Call Flow Handlers | Обработчики потоков звонков

#### Call Flow Handler | Обработчик потока звонков

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
class CustomCallFlowHandler extends \Bitrix\Voximplant\CallFlow\Handler
{
    public function onBeforeCallFlowCreate($params)
    {
        // Code executed before call flow is created
        // Код, выполняемый перед созданием потока звонков
        return $params;
    }
    
    public function onAfterCallFlowCreate($params, $result)
    {
        // Code executed after call flow is created
        // Код, выполняемый после создания потока звонков
        return $result;
    }
    
    public function onBeforeCallFlowUpdate($params)
    {
        // Code executed before call flow is updated
        // Код, выполняемый перед обновлением потока звонков
        return $params;
    }
    
    public function onAfterCallFlowUpdate($params, $result)
    {
        // Code executed after call flow is updated
        // Код, выполняемый после обновления потока звонков
        return $result;
    }
    
    public function onBeforeCallFlowDelete($params)
    {
        // Code executed before call flow is deleted
        // Код, выполняемый перед удалением потока звонков
        return $params;
    }
    
    public function onAfterCallFlowDelete($params, $result)
    {
        // Code executed after call flow is deleted
        // Код, выполняемый после удаления потока звонков
        return $result;
    }
    
    public function onBeforeCallFlowExecute($params)
    {
        // Code executed before call flow is executed
        // Код, выполняемый перед выполнением потока звонков
        return $params;
    }
    
    public function onAfterCallFlowExecute($params, $result)
    {
        // Code executed after call flow is executed
        // Код, выполняемый после выполнения потока звонков
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Voximplant\CallFlow\Handler::register('custom_call_flow', CustomCallFlowHandler::class);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
class CCustomCallFlowHandler extends CVoximplantCallFlowHandler
{
    public function OnBeforeCallFlowCreate($params)
    {
        // Code executed before call flow is created
        // Код, выполняемый перед созданием потока звонков
        return $params;
    }
    
    public function OnAfterCallFlowCreate($params, $result)
    {
        // Code executed after call flow is created
        // Код, выполняемый после создания потока звонков
        return $result;
    }
    
    public function OnBeforeCallFlowUpdate($params)
    {
        // Code executed before call flow is updated
        // Код, выполняемый перед обновлением потока звонков
        return $params;
    }
    
    public function OnAfterCallFlowUpdate($params, $result)
    {
        // Code executed after call flow is updated
        // Код, выполняемый после обновления потока звонков
        return $result;
    }
    
    public function OnBeforeCallFlowDelete($params)
    {
        // Code executed before call flow is deleted
        // Код, выполняемый перед удалением потока звонков
        return $params;
    }
    
    public function OnAfterCallFlowDelete($params, $result)
    {
        // Code executed after call flow is deleted
        // Код, выполняемый после удаления потока звонков
        return $result;
    }
    
    public function OnBeforeCallFlowExecute($params)
    {
        // Code executed before call flow is executed
        // Код, выполняемый перед выполнением потока звонков
        return $params;
    }
    
    public function OnAfterCallFlowExecute($params, $result)
    {
        // Code executed after call flow is executed
        // Код, выполняемый после выполнения потока звонков
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CVoximplantCallFlowHandler::Register('custom_call_flow', 'CCustomCallFlowHandler');
```

### CRM Integration Handlers | Обработчики интеграции с CRM

#### CRM Integration Handler | Обработчик интеграции с CRM

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
class CustomCrmIntegrationHandler extends \Bitrix\Voximplant\CrmIntegration\Handler
{
    public function onBeforeCrmLeadCreate($params)
    {
        // Code executed before CRM lead is created
        // Код, выполняемый перед созданием лида в CRM
        return $params;
    }
    
    public function onAfterCrmLeadCreate($params, $result)
    {
        // Code executed after CRM lead is created
        // Код, выполняемый после создания лида в CRM
        return $result;
    }
    
    public function onBeforeCrmContactCreate($params)
    {
        // Code executed before CRM contact is created
        // Код, выполняемый перед созданием контакта в CRM
        return $params;
    }
    
    public function onAfterCrmContactCreate($params, $result)
    {
        // Code executed after CRM contact is created
        // Код, выполняемый после создания контакта в CRM
        return $result;
    }
    
    public function onBeforeCrmDealCreate($params)
    {
        // Code executed before CRM deal is created
        // Код, выполняемый перед созданием сделки в CRM
        return $params;
    }
    
    public function onAfterCrmDealCreate($params, $result)
    {
        // Code executed after CRM deal is created
        // Код, выполняемый после создания сделки в CRM
        return $result;
    }
    
    public function onBeforeCrmActivityCreate($params)
    {
        // Code executed before CRM activity is created
        // Код, выполняемый перед созданием активности в CRM
        return $params;
    }
    
    public function onAfterCrmActivityCreate($params, $result)
    {
        // Code executed after CRM activity is created
        // Код, выполняемый после создания активности в CRM
        return $result;
    }
}

// Register handler
// Регистрация обработчика
\Bitrix\Voximplant\CrmIntegration\Handler::register('custom_crm_integration', CustomCrmIntegrationHandler::class);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
class CCustomCrmIntegrationHandler extends CVoximplantCrmIntegrationHandler
{
    public function OnBeforeCrmLeadCreate($params)
    {
        // Code executed before CRM lead is created
        // Код, выполняемый перед созданием лида в CRM
        return $params;
    }
    
    public function OnAfterCrmLeadCreate($params, $result)
    {
        // Code executed after CRM lead is created
        // Код, выполняемый после создания лида в CRM
        return $result;
    }
    
    public function OnBeforeCrmContactCreate($params)
    {
        // Code executed before CRM contact is created
        // Код, выполняемый перед созданием контакта в CRM
        return $params;
    }
    
    public function OnAfterCrmContactCreate($params, $result)
    {
        // Code executed after CRM contact is created
        // Код, выполняемый после создания контакта в CRM
        return $result;
    }
    
    public function OnBeforeCrmDealCreate($params)
    {
        // Code executed before CRM deal is created
        // Код, выполняемый перед созданием сделки в CRM
        return $params;
    }
    
    public function OnAfterCrmDealCreate($params, $result)
    {
        // Code executed after CRM deal is created
        // Код, выполняемый после создания сделки в CRM
        return $result;
    }
    
    public function OnBeforeCrmActivityCreate($params)
    {
        // Code executed before CRM activity is created
        // Код, выполняемый перед созданием активности в CRM
        return $params;
    }
    
    public function OnAfterCrmActivityCreate($params, $result)
    {
        // Code executed after CRM activity is created
        // Код, выполняемый после создания активности в CRM
        return $result;
    }
}

// Register handler
// Регистрация обработчика
CVoximplantCrmIntegrationHandler::Register('custom_crm_integration', 'CCustomCrmIntegrationHandler');
```

## REST API | REST API

### Call Management | Управление звонками

#### Start Call | Начало звонка

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Call::start([
    'USER_ID' => $USER->GetID(),
    'PHONE_NUMBER' => '+79001234567',
    'LINE_ID' => $lineId,
    'CALLER_ID' => $callerId,
    'CRM_ENTITY_TYPE' => 'LEAD',
    'CRM_ENTITY_ID' => $leadId
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoximplant::StartCall([
    'USER_ID' => $USER->GetID(),
    'PHONE_NUMBER' => '+79001234567',
    'LINE_ID' => $lineId,
    'CALLER_ID' => $callerId,
    'CRM_ENTITY_TYPE' => 'LEAD',
    'CRM_ENTITY_ID' => $leadId
]);
```

#### End Call | Завершение звонка

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Call::end($callId);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoximplant::EndCall($callId);
```

#### Transfer Call | Перенаправление звонка

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Call::transfer($callId, $userId);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoximplant::TransferCall($callId, $userId);
```

#### Record Call | Запись звонка

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Call::record($callId, true);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoximplant::RecordCall($callId, true);
```

### Line Management | Управление линиями

#### Create Line | Создание линии

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Line::add([
    'NAME' => 'Main Line',
    'DESCRIPTION' => 'Main phone line',
    'PHONE_NUMBER' => '+79001234567',
    'CALLER_ID' => $callerId,
    'ACTIVE' => 'Y'
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoximplant::AddLine([
    'NAME' => 'Main Line',
    'DESCRIPTION' => 'Main phone line',
    'PHONE_NUMBER' => '+79001234567',
    'CALLER_ID' => $callerId,
    'ACTIVE' => 'Y'
]);
```

#### Get Line | Получение линии

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$line = \Bitrix\Voximplant\Line::getById($lineId);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$line = CVoximplant::GetLine($lineId);
```

#### Update Line | Обновление линии

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Line::update($lineId, [
    'NAME' => 'Updated Line',
    'DESCRIPTION' => 'Updated phone line',
    'ACTIVE' => 'N'
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoximplant::UpdateLine($lineId, [
    'NAME' => 'Updated Line',
    'DESCRIPTION' => 'Updated phone line',
    'ACTIVE' => 'N'
]);
```

#### Delete Line | Удаление линии

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\Line::delete($lineId);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoximplant::DeleteLine($lineId);
```

### User Management | Управление пользователями

#### Assign User | Назначение пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\User::assign($userId, $lineId);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoximplant::AssignUser($userId, $lineId);
```

#### Unassign User | Отмена назначения пользователя

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\User::unassign($userId, $lineId);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoximplant::UnassignUser($userId, $lineId);
```

### Call Flow Management | Управление потоками звонков

#### Create Call Flow | Создание потока звонков

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\CallFlow::add([
    'NAME' => 'Main Flow',
    'DESCRIPTION' => 'Main call flow',
    'LINE_ID' => $lineId,
    'ACTIVE' => 'Y',
    'FLOW' => [
        'type' => 'menu',
        'options' => [
            'message' => 'Welcome to our company. Press 1 for sales, 2 for support.',
            'timeout' => 5,
            'retries' => 3,
            'items' => [
                [
                    'key' => '1',
                    'action' => 'transfer',
                    'params' => [
                        'user_id' => $salesUserId
                    ]
                ],
                [
                    'key' => '2',
                    'action' => 'transfer',
                    'params' => [
                        'user_id' => $supportUserId
                    ]
                ]
            ]
        ]
    ]
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoximplant::AddCallFlow([
    'NAME' => 'Main Flow',
    'DESCRIPTION' => 'Main call flow',
    'LINE_ID' => $lineId,
    'ACTIVE' => 'Y',
    'FLOW' => [
        'type' => 'menu',
        'options' => [
            'message' => 'Welcome to our company. Press 1 for sales, 2 for support.',
            'timeout' => 5,
            'retries' => 3,
            'items' => [
                [
                    'key' => '1',
                    'action' => 'transfer',
                    'params' => [
                        'user_id' => $salesUserId
                    ]
                ],
                [
                    'key' => '2',
                    'action' => 'transfer',
                    'params' => [
                        'user_id' => $supportUserId
                    ]
                ]
            ]
        ]
    ]
]);
```

#### Get Call Flow | Получение потока звонков

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$callFlow = \Bitrix\Voximplant\CallFlow::getById($callFlowId);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$callFlow = CVoximplant::GetCallFlow($callFlowId);
```

#### Update Call Flow | Обновление потока звонков

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\CallFlow::update($callFlowId, [
    'NAME' => 'Updated Flow',
    'DESCRIPTION' => 'Updated call flow',
    'ACTIVE' => 'N'
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoximplant::UpdateCallFlow($callFlowId, [
    'NAME' => 'Updated Flow',
    'DESCRIPTION' => 'Updated call flow',
    'ACTIVE' => 'N'
]);
```

#### Delete Call Flow | Удаление потока звонков

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\CallFlow::delete($callFlowId);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoximplant::DeleteCallFlow($callFlowId);
```

### CRM Integration | Интеграция с CRM

#### Create CRM Lead | Создание лида в CRM

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\CrmIntegration::createLead([
    'TITLE' => 'Call from ' . $phoneNumber,
    'NAME' => $name,
    'LAST_NAME' => $lastName,
    'PHONE' => [
        [
            'VALUE' => $phoneNumber,
            'VALUE_TYPE' => 'WORK'
        ]
    ],
    'COMMENTS' => 'Created from call',
    'SOURCE_ID' => 'CALL',
    'ASSIGNED_BY_ID' => $userId
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoximplant::CreateCrmLead([
    'TITLE' => 'Call from ' . $phoneNumber,
    'NAME' => $name,
    'LAST_NAME' => $lastName,
    'PHONE' => [
        [
            'VALUE' => $phoneNumber,
            'VALUE_TYPE' => 'WORK'
        ]
    ],
    'COMMENTS' => 'Created from call',
    'SOURCE_ID' => 'CALL',
    'ASSIGNED_BY_ID' => $userId
]);
```

#### Create CRM Activity | Создание активности в CRM

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('voximplant')
// Требуется: Bitrix\Main\Loader::includeModule('voximplant')
$result = \Bitrix\Voximplant\CrmIntegration::createActivity([
    'TYPE_ID' => 'CALL',
    'SUBJECT' => 'Call with ' . $phoneNumber,
    'START_TIME' => new \Bitrix\Main\Type\DateTime(),
    'END_TIME' => new \Bitrix\Main\Type\DateTime(),
    'COMPLETED' => 'N',
    'RESPONSIBLE_ID' => $userId,
    'PRIORITY' => 'NORMAL',
    'DESCRIPTION' => 'Call duration: 5 minutes',
    'DIRECTION' => 'INCOMING',
    'CALL_ID' => $callId,
    'PHONE_NUMBER' => $phoneNumber,
    'CRM_ENTITY_TYPE' => 'LEAD',
    'CRM_ENTITY_ID' => $leadId
]);

// Legacy
// Requires: CModule::IncludeModule('voximplant')
// Требуется: CModule::IncludeModule('voximplant')
$result = CVoximplant::CreateCrmActivity([
    'TYPE_ID' => 'CALL',
    'SUBJECT' => 'Call with ' . $phoneNumber,
    'START_TIME' => new \Bitrix\Main\Type\DateTime(),
    'END_TIME' => new \Bitrix\Main\Type\DateTime(),
    'COMPLETED' => 'N',
    'RESPONSIBLE_ID' => $userId,
    'PRIORITY' => 'NORMAL',
    'DESCRIPTION' => 'Call duration: 5 minutes',
    'DIRECTION' => 'INCOMING',
    'CALL_ID' => $callId,
    'PHONE_NUMBER' => $phoneNumber,
    'CRM_ENTITY_TYPE' => 'LEAD',
    'CRM_ENTITY_ID' => $leadId
]);
``` 