# Rails CheatSheet

## Rails

安裝 Rails

```ruby
$ gem install rails
```

建立新的 Rails 檔案

```ruby
$ rails new <app_name>
```

指定 Rails 版本

```ruby
$ rails _6.1.1.1_ new <app_name>
```

建立新的 Rails 檔案，並將資料庫從 SQLite -> PostgreSQL or MySQL
(-d = database)

```ruby
$ rails new app --database=postgresql
$ rails new app --database=mysql
```

如果使用 PostgreSQL or MySQL，要先建立 DB

```
$ createdb <db_name>
```

建立 API 模式的 Rails。減少 Gem、middleware 檔案。

```ruby
$ rails new app --api
```

啟動 Rails Server

```ruby
$ rails s
```

進入 Rails console / 沙盒模式

```
$ rails c
$ rails c --sandbox
```

查看 Rails Routes

```
$ rails routes
```

安裝 Gem 套件

```
$ bundle install
```

## Rails CLI

建立 controller（名稱複數)

```ruby
$ rails g controller <app_name> <action>
```

建立 model（名稱單數）

```ruby
$ rails g model <app_name> <:table_col>
```

## Migration

建立 Migration

```ruby
$ rails g migration <name> <col:type>
```

執行 Migration

```ruby
$ rails db:migrate
```

引入 seed 資料

```ruby
$ rails db:seed
```

返回前一步驟

```ruby
$ rails db:rollback
```

新增欄位名稱 / 修改欄位名稱 / 修改欄位型別 / 移除欄位名稱

```ruby
add_col(table_name, col, type, options)
rename_col(table_name, old_col_name, new_col_name)
change_column(table_name, col, type, options)
remove_col(table_name , col)
```

新增 / 移除 index

```
add_index(table_name, col, option)
remove_index(table_name, col, option)
```

## Rails Routes

Routes 使用的 HTTP 方法有五種，GET / POST / PATCH / PUT/ DELETE

```ruby
# /config/routes/routes.rb

GET "/", to: "<app_name>#index"
POST "/", to: "<app_name>#create"
PATCH "/:id", to: "<app_name>#index"
PUT "/:id", to: "<app_name>#index"
DELETE "/:id", to: "<app_name>#destroy"
```

RESTful 路徑
( resource 不含 :id , index ) 路徑

```ruby
resources :<app_name>
resource :<app_name>
```

額外增加路徑

```ruby
resources :<app_name> do
  member do
    get :<route_name>
  end

  collection do
    get :<route_name>
  end
end
```

## Rails Controller

執行 Action 前先載入

```ruby
before_action :def_name, only: [:action_names]
```

清洗確認 params

```ruby
params.require(:hash_name).permit(:col)
```

簡易 7 條 RESTful Action

```ruby
  before_action: :find_params, only: [:show, :edit, :update, :destroy]

  def index
    @<name> = <Name>.all
  end

  def show
  end

  def new
    @<name> = <Name>.new
  end

  def create
    @<name> = <Name>.new(<name>_params)
    if @<name>.save
      redirect_to <name>_path
    else
      render :new
    end
  end

  def edit
    @<name> = <Name>.find(params[:id])
  end

  def update
    @<name> = <Name>.find(params[:id])
    if @<name>.save(<name>_params)
      redirect_to <name>_path
    else
      render :edit
    end
  end

  def destroy
    @<name> = <Name>.find(params[:id])
    @<name>.destroy if <name>
    redirect_to <name>_path
  end

  private
  def <name>_params
    params.require(:hash_name).permit(:col)
  end

  def find_params
    @<name> = <Name>.find(params[:id])
  end
```
