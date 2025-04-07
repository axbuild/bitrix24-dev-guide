# Form Module | Модуль Формы

## Overview | Обзор

The Form module provides functionality for creating and managing web forms in Bitrix24, including form fields, validation, and submission handling. | Модуль Формы предоставляет функциональность для создания и управления веб-формами в Bitrix24, включая поля форм, валидацию и обработку отправки.

## Methods | Методы

### Forms | Формы

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'form.get',
    [
        'filter' => ['ACTIVE' => 'Y'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('form')
// Требуется: Bitrix\Main\Loader::includeModule('form')
$forms = \Bitrix\Form\FormTable::getList([
    'select' => ['*'],
    'filter' => ['=ACTIVE' => 'Y'],
    'order' => ['SORT' => 'ASC', 'NAME' => 'ASC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('form')
// Требуется: CModule::IncludeModule('form')
$forms = CForm::GetList(
    ['SORT' => 'ASC', 'NAME' => 'ASC'],
    ['ACTIVE' => 'Y'],
    false,
    ['nTopCount' => 50],
    ['*']
);
```

#### Add | Добавление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'form.add',
    [
        'fields' => [
            'NAME' => 'New Form',
            'SID' => 'NEW_FORM',
            'DESCRIPTION' => 'Form description',
            'SORT' => 500,
            'C_SITE' => ['s1'],
            'BUTTON' => 'Submit',
            'USE_CAPTCHA' => 'N',
            'SHOW_TEMPLATE' => 'Y',
            'SHOW_RESULT_TEMPLATE' => 'Y',
            'MAIL_EVENT_TYPE' => 'FORM_FILLING_NEW_FORM',
            'MAIL_EVENT_MESSAGE' => ['ACTIVE' => 'Y', 'EVENT_NAME' => 'FORM_FILLING_NEW_FORM', 'LID' => ['s1'], 'EMAIL_FROM' => '#DEFAULT_EMAIL_FROM#', 'EMAIL_TO' => '#EMAIL_TO#', 'SUBJECT' => 'New form submission', 'MESSAGE' => 'New form submission from #SITE_NAME#\n\nForm: #FORM_NAME#\n\n#ALL_RESULT#\n\nThis message was sent from the form on the site #SITE_NAME# (#SERVER_NAME#)']
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('form')
// Требуется: Bitrix\Main\Loader::includeModule('form')
$result = \Bitrix\Form\FormTable::add([
    'NAME' => 'New Form',
    'SID' => 'NEW_FORM',
    'DESCRIPTION' => 'Form description',
    'SORT' => 500,
    'C_SITE' => ['s1'],
    'BUTTON' => 'Submit',
    'USE_CAPTCHA' => 'N',
    'SHOW_TEMPLATE' => 'Y',
    'SHOW_RESULT_TEMPLATE' => 'Y',
    'MAIL_EVENT_TYPE' => 'FORM_FILLING_NEW_FORM',
    'MAIL_EVENT_MESSAGE' => ['ACTIVE' => 'Y', 'EVENT_NAME' => 'FORM_FILLING_NEW_FORM', 'LID' => ['s1'], 'EMAIL_FROM' => '#DEFAULT_EMAIL_FROM#', 'EMAIL_TO' => '#EMAIL_TO#', 'SUBJECT' => 'New form submission', 'MESSAGE' => 'New form submission from #SITE_NAME#\n\nForm: #FORM_NAME#\n\n#ALL_RESULT#\n\nThis message was sent from the form on the site #SITE_NAME# (#SERVER_NAME#)']
]);

// Legacy
// Requires: CModule::IncludeModule('form')
// Требуется: CModule::IncludeModule('form')
$formFields = [
    'NAME' => 'New Form',
    'SID' => 'NEW_FORM',
    'DESCRIPTION' => 'Form description',
    'SORT' => 500,
    'C_SITE' => ['s1'],
    'BUTTON' => 'Submit',
    'USE_CAPTCHA' => 'N',
    'SHOW_TEMPLATE' => 'Y',
    'SHOW_RESULT_TEMPLATE' => 'Y',
    'MAIL_EVENT_TYPE' => 'FORM_FILLING_NEW_FORM',
    'MAIL_EVENT_MESSAGE' => ['ACTIVE' => 'Y', 'EVENT_NAME' => 'FORM_FILLING_NEW_FORM', 'LID' => ['s1'], 'EMAIL_FROM' => '#DEFAULT_EMAIL_FROM#', 'EMAIL_TO' => '#EMAIL_TO#', 'SUBJECT' => 'New form submission', 'MESSAGE' => 'New form submission from #SITE_NAME#\n\nForm: #FORM_NAME#\n\n#ALL_RESULT#\n\nThis message was sent from the form on the site #SITE_NAME# (#SERVER_NAME#)']
];
$formId = CForm::Add($formFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'form.update',
    [
        'ID' => 123,
        'fields' => [
            'NAME' => 'Updated Form',
            'DESCRIPTION' => 'Updated description',
            'USE_CAPTCHA' => 'Y'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('form')
// Требуется: Bitrix\Main\Loader::includeModule('form')
$result = \Bitrix\Form\FormTable::update(123, [
    'NAME' => 'Updated Form',
    'DESCRIPTION' => 'Updated description',
    'USE_CAPTCHA' => 'Y'
]);

// Legacy
// Requires: CModule::IncludeModule('form')
// Требуется: CModule::IncludeModule('form')
$formFields = [
    'NAME' => 'Updated Form',
    'DESCRIPTION' => 'Updated description',
    'USE_CAPTCHA' => 'Y'
];
CForm::Set($formFields, 123);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'form.delete',
    ['ID' => 123]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('form')
// Требуется: Bitrix\Main\Loader::includeModule('form')
$result = \Bitrix\Form\FormTable::delete(123);

// Legacy
// Requires: CModule::IncludeModule('form')
// Требуется: CModule::IncludeModule('form')
CForm::Delete(123);
```

### Form Fields | Поля форм

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'form.field.get',
    [
        'formId' => 123,
        'filter' => ['ACTIVE' => 'Y'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('form')
// Требуется: Bitrix\Main\Loader::includeModule('form')
$fields = \Bitrix\Form\FieldTable::getList([
    'select' => ['*'],
    'filter' => ['=FORM_ID' => 123, '=ACTIVE' => 'Y'],
    'order' => ['SORT' => 'ASC', 'NAME' => 'ASC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('form')
// Требуется: CModule::IncludeModule('form')
$fields = CFormField::GetList(
    123,
    ['SORT' => 'ASC', 'NAME' => 'ASC'],
    ['ACTIVE' => 'Y'],
    false,
    ['nTopCount' => 50],
    ['*']
);
```

#### Add | Добавление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'form.field.add',
    [
        'formId' => 123,
        'fields' => [
            'TITLE' => 'New Field',
            'SID' => 'NEW_FIELD',
            'FIELD_TYPE' => 'text',
            'REQUIRED' => 'Y',
            'SORT' => 500,
            'COMMENTS' => 'Field description',
            'VALIDATION' => ['PATTERN' => '', 'MIN_LENGTH' => 0, 'MAX_LENGTH' => 0],
            'SETTINGS' => ['SIZE' => 30, 'MAX_LENGTH' => 0, 'DEFAULT_VALUE' => '']
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('form')
// Требуется: Bitrix\Main\Loader::includeModule('form')
$result = \Bitrix\Form\FieldTable::add([
    'FORM_ID' => 123,
    'TITLE' => 'New Field',
    'SID' => 'NEW_FIELD',
    'FIELD_TYPE' => 'text',
    'REQUIRED' => 'Y',
    'SORT' => 500,
    'COMMENTS' => 'Field description',
    'VALIDATION' => ['PATTERN' => '', 'MIN_LENGTH' => 0, 'MAX_LENGTH' => 0],
    'SETTINGS' => ['SIZE' => 30, 'MAX_LENGTH' => 0, 'DEFAULT_VALUE' => '']
]);

// Legacy
// Requires: CModule::IncludeModule('form')
// Требуется: CModule::IncludeModule('form')
$fieldFields = [
    'FORM_ID' => 123,
    'TITLE' => 'New Field',
    'SID' => 'NEW_FIELD',
    'FIELD_TYPE' => 'text',
    'REQUIRED' => 'Y',
    'SORT' => 500,
    'COMMENTS' => 'Field description',
    'VALIDATION' => ['PATTERN' => '', 'MIN_LENGTH' => 0, 'MAX_LENGTH' => 0],
    'SETTINGS' => ['SIZE' => 30, 'MAX_LENGTH' => 0, 'DEFAULT_VALUE' => '']
];
$fieldId = CFormField::Add($fieldFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'form.field.update',
    [
        'formId' => 123,
        'fieldId' => 456,
        'fields' => [
            'TITLE' => 'Updated Field',
            'REQUIRED' => 'N',
            'COMMENTS' => 'Updated description'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('form')
// Требуется: Bitrix\Main\Loader::includeModule('form')
$result = \Bitrix\Form\FieldTable::update(456, [
    'TITLE' => 'Updated Field',
    'REQUIRED' => 'N',
    'COMMENTS' => 'Updated description'
]);

// Legacy
// Requires: CModule::IncludeModule('form')
// Требуется: CModule::IncludeModule('form')
$fieldFields = [
    'TITLE' => 'Updated Field',
    'REQUIRED' => 'N',
    'COMMENTS' => 'Updated description'
];
CFormField::Set($fieldFields, 456);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'form.field.delete',
    [
        'formId' => 123,
        'fieldId' => 456
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('form')
// Требуется: Bitrix\Main\Loader::includeModule('form')
$result = \Bitrix\Form\FieldTable::delete(456);

// Legacy
// Requires: CModule::IncludeModule('form')
// Требуется: CModule::IncludeModule('form')
CFormField::Delete(456);
```

### Form Results | Результаты форм

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'form.result.get',
    [
        'formId' => 123,
        'filter' => ['STATUS_ID' => 'FORM_STATUS_1'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('form')
// Требуется: Bitrix\Main\Loader::includeModule('form')
$results = \Bitrix\Form\ResultTable::getList([
    'select' => ['*'],
    'filter' => ['=FORM_ID' => 123, '=STATUS_ID' => 'FORM_STATUS_1'],
    'order' => ['DATE_CREATE' => 'DESC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('form')
// Требуется: CModule::IncludeModule('form')
$results = CFormResult::GetList(
    123,
    ['DATE_CREATE' => 'DESC'],
    ['STATUS_ID' => 'FORM_STATUS_1'],
    false,
    ['nTopCount' => 50],
    ['*']
);
```

#### Add | Добавление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'form.result.add',
    [
        'formId' => 123,
        'fields' => [
            'STATUS_ID' => 'FORM_STATUS_1',
            'USER_ID' => 1,
            'STAT_GUEST_ID' => 0,
            'STAT_SESSION_ID' => '',
            'IP' => $_SERVER['REMOTE_ADDR'],
            'DATE_CREATE' => new \Bitrix\Main\Type\DateTime(),
            'DATE_UPDATE' => new \Bitrix\Main\Type\DateTime(),
            'ANSWERS' => [
                'NEW_FIELD' => 'Field value'
            ]
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('form')
// Требуется: Bitrix\Main\Loader::includeModule('form')
$result = \Bitrix\Form\ResultTable::add([
    'FORM_ID' => 123,
    'STATUS_ID' => 'FORM_STATUS_1',
    'USER_ID' => 1,
    'STAT_GUEST_ID' => 0,
    'STAT_SESSION_ID' => '',
    'IP' => $_SERVER['REMOTE_ADDR'],
    'DATE_CREATE' => new \Bitrix\Main\Type\DateTime(),
    'DATE_UPDATE' => new \Bitrix\Main\Type\DateTime()
]);

// Add answers
// Добавление ответов
if ($result->isSuccess()) {
    $resultId = $result->getId();
    \Bitrix\Form\AnswerTable::add([
        'RESULT_ID' => $resultId,
        'FIELD_ID' => 456,
        'ANSWER_TEXT' => 'Field value'
    ]);
}

// Legacy
// Requires: CModule::IncludeModule('form')
// Требуется: CModule::IncludeModule('form')
$resultFields = [
    'FORM_ID' => 123,
    'STATUS_ID' => 'FORM_STATUS_1',
    'USER_ID' => 1,
    'STAT_GUEST_ID' => 0,
    'STAT_SESSION_ID' => '',
    'IP' => $_SERVER['REMOTE_ADDR'],
    'DATE_CREATE' => new \Bitrix\Main\Type\DateTime(),
    'DATE_UPDATE' => new \Bitrix\Main\Type\DateTime()
];
$resultId = CFormResult::Add($resultFields);

// Add answers
// Добавление ответов
if ($resultId) {
    CFormAnswer::Add([
        'RESULT_ID' => $resultId,
        'FIELD_ID' => 456,
        'ANSWER_TEXT' => 'Field value'
    ]);
}
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'form.result.update',
    [
        'formId' => 123,
        'resultId' => 456,
        'fields' => [
            'STATUS_ID' => 'FORM_STATUS_2',
            'ANSWERS' => [
                'NEW_FIELD' => 'Updated field value'
            ]
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('form')
// Требуется: Bitrix\Main\Loader::includeModule('form')
$result = \Bitrix\Form\ResultTable::update(456, [
    'STATUS_ID' => 'FORM_STATUS_2'
]);

// Update answers
// Обновление ответов
$answers = \Bitrix\Form\AnswerTable::getList([
    'select' => ['ID'],
    'filter' => ['=RESULT_ID' => 456, '=FIELD_ID' => 789],
    'limit' => 1
])->fetch();

if ($answers) {
    \Bitrix\Form\AnswerTable::update($answers['ID'], [
        'ANSWER_TEXT' => 'Updated field value'
    ]);
}

// Legacy
// Requires: CModule::IncludeModule('form')
// Требуется: CModule::IncludeModule('form')
$resultFields = [
    'STATUS_ID' => 'FORM_STATUS_2'
];
CFormResult::Set($resultFields, 456);

// Update answers
// Обновление ответов
$answers = CFormAnswer::GetList(456, ['FIELD_ID' => 789]);
if ($answer = $answers->GetNext()) {
    CFormAnswer::Set([
        'ANSWER_TEXT' => 'Updated field value'
    ], $answer['ID']);
}
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'form.result.delete',
    [
        'formId' => 123,
        'resultId' => 456
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('form')
// Требуется: Bitrix\Main\Loader::includeModule('form')
$result = \Bitrix\Form\ResultTable::delete(456);

// Legacy
// Requires: CModule::IncludeModule('form')
// Требуется: CModule::IncludeModule('form')
CFormResult::Delete(456);
```

### Form Display | Отображение форм

#### Show Form | Показать форму

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('form')
// Требуется: Bitrix\Main\Loader::includeModule('form')
$APPLICATION->IncludeComponent(
    'bitrix:form',
    '',
    [
        'WEB_FORM_ID' => 123,
        'AJAX_MODE' => 'Y',
        'AJAX_OPTION_SHADOW' => 'N',
        'AJAX_OPTION_JUMP' => 'N',
        'AJAX_OPTION_STYLE' => 'Y',
        'AJAX_OPTION_HISTORY' => 'N'
    ]
);

// Legacy
// Requires: CModule::IncludeModule('form')
// Требуется: CModule::IncludeModule('form')
$APPLICATION->IncludeComponent(
    'bitrix:form',
    '',
    [
        'WEB_FORM_ID' => 123,
        'AJAX_MODE' => 'Y',
        'AJAX_OPTION_SHADOW' => 'N',
        'AJAX_OPTION_JUMP' => 'N',
        'AJAX_OPTION_STYLE' => 'Y',
        'AJAX_OPTION_HISTORY' => 'N'
    ]
);
```

#### Show Results | Показать результаты

```php
// D7
// Requires: Bitrix\Main\Loader::includeModule('form')
// Требуется: Bitrix\Main\Loader::includeModule('form')
$APPLICATION->IncludeComponent(
    'bitrix:form.result.list',
    '',
    [
        'WEB_FORM_ID' => 123,
        'AJAX_MODE' => 'Y',
        'AJAX_OPTION_SHADOW' => 'N',
        'AJAX_OPTION_JUMP' => 'N',
        'AJAX_OPTION_STYLE' => 'Y',
        'AJAX_OPTION_HISTORY' => 'N'
    ]
);

// Legacy
// Requires: CModule::IncludeModule('form')
// Требуется: CModule::IncludeModule('form')
$APPLICATION->IncludeComponent(
    'bitrix:form.result.list',
    '',
    [
        'WEB_FORM_ID' => 123,
        'AJAX_MODE' => 'Y',
        'AJAX_OPTION_SHADOW' => 'N',
        'AJAX_OPTION_JUMP' => 'N',
        'AJAX_OPTION_STYLE' => 'Y',
        'AJAX_OPTION_HISTORY' => 'N'
    ]
);
``` 