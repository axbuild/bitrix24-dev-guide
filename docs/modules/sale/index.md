# Sale Module | Модуль Магазина

## Overview | Обзор

The Sale module provides functionality for managing e-commerce operations in Bitrix24, including orders, payments, shipments, and price management. | Модуль Магазина предоставляет функциональность для управления операциями электронной коммерции в Bitrix24, включая заказы, платежи, доставку и управление ценами.

## Methods | Методы

### Orders | Заказы

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.order.list',
    [
        'filter' => ['CANCELED' => 'N'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$orders = \Bitrix\Sale\OrderTable::getList([
    'select' => ['*'],
    'filter' => ['=CANCELED' => 'N'],
    'order' => ['DATE_INSERT' => 'DESC'],
    'limit' => 50,
    'offset' => 0
]);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$orders = CSaleOrder::GetList(
    ['DATE_INSERT' => 'DESC'],
    ['CANCELED' => 'N'],
    false,
    ['nTopCount' => 50],
    ['*']
);
```

#### Get Order | Получение заказа

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.order.get',
    [
        'ID' => 123
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$order = \Bitrix\Sale\Order::load(123);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$order = CSaleOrder::GetByID(123);
```

#### Create Order | Создание заказа

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.order.add',
    [
        'fields' => [
            'ACCOUNT_NUMBER' => 'ORDER-001',
            'USER_ID' => 1,
            'PRICE' => 1000,
            'CURRENCY' => 'RUB',
            'STATUS_ID' => 'N',
            'PAYED' => 'N',
            'CANCELED' => 'N',
            'COMMENTS' => 'Order comment',
            'PERSON_TYPE_ID' => 1,
            'PAY_SYSTEM_ID' => 1,
            'DELIVERY_ID' => 1,
            'PRICE_DELIVERY' => 100,
            'DISCOUNT_VALUE' => 0,
            'DISCOUNT_NAME' => '',
            'TAX_VALUE' => 0,
            'USER_DESCRIPTION' => 'Customer comment',
            'ADDITIONAL_INFO' => '',
            'PS_STATUS' => 'N',
            'PS_STATUS_CODE' => '',
            'PS_STATUS_DESCRIPTION' => '',
            'PS_STATUS_MESSAGE' => '',
            'PS_SUM' => 0,
            'PS_CURRENCY' => '',
            'PS_RESPONSE_DATE' => '',
            'EMP_STATUS_ID' => 0,
            'EMP_CANCELED_ID' => 0,
            'EMP_MARKED_ID' => 0,
            'EMP_PAYED_ID' => 0,
            'EMP_DEDUCTED_ID' => 0,
            'TRACKING_NUMBER' => '',
            'XML_ID' => '',
            'PARAMS' => [],
            'PROPERTIES' => [
                'FIO' => 'John Doe',
                'PHONE' => '+1234567890',
                'EMAIL' => 'john@example.com',
                'ADDRESS' => '123 Main St'
            ]
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$order = \Bitrix\Sale\Order::create(SITE_ID, 1);
$order->setPersonTypeId(1);
$order->setPaySystemId(1);
$order->setDeliveryId(1);
$order->setPrice(1000);
$order->setCurrency('RUB');
$order->setUserId(1);

// Add properties
// Добавление свойств
$propertyCollection = $order->getPropertyCollection();
$propertyCollection->setValues([
    'FIO' => 'John Doe',
    'PHONE' => '+1234567890',
    'EMAIL' => 'john@example.com',
    'ADDRESS' => '123 Main St'
]);

$result = $order->save();

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$orderFields = [
    'ACCOUNT_NUMBER' => 'ORDER-001',
    'USER_ID' => 1,
    'PRICE' => 1000,
    'CURRENCY' => 'RUB',
    'STATUS_ID' => 'N',
    'PAYED' => 'N',
    'CANCELED' => 'N',
    'COMMENTS' => 'Order comment',
    'PERSON_TYPE_ID' => 1,
    'PAY_SYSTEM_ID' => 1,
    'DELIVERY_ID' => 1,
    'PRICE_DELIVERY' => 100,
    'DISCOUNT_VALUE' => 0,
    'DISCOUNT_NAME' => '',
    'TAX_VALUE' => 0,
    'USER_DESCRIPTION' => 'Customer comment',
    'ADDITIONAL_INFO' => '',
    'PS_STATUS' => 'N',
    'PS_STATUS_CODE' => '',
    'PS_STATUS_DESCRIPTION' => '',
    'PS_STATUS_MESSAGE' => '',
    'PS_SUM' => 0,
    'PS_CURRENCY' => '',
    'PS_RESPONSE_DATE' => '',
    'EMP_STATUS_ID' => 0,
    'EMP_CANCELED_ID' => 0,
    'EMP_MARKED_ID' => 0,
    'EMP_PAYED_ID' => 0,
    'EMP_DEDUCTED_ID' => 0,
    'TRACKING_NUMBER' => '',
    'XML_ID' => '',
    'PARAMS' => []
];
$orderId = CSaleOrder::Add($orderFields);

// Add properties
// Добавление свойств
if ($orderId) {
    $orderProps = [
        'ORDER_ID' => $orderId,
        'NAME' => 'FIO',
        'VALUE' => 'John Doe'
    ];
    CSaleOrderProps::Add($orderProps);
    
    $orderProps = [
        'ORDER_ID' => $orderId,
        'NAME' => 'PHONE',
        'VALUE' => '+1234567890'
    ];
    CSaleOrderProps::Add($orderProps);
    
    $orderProps = [
        'ORDER_ID' => $orderId,
        'NAME' => 'EMAIL',
        'VALUE' => 'john@example.com'
    ];
    CSaleOrderProps::Add($orderProps);
    
    $orderProps = [
        'ORDER_ID' => $orderId,
        'NAME' => 'ADDRESS',
        'VALUE' => '123 Main St'
    ];
    CSaleOrderProps::Add($orderProps);
}
```

#### Update Order | Обновление заказа

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.order.update',
    [
        'ID' => 123,
        'fields' => [
            'STATUS_ID' => 'P',
            'PAYED' => 'Y',
            'COMMENTS' => 'Updated comment'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$order = \Bitrix\Sale\Order::load(123);
$order->setField('STATUS_ID', 'P');
$order->setField('PAYED', 'Y');
$order->setField('COMMENTS', 'Updated comment');
$result = $order->save();

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$orderFields = [
    'STATUS_ID' => 'P',
    'PAYED' => 'Y',
    'COMMENTS' => 'Updated comment'
];
CSaleOrder::Update(123, $orderFields);
```

#### Delete Order | Удаление заказа

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.order.delete',
    ['ID' => 123]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$order = \Bitrix\Sale\Order::load(123);
$result = $order->delete();

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
CSaleOrder::Delete(123);
```

#### Get Order Statuses | Получение статусов заказа

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.order.status.list',
    []
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$statuses = \Bitrix\Sale\OrderStatus::getAllStatuses();

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$statuses = CSaleOrder::GetOrderStatuses();
```

### Payments | Платежи

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.payment.list',
    [
        'filter' => ['ORDER_ID' => 123],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$payments = \Bitrix\Sale\PaymentTable::getList([
    'select' => ['*'],
    'filter' => ['=ORDER_ID' => 123],
    'order' => ['DATE_INSERT' => 'DESC']
]);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$payments = CSalePayment::GetList(
    ['DATE_INSERT' => 'DESC'],
    ['ORDER_ID' => 123]
);
```

#### Get Payment | Получение платежа

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.payment.get',
    [
        'ID' => 456
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$payment = \Bitrix\Sale\Payment::load(456);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$payment = CSalePayment::GetByID(456);
```

#### Create Payment | Создание платежа

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.payment.add',
    [
        'fields' => [
            'ORDER_ID' => 123,
            'PAY_SYSTEM_ID' => 1,
            'PAY_SYSTEM_NAME' => 'Credit Card',
            'PAY_SYSTEM_ACTION' => 'pay',
            'PAY_VOUCHER_NUM' => '',
            'PAY_VOUCHER_DATE' => '',
            'DATE_PAID' => '',
            'EMP_PAID_ID' => 0,
            'PAY_RETURN_NUM' => '',
            'PAY_RETURN_DATE' => '',
            'EMP_RETURN_ID' => 0,
            'PRICE' => 1000,
            'CURRENCY' => 'RUB',
            'PAID' => 'N',
            'DATE_PAY_BEFORE' => '',
            'DATE_BILL' => '',
            'XML_ID' => '',
            'COMMENTS' => 'Payment comment'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$order = \Bitrix\Sale\Order::load(123);
$payment = \Bitrix\Sale\Payment::create($order);
$payment->setField('PAY_SYSTEM_ID', 1);
$payment->setField('PRICE', 1000);
$payment->setField('CURRENCY', 'RUB');
$result = $payment->save();

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$paymentFields = [
    'ORDER_ID' => 123,
    'PAY_SYSTEM_ID' => 1,
    'PAY_SYSTEM_NAME' => 'Credit Card',
    'PAY_SYSTEM_ACTION' => 'pay',
    'PRICE' => 1000,
    'CURRENCY' => 'RUB',
    'PAID' => 'N',
    'COMMENTS' => 'Payment comment'
];
$paymentId = CSalePayment::Add($paymentFields);
```

#### Update Payment | Обновление платежа

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.payment.update',
    [
        'ID' => 456,
        'fields' => [
            'PAID' => 'Y',
            'DATE_PAID' => new \Bitrix\Main\Type\DateTime(),
            'EMP_PAID_ID' => 1
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$payment = \Bitrix\Sale\Payment::load(456);
$payment->setPaid('Y');
$payment->setField('DATE_PAID', new \Bitrix\Main\Type\DateTime());
$payment->setField('EMP_PAID_ID', 1);
$result = $payment->save();

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$paymentFields = [
    'PAID' => 'Y',
    'DATE_PAID' => new \Bitrix\Main\Type\DateTime(),
    'EMP_PAID_ID' => 1
];
CSalePayment::Update(456, $paymentFields);
```

#### Delete Payment | Удаление платежа

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.payment.delete',
    ['ID' => 456]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$payment = \Bitrix\Sale\Payment::load(456);
$result = $payment->delete();

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
CSalePayment::Delete(456);
```

#### Get Payment Systems | Получение платежных систем

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.payment.system.list',
    []
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$paymentSystems = \Bitrix\Sale\PaySystem\Manager::getList([
    'filter' => ['ACTIVE' => 'Y']
]);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$paymentSystems = CSalePaySystem::GetList(
    ['SORT' => 'ASC', 'NAME' => 'ASC'],
    ['ACTIVE' => 'Y']
);
```

### Delivery | Доставка

#### Get Delivery | Получение доставки

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.delivery.get',
    [
        'ID' => 789
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$delivery = \Bitrix\Sale\Delivery\Services\Table::getList([
    'filter' => ['=ID' => 789]
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$delivery = CSaleDelivery::GetByID(789);
```

#### Create Delivery | Создание доставки

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.delivery.add',
    [
        'fields' => [
            'NAME' => 'Express Delivery',
            'ACTIVE' => 'Y',
            'SORT' => 100,
            'DESCRIPTION' => 'Express delivery service',
            'PRICE' => 500,
            'CURRENCY' => 'RUB',
            'PERIOD_FROM' => 1,
            'PERIOD_TO' => 2,
            'PERIOD_TYPE' => 'D',
            'WEIGHT_FROM' => 0,
            'WEIGHT_TO' => 1000,
            'ORDER_PRICE_FROM' => 0,
            'ORDER_PRICE_TO' => 100000,
            'ORDER_CURRENCY' => 'RUB',
            'ACTIVE' => 'Y',
            'PRICE_TYPE' => 'F',
            'SETTINGS' => [
                'CURRENCY' => 'RUB',
                'PRICE' => 500,
                'PERIOD' => [
                    'FROM' => 1,
                    'TO' => 2,
                    'TYPE' => 'D'
                ]
            ]
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$service = new \Bitrix\Sale\Delivery\Services\Configurable([
    'NAME' => 'Express Delivery',
    'ACTIVE' => 'Y',
    'SORT' => 100,
    'DESCRIPTION' => 'Express delivery service',
    'PRICE' => 500,
    'CURRENCY' => 'RUB',
    'PERIOD_FROM' => 1,
    'PERIOD_TO' => 2,
    'PERIOD_TYPE' => 'D',
    'WEIGHT_FROM' => 0,
    'WEIGHT_TO' => 1000,
    'ORDER_PRICE_FROM' => 0,
    'ORDER_PRICE_TO' => 100000,
    'ORDER_CURRENCY' => 'RUB',
    'PRICE_TYPE' => 'F',
    'SETTINGS' => [
        'CURRENCY' => 'RUB',
        'PRICE' => 500,
        'PERIOD' => [
            'FROM' => 1,
            'TO' => 2,
            'TYPE' => 'D'
        ]
    ]
]);
$result = $service->save();

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$deliveryFields = [
    'NAME' => 'Express Delivery',
    'ACTIVE' => 'Y',
    'SORT' => 100,
    'DESCRIPTION' => 'Express delivery service',
    'PRICE' => 500,
    'CURRENCY' => 'RUB',
    'PERIOD_FROM' => 1,
    'PERIOD_TO' => 2,
    'PERIOD_TYPE' => 'D',
    'WEIGHT_FROM' => 0,
    'WEIGHT_TO' => 1000,
    'ORDER_PRICE_FROM' => 0,
    'ORDER_PRICE_TO' => 100000,
    'ORDER_CURRENCY' => 'RUB',
    'PRICE_TYPE' => 'F',
    'SETTINGS' => [
        'CURRENCY' => 'RUB',
        'PRICE' => 500,
        'PERIOD' => [
            'FROM' => 1,
            'TO' => 2,
            'TYPE' => 'D'
        ]
    ]
];
$deliveryId = CSaleDelivery::Add($deliveryFields);
```

#### Update Delivery | Обновление доставки

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.delivery.update',
    [
        'ID' => 789,
        'fields' => [
            'NAME' => 'Updated Delivery',
            'PRICE' => 600,
            'DESCRIPTION' => 'Updated description'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$service = \Bitrix\Sale\Delivery\Services\Table::getList([
    'filter' => ['=ID' => 789]
])->fetch();

if ($service) {
    $service = new \Bitrix\Sale\Delivery\Services\Configurable($service);
    $service->setField('NAME', 'Updated Delivery');
    $service->setField('PRICE', 600);
    $service->setField('DESCRIPTION', 'Updated description');
    $result = $service->save();
}

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$deliveryFields = [
    'NAME' => 'Updated Delivery',
    'PRICE' => 600,
    'DESCRIPTION' => 'Updated description'
];
CSaleDelivery::Update(789, $deliveryFields);
```

#### Delete Delivery | Удаление доставки

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.delivery.delete',
    ['ID' => 789]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$service = \Bitrix\Sale\Delivery\Services\Table::getList([
    'filter' => ['=ID' => 789]
])->fetch();

if ($service) {
    $service = new \Bitrix\Sale\Delivery\Services\Configurable($service);
    $result = $service->delete();
}

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
CSaleDelivery::Delete(789);
```

#### Get Delivery Services | Получение служб доставки

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.delivery.service.list',
    []
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$deliveryServices = \Bitrix\Sale\Delivery\Services\Manager::getList([
    'filter' => ['ACTIVE' => 'Y']
]);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$deliveryServices = CSaleDelivery::GetList(
    ['SORT' => 'ASC', 'NAME' => 'ASC'],
    ['ACTIVE' => 'Y']
);
```

### Prices | Цены

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.product.price.list',
    [
        'filter' => ['PRODUCT_ID' => 123],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$prices = \Bitrix\Sale\PriceTable::getList([
    'select' => ['*'],
    'filter' => ['=PRODUCT_ID' => 123],
    'order' => ['SORT' => 'ASC']
]);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$prices = CSalePrice::GetList(
    ['SORT' => 'ASC'],
    ['PRODUCT_ID' => 123]
);
```

#### Get Price | Получение цены

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.product.price.get',
    [
        'ID' => 456
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$price = \Bitrix\Sale\PriceTable::getList([
    'filter' => ['=ID' => 456]
])->fetch();

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$price = CSalePrice::GetByID(456);
```

#### Create Price | Создание цены

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.product.price.add',
    [
        'fields' => [
            'PRODUCT_ID' => 123,
            'CATALOG_GROUP_ID' => 1,
            'PRICE' => 1000,
            'CURRENCY' => 'RUB',
            'QUANTITY_FROM' => 0,
            'QUANTITY_TO' => 0,
            'EXTRA_ID' => 0,
            'SORT' => 100
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$priceFields = [
    'PRODUCT_ID' => 123,
    'CATALOG_GROUP_ID' => 1,
    'PRICE' => 1000,
    'CURRENCY' => 'RUB',
    'QUANTITY_FROM' => 0,
    'QUANTITY_TO' => 0,
    'EXTRA_ID' => 0,
    'SORT' => 100
];
$result = \Bitrix\Sale\PriceTable::add($priceFields);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$priceFields = [
    'PRODUCT_ID' => 123,
    'CATALOG_GROUP_ID' => 1,
    'PRICE' => 1000,
    'CURRENCY' => 'RUB',
    'QUANTITY_FROM' => 0,
    'QUANTITY_TO' => 0,
    'EXTRA_ID' => 0,
    'SORT' => 100
];
$priceId = CSalePrice::Add($priceFields);
```

#### Update Price | Обновление цены

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.product.price.update',
    [
        'ID' => 456,
        'fields' => [
            'PRICE' => 1200,
            'CURRENCY' => 'RUB'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$priceFields = [
    'PRICE' => 1200,
    'CURRENCY' => 'RUB'
];
$result = \Bitrix\Sale\PriceTable::update(456, $priceFields);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$priceFields = [
    'PRICE' => 1200,
    'CURRENCY' => 'RUB'
];
CSalePrice::Update(456, $priceFields);
```

#### Delete Price | Удаление цены

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.product.price.delete',
    ['ID' => 456]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$result = \Bitrix\Sale\PriceTable::delete(456);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
CSalePrice::Delete(456);
```

#### Get Price Types | Получение типов цен

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.product.price.type.list',
    []
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$priceTypes = \Bitrix\Sale\PriceTypeTable::getList([
    'filter' => ['ACTIVE' => 'Y']
]);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$priceTypes = CSalePriceType::GetList(
    ['SORT' => 'ASC', 'NAME' => 'ASC'],
    ['ACTIVE' => 'Y']
);
```

### Discounts | Скидки

#### Get List | Получение списка

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.discount.list',
    [
        'filter' => ['ACTIVE' => 'Y'],
        'start' => 0
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$discounts = \Bitrix\Sale\DiscountTable::getList([
    'select' => ['*'],
    'filter' => ['=ACTIVE' => 'Y'],
    'order' => ['SORT' => 'ASC', 'NAME' => 'ASC']
]);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$discounts = CSaleDiscount::GetList(
    ['SORT' => 'ASC', 'NAME' => 'ASC'],
    ['ACTIVE' => 'Y']
);
```

#### Add | Добавление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.discount.add',
    [
        'fields' => [
            'NAME' => 'Summer Sale',
            'ACTIVE' => 'Y',
            'SORT' => 100,
            'ACTIVE_FROM' => new \Bitrix\Main\Type\DateTime(),
            'ACTIVE_TO' => new \Bitrix\Main\Type\DateTime('2023-08-31 23:59:59'),
            'PRIORITY' => 1,
            'LAST_DISCOUNT' => 'N',
            'CONDITIONS' => [
                'CLASS_ID' => 'CondGroup',
                'DATA' => [
                    'All' => 'AND',
                    'True' => 'True'
                ],
                'CHILDREN' => []
            ],
            'ACTIONS' => [
                'CLASS_ID' => 'CondGroup',
                'DATA' => [
                    'Type' => 'Discount',
                    'Value' => 10
                ],
                'CHILDREN' => []
            ],
            'APPLICATION' => 'All',
            'USE_COUPONS' => 'N',
            'COUPON' => '',
            'COUPON_ONE_TIME' => 'Y',
            'COUPON_ACTIVE' => 'Y'
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$discountFields = [
    'NAME' => 'Summer Sale',
    'ACTIVE' => 'Y',
    'SORT' => 100,
    'ACTIVE_FROM' => new \Bitrix\Main\Type\DateTime(),
    'ACTIVE_TO' => new \Bitrix\Main\Type\DateTime('2023-08-31 23:59:59'),
    'PRIORITY' => 1,
    'LAST_DISCOUNT' => 'N',
    'CONDITIONS' => [
        'CLASS_ID' => 'CondGroup',
        'DATA' => [
            'All' => 'AND',
            'True' => 'True'
        ],
        'CHILDREN' => []
    ],
    'ACTIONS' => [
        'CLASS_ID' => 'CondGroup',
        'DATA' => [
            'Type' => 'Discount',
            'Value' => 10
        ],
        'CHILDREN' => []
    ],
    'APPLICATION' => 'All',
    'USE_COUPONS' => 'N',
    'COUPON' => '',
    'COUPON_ONE_TIME' => 'Y',
    'COUPON_ACTIVE' => 'Y'
];
$result = \Bitrix\Sale\DiscountTable::add($discountFields);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$discountFields = [
    'NAME' => 'Summer Sale',
    'ACTIVE' => 'Y',
    'SORT' => 100,
    'ACTIVE_FROM' => new \Bitrix\Main\Type\DateTime(),
    'ACTIVE_TO' => new \Bitrix\Main\Type\DateTime('2023-08-31 23:59:59'),
    'PRIORITY' => 1,
    'LAST_DISCOUNT' => 'N',
    'CONDITIONS' => [
        'CLASS_ID' => 'CondGroup',
        'DATA' => [
            'All' => 'AND',
            'True' => 'True'
        ],
        'CHILDREN' => []
    ],
    'ACTIONS' => [
        'CLASS_ID' => 'CondGroup',
        'DATA' => [
            'Type' => 'Discount',
            'Value' => 10
        ],
        'CHILDREN' => []
    ],
    'APPLICATION' => 'All',
    'USE_COUPONS' => 'N',
    'COUPON' => '',
    'COUPON_ONE_TIME' => 'Y',
    'COUPON_ACTIVE' => 'Y'
];
$discountId = CSaleDiscount::Add($discountFields);
```

#### Update | Обновление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.discount.update',
    [
        'ID' => 789,
        'fields' => [
            'NAME' => 'Updated Summer Sale',
            'ACTIVE_TO' => new \Bitrix\Main\Type\DateTime('2023-09-30 23:59:59'),
            'ACTIONS' => [
                'CLASS_ID' => 'CondGroup',
                'DATA' => [
                    'Type' => 'Discount',
                    'Value' => 15
                ],
                'CHILDREN' => []
            ]
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$discountFields = [
    'NAME' => 'Updated Summer Sale',
    'ACTIVE_TO' => new \Bitrix\Main\Type\DateTime('2023-09-30 23:59:59'),
    'ACTIONS' => [
        'CLASS_ID' => 'CondGroup',
        'DATA' => [
            'Type' => 'Discount',
            'Value' => 15
        ],
        'CHILDREN' => []
    ]
];
$result = \Bitrix\Sale\DiscountTable::update(789, $discountFields);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$discountFields = [
    'NAME' => 'Updated Summer Sale',
    'ACTIVE_TO' => new \Bitrix\Main\Type\DateTime('2023-09-30 23:59:59'),
    'ACTIONS' => [
        'CLASS_ID' => 'CondGroup',
        'DATA' => [
            'Type' => 'Discount',
            'Value' => 15
        ],
        'CHILDREN' => []
    ]
];
CSaleDiscount::Update(789, $discountFields);
```

#### Delete | Удаление

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.discount.delete',
    ['ID' => 789]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$result = \Bitrix\Sale\DiscountTable::delete(789);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
CSaleDiscount::Delete(789);
```

### Shopping Cart | Корзина

#### Get Cart | Получение корзины

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.cart.get',
    [
        'USER_ID' => 1
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$basket = \Bitrix\Sale\Basket::loadItemsForFUser(
    \Bitrix\Sale\Fuser::getId(),
    SITE_ID
);

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$basket = CSaleBasket::GetList(
    ['ID' => 'ASC'],
    ['FUSER_ID' => CSaleBasket::GetBasketUserID()]
);
```

#### Add to Cart | Добавление в корзину

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.cart.add',
    [
        'fields' => [
            'PRODUCT_ID' => 123,
            'QUANTITY' => 1,
            'PRICE' => 1000,
            'CURRENCY' => 'RUB',
            'NAME' => 'Product Name',
            'PROPS' => [
                'COLOR' => 'Red',
                'SIZE' => 'M'
            ]
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$basket = \Bitrix\Sale\Basket::create(SITE_ID);
$item = $basket->createBasketItem();
$item->setFields([
    'PRODUCT_ID' => 123,
    'QUANTITY' => 1,
    'PRICE' => 1000,
    'CURRENCY' => 'RUB',
    'NAME' => 'Product Name',
    'PROPS' => [
        [
            'NAME' => 'COLOR',
            'VALUE' => 'Red',
            'CODE' => 'COLOR'
        ],
        [
            'NAME' => 'SIZE',
            'VALUE' => 'M',
            'CODE' => 'SIZE'
        ]
    ]
]);
$result = $item->save();

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$basketFields = [
    'PRODUCT_ID' => 123,
    'QUANTITY' => 1,
    'PRICE' => 1000,
    'CURRENCY' => 'RUB',
    'NAME' => 'Product Name',
    'FUSER_ID' => CSaleBasket::GetBasketUserID(),
    'LID' => SITE_ID
];
$basketId = CSaleBasket::Add($basketFields);

// Add properties
// Добавление свойств
if ($basketId) {
    $basketProps = [
        'BASKET_ID' => $basketId,
        'NAME' => 'COLOR',
        'VALUE' => 'Red',
        'CODE' => 'COLOR'
    ];
    CSaleBasketProps::Add($basketProps);
    
    $basketProps = [
        'BASKET_ID' => $basketId,
        'NAME' => 'SIZE',
        'VALUE' => 'M',
        'CODE' => 'SIZE'
    ];
    CSaleBasketProps::Add($basketProps);
}
```

#### Update Cart Item | Обновление элемента корзины

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.cart.update',
    [
        'ID' => 456,
        'fields' => [
            'QUANTITY' => 2,
            'PRICE' => 950
        ]
    ]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$basket = \Bitrix\Sale\Basket::loadItemsForFUser(
    \Bitrix\Sale\Fuser::getId(),
    SITE_ID
);
$item = $basket->getItemById(456);
if ($item) {
    $item->setField('QUANTITY', 2);
    $item->setField('PRICE', 950);
    $result = $item->save();
}

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$basketFields = [
    'QUANTITY' => 2,
    'PRICE' => 950
];
CSaleBasket::Update(456, $basketFields);
```

#### Delete from Cart | Удаление из корзины

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.cart.delete',
    ['ID' => 456]
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$basket = \Bitrix\Sale\Basket::loadItemsForFUser(
    \Bitrix\Sale\Fuser::getId(),
    SITE_ID
);
$item = $basket->getItemById(456);
if ($item) {
    $result = $item->delete();
}

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
CSaleBasket::Delete(456);
```

#### Clear Cart | Очистка корзины

```php
// REST API
// Requires: CRest::Init() with proper credentials
// Требуется: CRest::Init() с правильными учетными данными
$result = CRest::call(
    'crm.cart.clear',
    []
);

// D7
// Requires: Bitrix\Main\Loader::includeModule('sale')
// Требуется: Bitrix\Main\Loader::includeModule('sale')
$basket = \Bitrix\Sale\Basket::loadItemsForFUser(
    \Bitrix\Sale\Fuser::getId(),
    SITE_ID
);
$result = $basket->clear();

// Legacy
// Requires: CModule::IncludeModule('sale')
// Требуется: CModule::IncludeModule('sale')
$basketItems = CSaleBasket::GetList(
    ['ID' => 'ASC'],
    ['FUSER_ID' => CSaleBasket::GetBasketUserID()]
);
while ($basketItem = $basketItems->Fetch()) {
    CSaleBasket::Delete($basketItem['ID']);
}
``` 