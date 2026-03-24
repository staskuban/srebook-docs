---
title: "testing_functionality_and_contents_for_a_new_runbook_procedure"
layout: default
---

# testing_functionality_and_contents_for_a_new_runbook_procedure

```yaml
title: Установка расширения SREBook в Visual Studio Code из VSIX файла
description: Пошаговая инструкция для начинающих по ручной установке плагина SREBook в VS Code и его первичной настройке с использованием API-токена.
runbook_type: instruction
metadata:
  audience: Начинающие пользователи и специалисты начального уровня, предпочитающие работу через графический интерфейс (GUI) VS Code. Инструкция не требует навыков работы с терминалом.
  difficulty: beginner
goal:
  description: Успешно установить расширение 'srebook' в редактор Visual Studio Code, используя предварительно скачанный файл с расширением .vsix.
prerequisites:
  required:
    - item: Visual Studio Code
      details: Установленный редактор на компьютере пользователя.
    - item: Файл расширения srebook.vsix
      details: Файл, скачанный по прямой ссылке https://portal.srebook.tech/download.
    - item: API Токен
      details: Сгенерированный токен доступа в личном кабинете https://portal.srebook.tech/dashboard/tokens.
  optional: []
steps:
  - id: download_vsix
    title: Скачивание файла расширения
    description: Перейдите на официальный портал и загрузите файл .vsix.
    command: ""
    example: https://portal.srebook.tech/download
    notes: Сохраните файл в удобное место, например, в папку 'Загрузки'.
  - id: open_extensions
    title: Открытие панели расширений
    description: Запустите VS Code и нажмите на иконку Extensions в боковой панели (Activity Bar) или нажмите 'Ctrl+Shift+X'.
    command: ""
    example: ""
    notes: ""
  - id: install_from_vsix
    title: Установка из локального файла
    description: В верхней части панели расширений нажмите на значок «...» (More Actions) и выберите в выпадающем меню пункт «Install from VSIX...».
    command: ""
    example: ""
    notes: ""
  - id: select_file
    title: Выбор файла и подтверждение
    description: В открывшемся окне проводника выберите ранее скачанный файл 'srebook.vsix' и нажмите кнопку 'Install'.
    command: ""
    example: ""
    notes: Дождитесь появления системного уведомления в нижнем углу экрана о завершении установки.
validation:
  checks:
    - description: Настройка токена в плагине
      expected_result: После ввода токена и нажатия кнопки «Сохранить» в настройках (иконка шестеренки в чате), расширение принимает ключ.
    - description: Тестовый запрос в чат
      expected_result: При отправке сообщения в окно чата SREBook, ИИ генерирует и возвращает текстовый ответ.
troubleshooting:
  - issue: Ошибка 'Unauthorized' при попытке общения с ИИ
    solution: Выпустите новый токен на https://portal.srebook.tech/dashboard/tokens, вставьте его в поле настроек расширения (шестеренка в хедере панели плагина) и обязательно нажмите кнопку «Сохранить».
  - issue: Плагин не реагирует или чат 'завис' после настройки
    solution: "Выполните перезагрузку окна VS Code: нажмите 'F1', введите команду 'Developer: Reload Window' и нажмите Enter, либо полностью перезапустите приложение."
examples: []
best_practices:
  - Используйте чат SREBook для помощи в написании кода и анализа ошибок непосредственно в контексте проекта.
  - "Не передавайте в чат конфиденциальные данные: пароли, секретные ключи доступа и персональные данные."
tasks_summary:
  - id: goal
    status: completed
    answer: Успешно установить расширение 'srebook' в редактор Visual Studio Code, используя предварительно скачанный файл с расширением .vsix.
  - id: audience
    status: completed
    answer: Начинающие пользователи и специалисты начального уровня, предпочитающие работу через графический интерфейс (GUI) VS Code. Инструкция не требует навыков работы с терминалом.
  - id: prerequisites
    status: completed
    answer: |-
      1. Установленный редактор Visual Studio Code.
      2. Наличие скачанного файла расширения `srebook.vsix` с сайта https://portal.srebook.tech/download.
      3. Доступ к папке с загруженным файлом.
  - id: steps
    status: completed
    answer: |-
      1. **Скачайте файл расширения**: Перейдите по ссылке https://portal.srebook.tech/download и сохраните файл `srebook.vsix`.
      2. **Откройте раздел расширений**: Нажмите на иконку Extensions в боковой панели VS Code.
      3. **Вызовите меню**: Нажмите на значок «...» (More Actions) в верхней части панели расширений.
      4. **Запустите установку**: Выберите пункт «Install from VSIX...».
      5. **Выберите файл**: В появившемся окне выберите скачанный файл и нажмите «Install».
      6. **Ожидание**: Дождитесь уведомления об успешной установке в нижнем углу экрана.
  - id: validation
    status: completed
    answer: |-
      1. **Откройте панель SREBook**: Нажмите на иконку расширения в левой боковой панели (Activity Bar).
      2. **Перейдите в настройки**: В верхней части (хедере) панели расширения нажмите на иконку шестеренки.
      3. **Авторизуйтесь**: Вставьте ваш API-токен, полученный на странице https://portal.srebook.tech/dashboard/tokens, в появившееся поле.
      4. **Проверьте связь**: Перейдите в окно чата плагина и отправьте любой текстовый запрос.
      5. **Ожидаемый результат**: ИИ пришлет ответ в чат. Это означает, что плагин установлен, настроен и успешно связывается с сервером.
  - id: troubleshooting
    status: completed
    answer: |-
      1. **Ошибка 'Unauthorized'**: Возникает при использовании неверного или просроченного токена. Решение: Выпустить новый токен на https://portal.srebook.tech/dashboard/tokens, вставить его и нажать «Сохранить».
      2. **Зависание**: Решение — перезагрузка окна команда 'Developer: Reload Window'.
  - id: examples
    status: completed
    answer: |-
      - **Безопасность**: Не передавайте в чат конфиденциальные данные.
      - **Использование**: Используйте чат для написания кода и анализа ошибок.

```