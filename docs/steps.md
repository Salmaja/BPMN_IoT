### Этапы проекта

1. Настройка окружения
    1. Docker
    2. Camunda
    3. Python

2. Анализ требований
    1. Определить сценарии использования: управление светом, температурой, безопасностью
    2. Выделить ключевые события (например: «Температура > 25°C» → включить кондиционер)
    3. Составить список MQTT-топиков для устройств

3. Создать end-to-end процесс в Camunda Modeler:
    
    - Стартовые события: срабатывание датчиков (MQTT-сообщения).
        
    - Шлюзы: обработка условий (например: «Если свет выключен → отправить уведомление»).
        
    - Задачи: отправка команд на устройства через MQTT.
        
    - Использовать **Message Flow** для связи с внешними системами.
         
4. **Настройка MQTT-брокера** (1 день)

- Развернуть локальный брокер (Mosquitto/Eclipse Mosquitto).
    
- Создать топики:
    
    - `home/+/status` (для данных с датчиков).
        
    - `home/+/control` (для управляющих команд).

5. **Эмуляция IoT-устройств на Python** (2 дня)

- Написать скрипты:
    
    - **Даччик температуры:** Публикует случайные значения в `home/sensor/temp/status` каждые 5 сек.
        
    - **Умный свет:** Подписывается на `home/light/control`, меняет состояние (ON/OFF).
        
- Использовать библиотеку **paho-mqtt**: [![pypi.org](https://favicon.yandex.net/favicon/v2/pypi.org/?size=32&stub=1)pypi.org](https://pypi.org/project/paho-mqtt/).

**Интеграция Camunda с MQTT** (3 дня)

- Реализовать **Camunda-коннектор** для обработки MQTT-событий:
    
    - **Входные события:** Подписка на `home/+/status` → запуск процесса.
        
    - **Сервисные задачи:** Отправка команд в `home/+/control` через REST-API Camunda.
        
- Использовать **Camunda REST API**: [![docs.camunda.org](https://favicon.yandex.net/favicon/v2/docs.camunda.org/?size=32&stub=1)docs.camunda.org](https://docs.camunda.org/manual/7.17/reference/rest/).
    
**Симуляция процессов в Camunda** (2 дня)

- Запустить процессы через Camunda Tasklist.
    
- Проверить корректность:
    
    - При температуре > 25°C → активация задачи «Включить кондиционер».
        
    - Отсутствие ответа от датчика → переход в Escalation Lane.
        
- Пример симуляции: [![docs.camunda.org](https://favicon.yandex.net/favicon/v2/docs.camunda.org/?size=32&stub=1)Camunda Docs](https://docs.camunda.org/get-started/quick-start/).

#### 7. **Тестирование и оптимизация** (2 дня)

- Сценарии:
    
    - Одновременное срабатывание датчиков света и температуры.
        
    - Потеря связи с MQTT-брокером → обработка исключений.
        
- Замерить latency между событием и реакцией системы.
    

---

#### 8. **Документация** (1 день)

- Описать архитектуру в C4-моделях (Context, Container уровни).
    
- Подготовить видео-демо работы системы.
    
- Выложить код на GitHub с README: [![github.com](https://favicon.yandex.net/favicon/v2/github.com/?size=32&stub=1)github.com](https://github.com/).