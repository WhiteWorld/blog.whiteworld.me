{
    "date": "2015-01-22",
    "description": null,
    "draft": false,
    "id": 10,
    "image": null,
    "meta_title": null,
    "slug": "rails4-cheat-sheet",
    "tags": [
        "Rails",
        "Cheat Sheet"
    ],
    "title": "Rails4 Cheat Sheet",
    "type": "post"
}


### Model

```ruby:n
# 创建Model
class Post < ActiveRecord::Base
end
# 多对多关系（两种）
has_many :though
has_and_belongs_to_many
# 一对一关系
has_one
# 多对一关系
has_many
belongs_to

# validation 数据验证
validates :title, presence: true
topic.save
# => false
topic.save!
# => ActiveRecord::RecordInvalid: Validation failed: Title can't be blank
validates_presence_of
validates_uniqueness_of


# scope 把复杂的ORM语句创建为一个快捷方式
class Topic < ActiveRecord::Base
    scope :recent, -> { order("created_at DESC") } 
end

# ids has_many产生的方法，可以在form中使用
<%=  simple_form_for @drink do |f| %>
  <%= f.association :materials, :as => :check_boxes %><br>
  <%= f.submit "Submit" %>
<% end %>

# collect(&:id) 跟map一样
topics = [{id:1, title:"topic1"}, {id:2, title:"topic2"}]
topics.collect(&:id)
# => [1,2]

# includes 提前把关系元素取出来，类似其他ORM中的lazy方法
class Board < ActiveRecord::Base
  def
    @boards = Board.includes(:topics).all
    # 没有includes：@boards = Board.all
  end
end

# counter_cache 在计算belong object的数量时避免一次sql COUNT指令
class Order < ActiveRecord::Base
  belongs_to :customer, counter_cache: true
end
class Customer < ActiveRecord::Base
  has_many :orders
end
# 使用时添加orders_count列在Customer表中


# STI 暂时不清楚，用到再说

# Polymorphic Assoiciaion 两个不同的model可以同时has_many一个model方法，有点像组合
class Comment < ActiveRecord::Base
  belongs_to :commentable, :polymorphic => true
end
class Board < ActiveRecord::Base
  has_many :comments, :as => :commentable
end
class Topic < ActiveRecord::Base
  has_many :comments, :as => :commentable
end


```


### 中文化

```ruby:n
config.i18n.load_path += Dir[Rails.root.join('my', 'locales', '*.{rb,yml}').to_s]
config.i18n.default_locale = :'zh-CN'
# then,add files in config/locales
```

### Views

```ruby:n

# helper 封装常用的操作，减少views中嵌入的代码block
# partial 封装重复的HTML内容， collection partial 进一步简化，省去循环

# yield , content_for

# 逻辑判断，block， orm语句， 不应该在view里（尽量）

# form
<%= form_for @topic do |f| %>
    <%= f.label :name %>
    <%= f.text_field :name %>
    <%= f.submit %>
<% end %>

# nest form 暂时没用到


# 内建Helper
stylesheet_link_tag 
image_tag
form_for

# Helper_method， 在controller里面的method声明为helper_method 才可以在views中使用
# view_context 在controller必须使用view_context才能调用普通的helper（建议不要混着调用）

# link_to
<%= link_to user_path(@user) do%>
<%= link_to game_dislike_path(@game), class:'btn btn-sm btn-info' do%>已收藏 <% end %>
# form add class
html: {method: :put, class: 'form-horizontal'}
```

### Controller
```ruby:n
# Filter
after_action
around_action

# Strong Parameters
class PeopleController < ActionController::Base
  def update
    person.update_attributes!(person_params)
    redirect_to :back
  end
  private
    def person_params
      params.require(:person).permit(:name, :age)
    end
end

# redirect_to
# respond_with
# builder
```

### Asset Pipeline
```ruby:n
# Sass/SCSS
# SCSS 兼容 CSS 语法

# CoffeeScript
```

## Routing
```ruby:n
# 指定動作跟controller action
get 'products/:id' => 'catalog# view'

# 自動按照rails內建的RESTful路徑判斷controller action
resources :products
# member & collection
resources :products do
# 會產生products/:id/short
     member do
        get 'short'
        post 'toggle'
    end
# 會產生products/sold
    collection do
        get 'sold'
    end
end
```
