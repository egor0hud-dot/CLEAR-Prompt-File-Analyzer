# CLEAR Prompt File Analyzer

Библиотека и набор промптов для анализа файлов с использованием LLM.

Проект использует фреймворк CLEAR:

- Context
- Lens / Limitations
- Examples
- Action
- Result

Основная задача — анализ содержимого файлов и возврат структурированных JSON-ошибок.

---

## Возможности

- Анализ кода
- Анализ документов
- Проверка ошибок
- Выявление рисков
- Поиск нарушений best practices
- Формирование рекомендаций
- JSON structured output
- Severity classification

---

## Структура ответа

```json
[
  {
    "error": "Описание ошибки",
    "recommendation": "Рекомендация",
    "line": 42,
    "severity": "high"
  }
]
