# REST API Documentation

Base URL: `/api/v1`

## Authentication
JWT Bearer Token.

### Authentication Endpoints
- POST /auth/login
- POST /auth/logout
- POST /auth/refresh
- GET /auth/profile

## Modules
### Users
GET/POST /users
GET/PUT/DELETE /users/{uuid}

Pagination: page, per_page
Sorting: name,email,created_at
Filtering: role,branch,is_active
Search: name,email

### Roles
CRUD /roles
### Permissions
CRUD /permissions
### Branches
CRUD /branches
### Brands
CRUD /brands
### Car Models
CRUD /car-models
### Products
CRUD /products
PATCH /products/{uuid}/publish
PATCH /products/{uuid}/featured
Filtering: branch_id,brand_id,car_model_id,year,featured,publish_status
Sorting: price,year,mileage,created_at
Search: title,sku

### Product Images
GET/POST/DELETE /products/{uuid}/images
### Product Videos
GET/POST/DELETE /products/{uuid}/videos
### Banners
CRUD /banners
### Company Profile
GET/PUT /company-profile
### Dashboard
GET /dashboard/statistics
### Settings
GET/PUT /settings
### Audit Logs
GET /audit-logs

## Standard Request Header
Authorization: Bearer {token}
Accept: application/json

## Success Response
```json
{"success":true,"message":"Success","data":{},"meta":{}}
```

## Error Response
```json
{"success":false,"message":"Validation Error","errors":{}}
```

## Status Codes
200,201,204,400,401,403,404,409,422,500
