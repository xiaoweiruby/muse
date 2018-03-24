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
```
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpnw57nd6vj31bk0h0wi2.jpg)
