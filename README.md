# Система управления школой
## Обзор
Этот проект представляет собой систему управления базой данных школы, разработанную с использованием FastAPI. 
Система предназначена для управления записями студентов, классами и оценками. 
### Она поддерживает:
- [x] Создание и обновление профилей студентов через запросы get, post, put, delite
- [x] Атоматическое вычисление средних оценок в профиле студентов при внесения оценок в базу данных
- [x] Форматирование данных после ввода на стороне сервера
- [x] Тестирование в отдельной базе данных с поддержкой генерации тест кейсов

### Технологии:
- **Backend: FastAPI**
- **База данных: PostgreSQL**
- **Тестирование: pytest**

### Структура:

Программа реализована с помощью ряда моделуй папки "src", функционал каждого из которых описан ниже:

#### сonfig.py
Устанавливает текущий путь к базе данных в зависимосте от параметров запуска (тестовый или нет)

#### crud.py
Реализует операции создания, чтения, обновления и удаления (CRUD) для взаимодействия с базой данных

#### database.py
Отвечает за настройку и управление подключением к базе данных.
Обеспечивает подключение к базе данных и инициализацию таблиц.

#### main.py
Модуль main содержит основной код приложения. 
Здесь инициализируется и запускается FastAPI-приложение, а также настраиваются маршруты и эндпоинты. 
Этот модуль представляет собой точку входа для запуска приложения.

#### models.py
Модуль models определяет структуры данных и модели для работы с базой данных. 
Здесь создаются классы, представляющие таблицы в базе данных, и определяются их поля и связи. 
Этот модуль используется для взаимодействия с базой данных через ORM и в нашем случае также рассчитывает средний балл ученика при получение поля с оценками.

#### schemas.py
Модуль schemas содержит схемы данных, используемые для валидации входящих и исходящих данных в API. 
Схемы определяются с помощью Pydantic и используются для валидации входящих запросов.

#### test_main.py
Модуль test_main отвечает за тестирование функциональности приложения с помощью библиотеку pytest, а также fastapi.testclient для тестирования эндпоинтов FastAPI-приложения.
Для тестирования создается тестовая таблица, которая по умолчанию имеет название "students"(как и основаня), но располагается в другой базе данных(тестовой), путь к которой указывается в config.py.
После выполнения тестов эта база данных будет удалена. При повторном запуске тестов - создана снова.
Используются тесты:
- CRUD операций
- Тесты валидации
- Параметризованные тесты

Присутствуют тесткейсы с генерацией входных данных при помощи библиотеки Faker, которые можно задавать в функции generate_random_student_data и изменять количество тесткейсов в фикстуре к функции test_create_student.


### Установка 

- Клонируйте репозиторий:
```bash
git clone https://github.com/Dopelen/School
```

- Создайте виртуальное окружение и активируйте его:
```bash
python -m venv venv
# Для Windows перейдите в папку venv -> Scripts -> activate
venv\Scripts\activate
```

- Перейдите в корневую папку проекта "School" и установите зависимости:
```bash
pip install -r requirements.txt
```

- Установите путь к своей базе данных в файле *config.py*

- Запустите приложение из папки *School/src*
```bash
uvicorn main:app --reload
```

- Запустите тесты из корневой папки *School*
```bash
pytest tests 
```

