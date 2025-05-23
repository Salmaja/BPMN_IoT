## Контекст проекта

### Проблема и цель

Современные системы умного дома состоят из множества устройств (датчики, исполнительные устройства, шлюзы), которые генерируют события и требуют сложной логики взаимодействия. Традиционные подходы (жестко закодированные сценарии в прошивках или облачных сервисах) плохо масштабируются и усложняют поддержку.

Цель проекта — разработать гибкую систему управления IoT-процессами умного дома на основе BPMN 2.0, позволяющую:

* Визуально проектировать сценарии (например, автоматизацию освещения или климат-контроля).
* Динамически менять логику без перепрограммирования устройств.
* Обеспечивать мониторинг и обработку ошибок на уровне бизнес-процессов.

### Ключевые пользователи и потребности
| Роль	| Потребности | 
|---|---|
| Домовладелец | Удобное управление устройствами, автоматизация рутинных сценариев (например, включение света при движении) |
| Разработчик IoT |	Гибкий API для интеграции новых устройств, отладка процессов |
| Администратор системы | Мониторинг состояния устройств, обработка сбоев (например, потеря связи с датчиком) |


### Технологический стек
BPMN-движок: Camunda (open-source, поддержка сложных сценариев).

Протокол связи: MQTT (легковесный, идеален для IoT).

Эмуляция устройств: Python + библиотека paho-mqtt.

Развертывание: Docker (изоляция Camunda, Mosquitto и эмуляторов).

### Входы и выходы системы
#### Входы:

1. События от датчиков (температура, движение, освещенность).
2. Команды пользователя (через мобильное приложение или голосового ассистента).

#### Выходы:

1. Управляющие сигналы на устройства (включить свет, изменить температуру).
2. Уведомления пользователю (Telegram, email, пуш).

### Интеграции
Внутренние:

1. MQTT-брокер (Mosquitto) — центральный хаб для событий.
2. Camunda — исполнение BPMN-процессов.

Внешние (опционально):

1. Алиса (голосовое управление).
2. Облачные сервисы (например, погодный API для прогнозирования температуры или закатов/рассветов).

### Ограничения
Аппаратные: Проект использует эмуляцию устройств, но должен работать с реальными ESP32/Raspberry Pi.
Безопасность: Данные MQTT передаются без шифрования (в реальной системе требуется TLS).
Производительность: Camunda не оптимизирован для high-load IoT-сценариев (альтернатива — Kafka + микросервисы).

### Бизнес-контекст
Применение: Управление умными домами, офисами, промышленными IoT-системами (в рамках пета не применимо)

Конкуренты:

Готовые платформы (Home Assistant, OpenHAB) — менее гибкие в сложной автоматизации.

Проприетарные решения (Samsung SmartThings) — привязка к экосистеме.

Уникальность: Декларативное описание процессов через BPMN вместо программирования.


### Почему BPMN?
Наглядность: Сценарии видны даже нетехническим специалистам.

Гибкость: Изменение логики без перезапуска системы.

Отказоустойчивость: Встроенные в BPMN механизмы обработки ошибок (например, резервные сценарии при недоступности устройства).

### Перспективы развития (не для пета)
Добавление AI-аналитики (предсказание действий пользователя).

Поддержка Edge Computing (запуск процессов прямо на шлюзах, например, Node-RED).

Масштабирование на умные города (управление уличным освещением, парковками).

### Итог
Проект превращает набор IoT-устройств в единую управляемую систему с прозрачной логикой, которую можно адаптировать под любые сценарии. В отличие от готовых решений, он дает полный контроль над процессами и интеграциями.


### Ограничения для пета
Поскольку спектр уведомлений и управления достаточно велик, а проект всего лишь тестовый, то можно ограничим контекст:
1. Освещение, которое выключается в определённое время
2. Шторы, которые открываются вместе со срабатыванием будильника
3. Повышение и понижение температуры, когда можно включить/выключить кондиционер
4. Настройки - опционально

