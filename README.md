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

# 以上的代码的梳理，完成了基本功能的 CRUD 的构建；
```
git status
git add .
git commit -m "add post CRUD"
git push origin add_gem
```
![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fpp61v0931j31kw0otdl6.jpg)
![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fpp61wmb2sj317s0q6tcg.jpg)
![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fpp61xzkxmj318a0s20yj.jpg)
![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fpp61zezq0j318k0ligq6.jpg)

```
git checkout -b devise
gem 'devise', '~> 4.4', '>= 4.4.3'
bundle install
rails g devise:views
rails g devise User
rake db:migrate
rails g migration add_user_id_to_post user_id:integer
rake db:migrate
---
app/models/post.rb
---
class Post < ApplicationRecord
  belongs_to :user
end
---
app/models/user.rb
class User < ApplicationRecord
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :trackable, :validatable
  has_many :posts
end
---
```
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpq0b9q4mvj31kw11048o.jpg)
```
app/controllers/posts_controller.rb
---
class PostsController < ApplicationController
  before_action :find_post, only: [:show, :edit, :update, :destroy]
  before_action :authenticate_user!, except: [:index, :show]
  def index
    @posts = Post.all.order("created_at DESC")
  end

  def show

  end

  def new
   @post = current_user.post.build
  end

  def create
    @post = current_user.post.build(post_params)
    if @post.save
    redirect_to @post
    else
    render 'new'
  end
end

  def edit
  end

  def update
    if @post.update(post_params)
      redirect_to @post
    else
      render 'edit'
  end
end

  def destroy
    @post.destroy
    redirect_to root_path
  end

  private

  def find_post
    @post = Post.find(params[:id])
  end

  def post_params
    params.require(:post).permit(:title, :link, :description)
  end
end
```
```
rails server
http://localhost:3000/users/sign_in
```
![image](https://ws2.sinaimg.cn/large/006tKfTcgy1fpq0bjazoxj31by0egq4c.jpg)
![image](https://ws2.sinaimg.cn/large/006tKfTcgy1fpq0fxw4y6j31js0bugn9.jpg)
![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fpq0fz2y4hj30ua09igmf.jpg)

```
rails c
2.3.1 :001 > @post = Post.last
2.3.1 :002 > @post = Post.last
2.3.1 :003 > @post = Post.first
2.3.1 :004 > @post.user_id = 1
2.3.1 :005 > @post.save
2.3.1 :006 > exit
```
![image](https://ws4.sinaimg.cn/large/006tKfTcgy1fpq0p6kwwij31kw0ig10b.jpg)
```
git status
git add .
git commit -m "add user_id & setuo devise"
git push origin devise
```
![image](https://ws4.sinaimg.cn/large/006tKfTcgy1fpq0sj134mj318a112qcm.jpg)

```
rails g migration add_name_to_user name:string
rake db:migrate
rails g devise views
```
```
app/views/devise/registrations/edit.html.erb
---
<div class="form-inputs">
  <%= f.input :name, required: true, autofocus: true %>
  <%= f.input :email, required: true %>
---
app/views/devise/registrations/new.html.erb
---
<div class="form-inputs">
  <%= f.input :name, required: true, autofocus: true %>
  <%= f.input :email, required: true %>
  <%= f.input :password, required: true, hint: ("#{@minimum_password_length} characters minimum" if @minimum_password_length) %>
  <%= f.input :password_confirmation, required: true %>
</div>
---
app/controllers/application_controller.rb
---
https://stackoverflow.com/questions/37341967/rails-5-undefined-method-for-for-devise-on-line-devise-parameter-sanitizer
---
class ApplicationController < ActionController::Base
  protect_from_forgery with: :exception

   before_action :configure_permitted_parameters, if: :devise_controller?

 	protected

 	def configure_permitted_parameters
 	  devise_parameter_sanitizer.permit(:sign_up, keys: [:username])
 	  devise_parameter_sanitizer.permit(:account_update, keys: [:username])
 	end
 end
---
```
![image](https://ws2.sinaimg.cn/large/006tKfTcly1fpq1wj68axj312e0fiwg1.jpg)
![image](https://ws1.sinaimg.cn/large/006tKfTcly1fpq1wizvgrj312a0hwgnj.jpg)

```
git checkout -b paperclip
app/models/post.rb
---
class Post < ApplicationRecord
  belongs_to :user
  has_attached_file :image, styles: { medium: "700x500>", thumb: "350x250>" }
  validates_attachment_content_type :image, content_type: /\Aimage\/.*\z/
end
---
rails generate paperclip post image
rake db:migrate
```
![image](https://ws3.sinaimg.cn/large/006tNc79gy1fpq9bf0klij31kw0g7dko.jpg)

```
app/views/posts/show.html.haml
---
%h1= @post.title
%p= @post.link
%p= @post.description
%p= @post.user.name
%p= @post.image


= link_to "home", root_path
= link_to "edit", edit_post_path(@post)
= link_to "Delete", post_path(@post), method: :delete, data: { confirm: "Are you sure?" }
---
app/controllers/posts_controller.rb
---
private

def find_post
  @post = Post.find(params[:id])
end

def post_params
  params.require(:post).permit(:title, :link, :description, :image)
end
end
---
```

# 本案例的关键的操作在于：
- （1）完成基本 CRUD 的基本功能；（model + controller + views + routes）
- （2）完成 devise + name 的使用；（这个注册页面的修改上面，还需要强化认知；）
http://xbearx1987-blog.logdown.com/posts/1707961-how-to-devise-new-name-field-and-administrator-rights
```
Devise 4的参数Sanitaizer API已更改

class ApplicationController < ActionController::Base
  before_action :configure_permitted_parameters, if: :devise_controller?

  protected

  def configure_permitted_parameters
    devise_parameter_sanitizer.permit(:sign_up, keys: [:username])
  end
end
```
- （3）完成 图片 栏位的使用；gem paperclip（这个图片上传的 gem 需要使用最新的上传功能）
```
app/views/posts/_form.html.haml
---
= simple_form_for @post do |f|
	= f.input :image
	= f.input :title
	= f.input :link
	= f.input :description

	= f.button :submit
---
app/views/posts/show.html.haml
---
= image_tag @post.image.url(:medium)
%h1= @post.title
%p= @post.link
%p= @post.description
%p= @post.user.name


= link_to "home", root_path
= link_to "edit", edit_post_path(@post)
= link_to "Delete", post_path(@post), method: :delete, data: { confirm: "Are you sure?" }
---
app/models/post.rb
---
class Post < ApplicationRecord
  belongs_to :user
  has_attached_file :image, styles: { medium: "700x500>", thumb: "350x250>" }
  validates_attachment_content_type :image, content_type: /\Aimage\/.*\z/
end
---
app/views/posts/index.html.haml
---
- @posts.each do |post|
  = link_to (image_tag post.image.url), post
  %h2= link_to post.title, post

  = link_to "add posts", new_post_path
---
```
![image](https://ws4.sinaimg.cn/large/006tKfTcly1fpqalvwfuij30ng0dmab0.jpg)
![image](https://ws4.sinaimg.cn/large/006tKfTcly1fpqam397hjj30uq0rmtlo.jpg)
![image](https://ws3.sinaimg.cn/large/006tKfTcly1fpqaucz05ij30xo0wadsz.jpg)

```
git status
git add .
git commit -m "add paperclip for image up;oadomg"


- （4）完成 用户 评论的对接；
- （5）完成 页面 美化的调试；
