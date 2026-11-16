# Money Talks Project — Backend Root

Родительский Maven-проект backend-части **Money Talks Project** — системы учёта
личных финансов, построенной как набор Spring Boot-микросервисов.

Репозиторий содержит только `pom.xml` (`packaging: pom`): общие версии Java,
Spring Boot и Spring Cloud, из которого наследуются все сервисы проекта.

## Что задаёт root

| Параметр | Значение |
|---|---|
| Group ID | `b4e.ru` |
| Artifact ID | `mtp-backend-root` |
| Версия | `0.1.0` |
| Java | 21 |
| Spring Boot | 4.0.1 (`spring-boot-starter-parent`) |
| Spring Cloud | 2025.1.0 (BOM в `dependencyManagement`) |
| MapStruct | 1.5.5.Final |
| JJWT | 0.12.3 |

Сервисы подключают root как родителя с пустым `relativePath`, то есть POM должен
быть установлен в локальный Maven-репозиторий.

## Сборка

Требуется JDK 21.

```bash
./mvnw install
```

В Windows:

```powershell
.\mvnw.cmd install
```

`install` для `pom`-проекта публикует `b4e.ru:mtp-backend-root:0.1.0` локально.
После этого можно собирать `mtp-backend-commons` и сервисы, которые наследуют
родителя.

## Сервисы системы

| Репозиторий | Назначение | Порт |
|---|---|---|
| [mtp-backend-commons](https://github.com/Sun1tAr/mtp-backend-commons) | Общие DTO, ошибки, заголовки, контекст запроса | — |
| [mtp-backend-ms-gateway](https://github.com/Sun1tAr/mtp-backend-ms-gateway) | Точка входа, маршрутизация, JWT | 8080 |
| [mtp-backend-ms-cathegories](https://github.com/Sun1tAr/mtp-backend-ms-cathegories) | Категории доходов и расходов | 8081 |
| [mtp-backend-ms-account](https://github.com/Sun1tAr/mtp-backend-ms-account) | Счета, балансы и исполнение ордеров | 8082 |
| [mtp-backend-ms-user](https://github.com/Sun1tAr/mtp-backend-ms-user) | Пользователи и учётные данные | 8083 |
| [mtp-backend-ms-transaction](https://github.com/Sun1tAr/mtp-backend-ms-transaction) | Транзакции и оркестрация операций | 8084 |

Общая документация проекта — в узловом репозитории
[Money-Talks-Project](https://github.com/Sun1tAr/Money-Talks-Project).
Аналитические материалы и BPMN-модели — в
[MTP-docs](https://github.com/Sun1tAr/MTP-docs).

## Порядок локальной сборки

```bash
# 1. Родительский POM
./mvnw install

# 2. Общий модуль
cd ../mtp-backend-commons && ./mvnw install

# 3. Любой сервис
cd ../mtp-backend-ms-user && ./mvnw spring-boot:run
```

Сервисам нужны PostgreSQL и переменные окружения из их собственных README.
