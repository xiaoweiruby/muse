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
