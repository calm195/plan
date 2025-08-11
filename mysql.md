# 数据库设计

## 博客表 (`posts`)

| 字段       | 类型         | 说明                   |
| :--------- | :----------- | :--------------------- |
| id         | INT/BIGINT   | 主键，自增             |
| user_id    | INT/BIGINT   | `users.id`             |
| title      | VARCHAR(200) | 博客标题               |
| content    | TEXT         | 博客内容 (长文本)      |
| created_at | TIMESTAMP    | 创建时间               |
| updated_at | TIMESTAMP    | 最后修改时间           |
| status     | VARCHAR(20)  | 状态 (draft/published) |

## 分类表 (`categories`)

| 字段 | 类型        | 说明                 |
| :--- | :---------- | :------------------- |
| id   | INT/BIGINT  | 主键，自增           |
| name | VARCHAR(50) | 分类名称 (如 "技术") |

## 博客分类关联表 (`post_categories`) - 多对多

| 字段        | 类型       | 说明            |
| :---------- | :--------- | :-------------- |
| id          | INT/BIGINT | 主键，自增      |
| category_id | INT/BIGINT | `categories.id` |
| post_id     | INT/BIGINT | `posts.id`      |