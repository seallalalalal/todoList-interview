# todoList-Inverview

因為時間真的不夠寫完，所以只寫了一點點的 frontend 的部分<br>
backend 只有初始專案 QwQ<br>
晚點會再補上 API 設計、database 設計的文件<br>

### Start Container

1. cd to root
2. `docker-compose up -d`

### Services

- frontend: http://localhost
- backend: http://localhost:8080
- database: http://localhost:5432

# API

| Path           | Method | Function                                        |
| :------------- | :----- | :---------------------------------------------- |
| `/login`       | POST   | Let user login and if success return token      |
| `/get-task`    | GET    | Get all the task in the database                |
| `/post-task`   | POST   | When user add a task, post it into database     |
| `/edit-task`   | POST   | Modify and update task                          |
| `/get-comment` | GET    | Get comments of certain task from comment table |
| `post-comment` | POST   | Post comment into database                      |

Path: `/get-task`
Request:

- Method: POST
- Request Body:

```json!
{
    "taskName": "do the laundry",
    "taskOwner": "842f638c-4f58-11ed-8453-0242ac1b0003",
    "dueTime": "2022/03/10 10:00",
    "description": "Remember to wash all your clothes",
}
```

Response:

- Status code 200

```json!
{
   "msg": "SUCCESS"
}
```

# DB schema

### user

| attribute | Type                            | Example                              |
| :-------- | :------------------------------ | :----------------------------------- |
| user_id   | VARCHAR(36)</br>**Primary Key** | 842f638c-4f58-11ed-8453-0242ac1b0003 |
| name      | VARCHAR(256)                    | Brian                                |
| email     | VARCHAR(256)                    | user@gmail.com                       |
| enabled   | TINYINT(1)                      | 1                                    |
| avatar    | BYTEA                           | (Binary Data)                        |
| token     | VARCHAR(512)                    | (token)                              |

### task

| attribute   | Type                             | Example                              |
| :---------- | :------------------------------- | :----------------------------------- |
| task_id     | VARCHAR(36) </br>**Primary Key** | 842f638c-4f58-11ed-8453-0242ac1b0003 |
| task_name   | VARCHAR(256)                     | taskName                             |
| is_complete | BOOLEAN                          | false                                |
| task_owner  | VARCHAR(36) </br>**Foreign Key** | 842f638c-4f58-11ed-8453-0242ac1b0003 |
| due_time    | DATE                             | 2021-09-27 15:22:53.679985+02        |
| description | TEXT                             | "fsdfjasdfsdf"                       |

### comment

| attribute    | Type                            | Example                              |
| :----------- | :------------------------------ | :----------------------------------- | ------------ | ---- | ----------------------------- |
| comment_id   | VARCHAR(36)</br>**Primary Key** | 842f638c-4f58-11ed-8453-0242ac1b0003 |
| content      | TEXT                            | "content"                            | comment-time | DATE | 2021-09-27 15:22:53.679985+02 |
| comment-task | VARCHAR(36)</br>**Foreign Key** | 842f638c-4f58-11ed-8453-0242ac1b0003 |

### history

| attribute   | Type                            | Example                                         |
| :---------- | :------------------------------ | :---------------------------------------------- |
| history_id  | VARCHAR(36)</br>**Primary Key** | 842f638c-4f58-11ed-8453-0242ac1b0003            |
| action      | SMALLINT                        | 0:create<br> 1:delete<br>2:modify               |
| user        | VARCHAR(36)</br>**Foreign Key** | 842f638c-4f58-11ed-8453-0242ac1b0003            |
| description | TEXT                            | "Brian change due date from 2019 to 2022......" |
| target-task | VARCHAR(36)</br>**Foreign Key** | 842f638c-4f58-11ed-8453-0242ac1b0003            |
