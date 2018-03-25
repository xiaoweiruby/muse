# 才华横溢 muse 案例教学 12
```
cd workspace
rails new muse
cd muse
git init
git commit -m "initial commit"
git remote add origin https://github.com/shenzhoudance/muse.git
git push -u origin master
```
```
atom .
rails server
http://localhost:3000/
```
![image](https://ws2.sinaimg.cn/large/006tKfTcgy1fpnw0fa0rej30uy0rsh3o.jpg)

```
git checkout -b post
rails g model post title:string link:string description:text
rake db:migrate
git add .
git commit -m "add model post"
git push origin post
```
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpnw57nd6vj31bk0h0wi2.jpg)
```
rails g controller Posts
---
config/routes.rb
---
Rails.application.routes.draw do
  resources :posts
  root 'posts#index'
end
---
```
![image](https://ws4.sinaimg.cn/large/006tKfTcgy1fpnwxsqojij311u09wjs6.jpg)
```
app/controllers/posts_controller.rb
---
class PostsController < ApplicationController
  def index
  end
end
---
```
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpnx04vaesj31kw0hp44e.jpg)
```
app/views/posts/index.html.erb
---
<h1>欢迎来到才华横溢的世界</h1>
```
![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fpnx26bh58j30r808kdgf.jpg)

```
git checkout -b add_gem
https://rubygems.org/
---
gem 'haml', '~> 5.0', '>= 5.0.4'
gem 'simple_form', '~> 3.5', '>= 3.5.1'
gem 'paperclip', '~> 6.0'
---
bundle install
git status
git add .
git commit -m "add application gems and post view files"
```
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpp3ktwqsij31c20h8adl.jpg)

```
app/controllers/posts_controller.rb
---
def index
end
def show
end
def new
@post = Post.new
end
def create
@post = Post.new(post_params)
if @post.save
 redirect_to @post
else
 render 'new'
end

def edit
end

def update
end

def destroy
end

private

def find_params
end

def post_params
params.require(:post).permit(:title, :link, :description)
end
end
---
app/views/posts/_form.html.haml
---
= simple_form_for @post do |f|
	= f.input :title
	= f.input :link
	= f.input :description

	= f.button :submit
---
app/views/posts/new.html.haml
---
%h1 Add Inspiration

= render 'form'
---
```
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpp423dip1j30ou0dkgmg.jpg)

# 添加内容不被 show 页面显示

![image](https://ws3.sinaimg.cn/large/006tKfTcly1fpp49hi0faj30oi0dmgmx.jpg)
![image](https://ws2.sinaimg.cn/large/006tKfTcly1fpp49nbglnj31kw0gd7ab.jpg)

# 显示 show 的内容
```
app/views/posts/show.html.haml
--
%h1= @post.title
%h1= @post.link
%h1= @post.description
---
app/controllers/posts_controller.rb
---
class PostsController < ApplicationController
  before_action :find_post, only: [:show, :edit, :update, :destroy]

  def index

  end

  def show

  end

  def new
   @post = Post.new
  end

  def create
    @post = Post.new(post_params)
    if @post.save
    redirect_to @post
    else
    render 'new'
  end
end

  def edit
  end

  def update
  end

  def destroy
  end

  private

  def find_post
    @post = Post.find(params[:id])
  end

  def post_params
    params.require(:post).permit(:title, :link, :description)
  end
end
---
```
![image](https://ws2.sinaimg.cn/large/006tKfTcly1fpp4mwslgzj31080d8q4r.jpg)

# 首页页面呈现效果
```
app/views/posts/index.html.haml
---
- @posts.each do |post|
  %h2= link_to post.title, post

= link_to "add posts", new_post_path
---
```
![image](https://ws3.sinaimg.cn/large/006tKfTcly1fpp51g7tasj31bc0cwac8.jpg)
```
app/controllers/posts_controller.rb
---
def index
		@posts = Post.all.order("created_at DESC")
	end
---

app/views/posts/show.html.haml
---
%h1= @post.title
%h1= @post.link
%h1= @post.description

= link_to "home", root_path
= link_to "edit", edit_post_path(@post)
= link_to "Delete", post_path(@post), method: :delete, data: { confirm: "Are you sure?" }

```

![image](https://ws4.sinaimg.cn/large/006tKfTcly1fpp5h200bqj30oi0dmgmx.jpg)
![image](https://ws3.sinaimg.cn/large/006tKfTcly1fpp5h3k7kjj30m40emabi.jpg)
![image](https://ws1.sinaimg.cn/large/006tKfTcly1fpp5h9eoj9j30mw08oaan.jpg)

git add .
git commit -m "add post CRUD"
git push origin add_gem
# 以上的代码的梳理，完成了基本功能的 CRUD 的构建；
