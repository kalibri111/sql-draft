# sql-draft
## Концептуальная модель
![Снимок экрана 2023-04-11 в 19.58.53.png](images%2F%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202023-04-11%20%D0%B2%2019.58.53.png)
1) Person – много людей имеют одинаковые доступы, люди могут принадлежать к нескольким организациям, иметь разные роли
2) Person-Organization – разбиение many-to-many relationship
3) Organization – определяет структурное подразделение людей
4) Access – сущность определяет уровень доступа person к разным регионам
5) Checkpoint – сущность определяющая временные отметки прохождения контроля
6) Area – разделяет уровни доступа, разные люди могут иметь разный набор доступов
7) Auth – тип контроля, необходимые меры
8) Security – сущность соответствует охранной организации
## Логическая модель
![Снимок экрана 2023-04-11 в 19.44.02.png](images%2F%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202023-04-11%20%D0%B2%2019.44.02.png)
## Физическая модель
### Person
| Field        | Type    | Key | Description               |
|--------------|---------|-----|---------------------------|
| id           | bigint  | PK  |                           |
| firstName    | text    |     | Users first name          |
| lastName     | test    |     | Users last name           |
| age          | int     |     | Users age                 |
| sex          | boolean |     | 1 - men/ 0 - women        |
| admitted     | date    |     | Timestamp of registration |
### Person-Organization
| Field        | Type    | Key | Description               |
|--------------|---------|-----|---------------------------|
| id           | bigint  | PK  |                           |
| person       | bigint  | FK  | Link for person           |
| organization | bigint  | FK  | Link for organization     |
| role         | enum    |     | Type of person            |
### Access
| Field  | Type    | Key | Description          |
|--------|---------|-----|----------------------|
| id     | bigint  | PK  |                      |
| person | bigint  | FK  | Link for person      |
| area   | bigint  | FK  | Link for access area |
### Area
| Field    | Type   | Key | Description                               |
|----------|--------|-----|-------------------------------------------|
| id       | bigint | PK  |                                           |
| name     | text   |     | Human readable name of access area        |
| auth     | bigint | FK  | Link for control type                     |
| address  | text   |     | Address of access area                    |
| security | bigint | FK  | Link to security organization description |
### Checkpoint
| Field     | Type    | Key | Description                              |
|-----------|---------|-----|------------------------------------------|
| id        | bigint  | PK  |                                          |
| isEnter   | boolean |     | Check for enter of exit                  |
| access    | bigint  | FK  | One-to-one link for access entity        |
| timestamp | date    |     | Timestamp of checking                    |
### Auth
| Field    | Type    | Key | Description                               |
|----------|---------|-----|-------------------------------------------|
| id       | bigint  | PK  |                                           |
| type     | enum    |     | Type of control                           |
| passport | boolean |     | Is document needed                        |
### Security
| Field        | Type    | Key | Description                                   |
|--------------|---------|-----|-----------------------------------------------|
| id           | bigint  | PK  |                                               |
| name         | text    |     | Name of security organization                 |
| reactionTime | time    |     | Time of squad arrived, needed for some reason |
| armed        | boolean |     | Has organization assigned to wear weapon      |
| tel          | text    |     | Telephone number for reaction                 |
| about        | text    |     | Additional information                        |
