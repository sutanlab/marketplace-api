# Point of Sales API

> RESTful API for Point of Sales App

## TODO Task
- [x] CRUD Products
- [x] CRUD Categories
- [x] Validation schema
- [x] Search product by name
- [x] Sort product by name, category, date updated
- [x] Pagination products
- [x] Upload image (on products)
- [x] Cannot reduce stock (on products) below 0
- [x] Allowed CORS
- [x] Authentication with JWT
- [x] Rows caching with redis

## Stacks
- Node JS
- MySQL
- ExpressJS
- Sequelize ORM
- JOI Validator
- Redis

## Build Setup
1. Clone repository
`$ git clone https://github.com/sutanlab/point-of-sales-api.git`

2. Install depedencies
```bash
# with npm
$ npm install

# or with yarn
$ yarn install
```

3. Setup your environment variable in `.env` files (if not exists, create your own).
```env
# NODE_ENV development | production | test
NODE_ENV = development

# DATABASE
DB_HOSTNAME = 127.0.0.1
DB_USERNAME = root
DB_PASSWORD = xxxx
DB_NAME = dbtest

# SECRET KEY
SECRET_JWT = xxxx
```

4. Run database migrations (with shortcut scripts with `yarn` or `npm run`)
```bash
$ yarn db:init # create database

$ yarn db:migrate # run database migrations

$ yarn db:seed # run database seeder (if you want)

$ yarn db:rollback # rollback migrations

$ yarn db:drop # drop table
```

5. Serve server
```bash
$ yarn start
```

## API Details

### Products
| Method | Endpoint | Description | Request Param | Request Body | Request Query |
| --- | --- | --- | --- | --- | --- |
| GET | /api/product | Get products | -  | -  | `search`: STRING, `limit`: NUMBER, `page`: NUMBER, `sort`: STRING (column with order splitted by '-'. Ex: sort=name-asc (order by name ASC) |
| POST | /api/product | Create new product | - | `name`: STRING, `category`: STRING (UUID), `description`: STRING, `price`: NUMBER, `stock`: NUMBER, `image: FILE` | - |
| GET | /api/product/:id | Get one product by id | `id`: STRING (UUID) | - | - |
| PUT | /api/product/:id | Update product | `id`: STRING (UUID) | `name`: STRING, `category`: STRING (UUID), `description`: STRING, `price`: NUMBER, `stock`: NUMBER, `image: FILE` | - |
| DELETE | /api/product/:id | Delete product | `id`: STRING (UUID) | - | - |
| GET | /file/image/product/:id | Get product image | `id`: STRING (UUID) | - | - |

### Category
| Method | Endpoint | Description | Request Param | Request Body | Request Query |
| --- | --- | --- | --- | --- | --- |
| GET | /api/category | Get category | -  | -  | - |
| POST | /api/category | Create new category | - | `name`: STRING | - |
| GET | /api/category/:id | Get one category by id | `id`: STRING (UUID) | - | - |
| PUT | /api/category/:id | Update category | `id`: STRING (UUID) | `name`: STRING | - |
| DELETE | /api/category/:id | Delete category | `id`: STRING (UUID) | - | - |

### User
| Method | Endpoint | Description | Request Param | Request Body | Request Query |
| --- | --- | --- | --- | --- | --- |
| PUT | /api/user/:id | Update user | `id`: STRING (UUID) | `name`: STRING, `email`: STRING, `password`: STRING | - |
| DELETE | /api/user/:id | Delete user | `id`: STRING (UUID) | - | - |

### Auth
| Method | Endpoint | Description | Request Headers | Request Body |
| --- | --- | --- | --- | --- |
| POST | /auth/register | Register user | -  | `name`: STRING, `email`: STRING, `password`: STRING |
| POST | /auth/login | Login user | - | `email`: STRING, `password`: STRING |
| GET | /auth/info | Get user info | `authorization`: STRING (TOKEN) | - |

---
Copyright © 2019 by Sutan Gading Fadhillah Nasution