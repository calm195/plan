# 数据库设计

## 公共词条(`global`)

| 字段       | 类型         | 说明                   |
| :--------- | :----------- | :--------------------- |
| id         | INT/BIGINT   | 主键，自增             |
| created_at | TIMESTAMP    | 创建时间               |
| updated_at | TIMESTAMP    | 最后修改时间           |
| deleted_at     | TIMESTAMP  | 删除时间 |

## 博客表 (`posts`)

| 字段    | 类型         | 说明     |
| :------ | :----------- | :------- |
| title   | VARCHAR(200) | 博客标题 |
| content | TEXT         | 博客内容 |
| path    | VARCHAR(200) | 博客路径 |

## 分类表 (`categories`)

| 字段 | 类型        | 说明                 |
| :--- | :---------- | :------------------- |
| name | VARCHAR(50) | 分类名称 (如 "技术") |

## 博客分类关联表 (`posts_categories`)

| 字段        | 类型       | 说明            |
| :---------- | :--------- | :-------------- |
| category_id | INT/BIGINT | `categories.id` |
| post_id     | INT/BIGINT | `posts.id`      |

## 访问表 (`visit`)

| 字段 | 类型       | 说明     |
| :--- | :--------- | :------- |
| ip   | INT/BIGINT | 用户IP   |
| path | INT/BIGINT | 路径列表 |