# Rails CheatSheet

## 新增 Rails

安裝 Rails

```ruby
gem install rails
```

建立新的 Rails 檔案，「app」名稱可替換。

```ruby
rails new app
```

建立新的 Rails 檔案，並將資料庫從 SQLite -> PostgreSQL or MySQL
(-d = database)

```ruby
rails new app --d=postgresql
rails new app --d=mysql
```

建立 API 模式的 Rails。減少 Gem、middleware 檔案。

```ruby
rails new app --api
```

## 設定 Rails

啟動 Rails Server

```ruby
rails s
```

Routes 使用的 HTTP 方法有五種，GET / POST / PATCH / PUT/ DELETE

/_config / routes / routes.rb_

```ruby
# /config/routes/routes.rb

GET "/", to: "books#index"
POST "/", to: "books#create"
PATCH "/:id", to: "books#index"
PUT "/:id", to: "books#index"
DELETE "/:id", to: "books#destroy"
```

RESTful 路徑

```ruby
resources :books
```
