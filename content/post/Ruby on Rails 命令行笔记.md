{
    "date": "2015-01-22",
    "description": null,
    "draft": false,
    "id": 11,
    "image": null,
    "meta_title": null,
    "slug": "ruby-on-rails-cli-tutorial",
    "tags": [
        "Rails",
        "Tutorial",
        "Cli"
    ],
    "title": "Ruby on Rails \u547d\u4ee4\u884c\u7b14\u8bb0",
    "type": "post"
}


### Create Migration

创建单独的Migration

```bash
# 添加列
rails generate migration AddPartNumberToProducts
rails generate migration AddPartNumberToProducts part_number:string
rails generate migration AddPartNumberToProducts part_number:string:index
# 删除列
rails generate migration RemovePartNumberFromProducts part_number:string
rails generate migration AddDetailsToProducts part_number:string price:decimal
# 创建表
rails generate migration CreateProducts name:string part_number:string
# 添加reference
rails generate migration AddUserRefToProducts user:references
# 创建JoinTable
rails g migration CreateJoinTableCustomerProduct customer product
```

创建Model

```bash
rails generate model Product name:string description:text
```

### Writing a Migration

```ruby
# Creating a Table
create_table :products do |t|
  t.string :name
end
# Creating a Join Table
create_join_table :products, :categories
# Changing Tables
change_table :products do |t|
  t.remove :description, :name
  t.string :part_number
  t.index :part_number
  t.rename :upccode, :upc_code
end
```

### Running Migrations

```bash
rake db:migrate 
# Rolling Back
rake db:rollback
rake db:rollback STEP=3
# Setup the Database
rake db:setup
# Resetting the Database
rake db:reset 
rake db:drop db:setup
```
