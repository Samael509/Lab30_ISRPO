# Лабораторная работа №30. JSON и модели данных

## Основная информация
- **ФИО:** Уютов Павел Александрович
- **Группа:** ИСП-231
- **Дата:** 31.05.2026

## Краткое описание
Изучили формат JSON, настройку сериализации в ASP.NET Core, атрибуты [JsonPropertyName] и [JsonIgnore], сериализацию enum как строки, ручную сериализацию и десериализацию через JsonSerializer.

## Структура проекта

- `Program.cs` - настройка сервисов, JSON, Swagger
- `HeroesApi.csproj` - файл проекта
- `Models/Hero.cs` - модели Hero, Weapon, enum Universe
- `Data/HeroesStore.cs` - хранилище героев в памяти
- `Controllers/HeroesController.cs` - контроллер с маршрутами
- `img/` - скрины
- `README.md` - описание

## Маршруты

| Метод | URL | Описание | Статус |
|---|---|---|---|
| GET | /api/heroes | Все герои (фильтр по universe) | 200 |
| GET | /api/heroes/{id} | Герой по id | 200/404 |
| GET | /api/heroes/demo | Сравнение настроек сериализации | 200 |
| GET | /api/heroes/search | Поиск по имени | 200/400 |
| GET | /api/heroes/serialize | Демонстрация JsonSerializer | 200 |

## Атрибуты JSON

| Атрибут / настройка | Что делает | Пример |
|---|---|---|
| `[JsonPropertyName("name")]` | Задаёт имя поля в JSON | "name" вместо "Name" |
| `[JsonIgnore]` | Поле не попадает в JSON | Пароли, внутренние поля |
| `PropertyNamingPolicy.CamelCase` | Все поля в camelCase | "realName" вместо "RealName" |
| `JsonStringEnumConverter` | Enum как строка | "Marvel" вместо 0 |
| `WriteIndented = true` | JSON с отступами | Для удобства при разработке |

## Главные выводы
1. Сериализация — это преобразование объекта C# в JSON-строку. Десериализация — обратный процесс: JSON-строка → объект C#.
2. [JsonIgnore] нужен чтобы скрыть от клиента служебные данные — например пароли, токены, внутренние заметки.
3. Enum лучше сериализовывать строкой — клиент сразу видит "Marvel" вместо непонятного числа 0.
4. После настройки CamelCase все поля стали в нижнем регистре — realName, powerLevel вместо RealName, PowerLevel.