
---
### 1. **Таблица Ученики** (students)

Храним основную информацию о учениках, включая уникальный идентификатор и метаданные.

```sql
CREATE TABLE students (
    id INT PRIMARY KEY,  -- Уникальный идентификатор ученика
    name VARCHAR(255),           -- Имя ученика
    created_at DATE,             -- Дата создания записи ученика
    updated_at DATE              -- Дата последнего обновления данных ученика
);
```

### 2. **Таблица Контакты** (contacts)

Для хранения различных типов контактов учеников, связанных с учениками через внешний ключ.

```sql
CREATE TABLE contacts (
    id INT PRIMARY KEY,   -- Уникальный идентификатор контакта
    student_id INT,               -- Внешний ключ, ссылающийся на таблицу students
    contact_type VARCHAR(50),     -- Тип контакта (например, "учитель", "родитель")
    contact_info VARCHAR(255),    -- Контактная информация (телефон, почта и т.д.)
    FOREIGN KEY (student_id) REFERENCES students(student_id)
);
```

### 3. **Таблица Стоимость Занятия** (lesson_costs)

Сохраняем информацию о стоимости уроков, где каждый ученик может иметь разные стоимости уроков.

```sql
CREATE TABLE lesson_costs (
    cost_id INT PRIMARY KEY,      -- Уникальный идентификатор стоимости занятия
    student_id INT,               -- Внешний ключ, ссылающийся на таблицу students
    lesson_cost DECIMAL(10, 2),   -- Стоимость занятия
    created_at DATE,              -- Дата указания стоимости
    FOREIGN KEY (student_id) REFERENCES students(student_id)
);
```

### 4. **Таблица Оплаты** (payments)

Информация об оплатах, связанных с учениками.

```sql
CREATE TABLE payments (
    payment_id INT PRIMARY KEY,    -- Уникальный идентификатор платежа
    student_id INT,                -- Внешний ключ, ссылающийся на таблицу students
    amount DECIMAL(10, 2),         -- Сумма оплаты
    payment_date DATE,             -- Дата оплаты
    FOREIGN KEY (student_id) REFERENCES students(student_id)
);
```

### 5. **Таблица Домашних Заданий** (homework)

Сохраняем домашние задания, связанные с учениками.

```sql
CREATE TABLE homework (
    homework_id INT PRIMARY KEY,    -- Уникальный идентификатор домашнего задания
    student_id INT,                 -- Внешний ключ, ссылающийся на таблицу students
    homework_description TEXT,      -- Описание домашнего задания
    created_at DATE,                -- Дата создания домашнего задания
    updated_at DATE,                -- Дата последнего обновления
    FOREIGN KEY (student_id) REFERENCES students(student_id)
);
```

### 6. **Таблица Уроков** (lessons)

Информация о проведенных уроках с учётом их статуса и описания.

```sql
CREATE TABLE lessons (
    lesson_id INT PRIMARY KEY,      -- Уникальный идентификатор урока
    student_id INT,                 -- Внешний ключ, ссылающийся на таблицу students
    lesson_datetime DATETIME,       -- Дата и время проведения урока
    status VARCHAR(50),             -- Статус урока (null, проведен, перенесен, отменен)
    lesson_description TEXT,        -- Описание урока
    created_at DATE,                -- Дата создания урока
    updated_at DATE,                -- Дата последнего обновления описания урока
    FOREIGN KEY (student_id) REFERENCES students(student_id)
);
```
