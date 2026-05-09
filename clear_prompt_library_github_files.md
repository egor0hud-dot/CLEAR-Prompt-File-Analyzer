# GitHub-файлы для библиотеки CLEAR Prompt Analyzer

Ниже приведён готовый набор файлов для публикации библиотеки/проекта с CLEAR-промптом анализа файлов.

---

# README.md

```md
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
```

---

## Установка

```bash
pip install clear-prompt-analyzer
```

---

## Использование

```python
from clear_prompt_analyzer import build_prompt

prompt = build_prompt(
    filename="main.py",
    file_type="python",
    file_content="print(eval(input()))"
)

print(prompt)
```

---

## Пример CLEAR-промпта

```text
Context:
Ты — эксперт по анализу файлов.

Lens / Limitations:
Ответ только в JSON.

Examples:
[
  {
    "error": "Использование eval",
    "recommendation": "Удалить eval",
    "line": 1,
    "severity": "high"
  }
]

Action:
Проанализируй файл.

Result:
Верни JSON-массив объектов.
```

---

## Поддерживаемые типы файлов

- Python
- JavaScript
- JSON
- YAML
- Markdown
- TXT
- DOCX (через extraction)
- PDF (через extraction)

---

## Roadmap

- [ ] RAG integration
- [ ] Multi-agent analysis
- [ ] AI scoring
- [ ] Auto-fix generation
- [ ] GitHub Actions integration

---

## License

MIT
```

---

# LICENSE

```text
MIT License

Copyright (c) 2026

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files...
```

---

# .gitignore

```gitignore
__pycache__/
*.pyc
.env
venv/
.idea/
.vscode/
.pytest_cache/
coverage/
dist/
build/
*.egg-info/
```

---

# requirements.txt

```text
pydantic>=2.0.0
python-dotenv>=1.0.0
```

---

# pyproject.toml

```toml
[build-system]
requires = ["setuptools>=61.0"]
build-backend = "setuptools.build_meta"

[project]
name = "clear-prompt-analyzer"
version = "0.1.0"
description = "CLEAR framework prompt builder for file analysis"
readme = "README.md"
requires-python = ">=3.10"
license = {text = "MIT"}
authors = [
  {name = "Author"}
]
dependencies = [
  "pydantic>=2.0.0"
]
```

---

# setup.py

```python
from setuptools import setup, find_packages

setup(
    name="clear-prompt-analyzer",
    version="0.1.0",
    packages=find_packages(where="src"),
    package_dir={"": "src"},
)
```

---

# src/clear_prompt_analyzer/__init__.py

```python
from .prompt_builder import build_prompt
```

---

# src/clear_prompt_analyzer/prompt_builder.py

```python
from textwrap import dedent


def build_prompt(filename: str, file_type: str, file_content: str) -> str:
    return dedent(f"""
    Context:
    Ты — эксперт по анализу документов, кода и текстовых файлов.

    Необходимо проанализировать:
    - Имя файла: {filename}
    - Тип файла: {file_type}

    Содержимое файла:
    ```
    {file_content}
    ```

    Lens / Limitations:
    - Ответ должен быть строго JSON.
    - Не использовать markdown.
    - Не добавлять пояснения.

    Examples:
    [
      {{
        "error": "Использование eval",
        "recommendation": "Удалить eval",
        "line": 12,
        "severity": "high"
      }}
    ]

    Action:
    Проанализируй файл и найди ошибки.

    Result:
    Верни JSON-массив объектов.
    """).strip()
```

---

# tests/test_prompt_builder.py

```python
from clear_prompt_analyzer import build_prompt


def test_prompt_generation():
    prompt = build_prompt(
        filename="test.py",
        file_type="python",
        file_content="print('hello')"
    )

    assert "Context:" in prompt
    assert "Result:" in prompt
```

---

# CHANGELOG.md

```md
# Changelog

## [0.1.0] - 2026-05-09

### Added
- CLEAR prompt builder
- JSON analysis format
- Severity support
- File analysis template
```

---

# CONTRIBUTING.md

```md
# Contributing

1. Fork repository
2. Create feature branch
3. Add tests
4. Open Pull Request

## Coding standards

- Black
- Ruff
- Type hints
```

---

# SECURITY.md

```md
# Security Policy

Если вы нашли проблему безопасности:

- не публикуйте её публично;
- создайте private issue.
```

---

# .env.example

```env
OPENAI_API_KEY=
MODEL_NAME=gpt-5.5
```

---

# .github/workflows/ci.yml

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'

      - name: Install dependencies
        run: |
          pip install -r requirements.txt
          pip install pytest

      - name: Run tests
        run: |
          pytest
```

---

# .github/ISSUE_TEMPLATE/bug_report.md

```md
---
name: Bug report
about: Сообщить об ошибке
---

## Описание

## Шаги воспроизведения

## Ожидаемое поведение
```

---

# .github/pull_request_template.md

```md
## Что изменено

## Checklist

- [ ] Тесты добавлены
- [ ] Документация обновлена
- [ ] Линтеры пройдены
```

---

# docs/prompt_architecture.md

```md
# CLEAR Prompt Architecture

## Context
Описание задачи.

## Lens
Ограничения и правила.

## Examples
Few-shot examples.

## Action
Основное действие модели.

## Result
Формат результата.
```

