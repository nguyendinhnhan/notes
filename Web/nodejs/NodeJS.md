https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol

1. Start nodejs - https://expressjs.com/en/starter/installing.html
- npm init
- create index.js file in root folder
- npm install express
  
2. Hello word - https://expressjs.com/en/starter/hello-world.html
- copy example, paste to index.js
- node index.js
- Go to http://localhost:3000/

3. Nodemon & Debug
- npm install --save-dev nodemon
- nodemon --inspect index.js => open inspect on Chrome -> click node icon -> debug, break point,... debug nhanh hơn là gõ console.log

4. Git
- git init
- create .gitignore -> add node_modules/ ; .vscode
- git add . ; git commit -m "Initial commit" ; git remote add origin https://github.com/nguyendinhnhan/node_blog.git ; git push -u origin master

5. Morgan
- HTTP request logger middleware for Nodejs
- npm i morgan --save-dev
- const morgan = require('morgan') ; app.use(morgan('combined'))

6. Template engine (handlebars) - fs, pug,..
- https://www.npmjs.com/package/express-handlebars
- npm i express-handlebars
- https://github.com/nguyendinhnhan/node_blog/commit/0f69847411a6cc06b048b4c35d06457d8bdfccdd

7. Static file & SCSS
- app.use(express.static(path.join(__dirname, 'public')))
- http://localhost:3000/img/logo.png -> show logo img
- npm i node-sass --save-dev
- scss build to css file -> production use css file
- https://github.com/nguyendinhnhan/node_blog/commit/71965e40ac1a056ea99fb8ddf0dffd06af0e895d

8. Bootstrap 4
- use cdn (link http)
- copy navbar in component -> paste to header.hbs
- https://github.com/nguyendinhnhan/node_blog/commit/073c31e4c7bd6e3682b53fc594171b5e055f21ef

9. Basic routing - https://expressjs.com/en/starter/basic-routing.html

10. GET
- Default is GET
- Form, javascript => mới dùng được POST
  
11. Query parameters
- http://localhost:3000/search?q=f8%20lap%20trinh&author=test
- console.log(req.query) => { q: 'f8 lap trinh', author: 'test' }

12. Form default behavior
- <input type="text" name="q" value="f8 lap trinh">
- submit -> URL: http://localhost:3000/search?q=f8+lap+trinh -> GET and Query parameters: req.query = {q: 'f8 lap trinh'}

- POST -> <form method="POST"> <input type="text" name="q" value="f8 lap trinh">
- submit -> URL: http://localhost:3000/search -> POST and Form Data: req.body = {q: 'f8 lap trinh'}
- Issue: f5/press reload icon -> still POST
- Select text in URL and enter -> GET

- <form method="POST" action="/news"> -> submit and redirect to news page with POST method

13. POST
- submit -> data không bị đính trên URL nữa mà được gửi ngầm đi
- app.use(express.urlencoded({extended: true})) -> to use req.body
- nodejs >= 4.16 is included "body-parser", thấp hơn phải tự cài
- "body-parser" có thằng "qs" giúp parse form data đưa vào biến req.body

14. MVC
- Model, View, Controller
- ![alt text](./images/mvc.png)

15. Routes & Controllers
- https://github.com/nguyendinhnhan/node_blog/commit/079ff828f14a83059ecba18df2c8729104e4bcd3

16. Install MongoDB
- https://www.mongodb.com/try/download/compass => download & install MongoDB Compass
- https://www.mongodb.com/try/download/community => download & install MongoDB Community
- echo $PATH
- sudo mkdir -p /usr/local/mongodb
    + move mongodb folder to /usr/local -> tranh bi xoa nham...
- cp -R /path/to/download/mongodb/bin /usr/local/mongodb
    + sudo chmod 777 /usr/local/mongodb -> neu bi error Permission denied
    + ls -la /usr/local/mongodb/bin
- vi ~/.bashrc
    + a -> to insert in vim
    + export PATH="/usr/local/mongodb/bin:$PATH"
    + or neu co san local/bin:$PATH => export PATH="/usr/local/bin:/usr/local/mongodb/bin:$PATH"
    + esc -> exit insert mode
    + Shift + :wq
- source ~/.bashrc
- echo $PATH
- mongod
    - error /data/db not found
      + sudo mkdir -p /data/db
      + or run: mongod --dbpath /Users/nhannguyen/Documents/Projects/DB/data/db
        - create a foler: sudo mkdir -p /Users/nhannguyen/Documents/Projects/DB/data/db
        - sudo chmod 777 /Users/nhannguyen/Documents/Projects/DB/data/db

- open MondoDB Compass -> paste a standalone connection string
    + mongodb://127.0.0.1:27017
    + Connect

17. Prettier, lint-staged, husky
- npm i prettier lint-staged husky --save-dev
- https://github.com/nguyendinhnhan/node_blog/commit/00f79a1d13fbeb726cc8f9334d09e0eec9c91c1e

18. Model
- ports
    + mongoDB 27017
    + http 80
    + https ssl 443
    + mysql 3306
- Create Database: f8_blog_dev, collection: Courses -> Add data
- Document Database
    + Collection
        + document
            + document: có thể k cùng cấu trúc fields như SQL
            + ví dụ:
                + document1: _id, name, image
                + document2: _id, test
            + ưu điểm linh hoạt
            + với những data như khoá học trên f8 giống nhau -> nên sử dụng mongoose để giúp tổ chức theo dạng object model, và quản lý fields chặt chẽ hơn
- https://github.com/nguyendinhnhan/node_blog/commit/eb34d1b02e4117e19697e448383d8e2d45d76ef9

19. Refactor & JSON viewer
- Json viewer extension chrome
- https://github.com/nguyendinhnhan/node_blog/commit/81b47ce6367e3db588ac035cb31c2eb1cfe122ad

20. CRUD - Read DB
- https://github.com/nguyendinhnhan/node_blog/commit/09464bd0f7b7e554ca6c280d38b62bce88772dce

21. Course Detail page
- https://github.com/nguyendinhnhan/node_blog/commit/20b6749adb453d3ef3f0cbdb92fdefb95ff0ea33

22. Create a new course
- https://github.com/nguyendinhnhan/node_blog/commit/502beed2025c28e29df3f479f310ab436074548c

23. Update course
- helpers: {sum: (a, b) => a + b}}) -> add functions sum to use in view: {{sum @index 1}} -> STT sẽ bắt đầu từ 1 thay vì 0
- res.redirect("/me/stored/courses") -> thêm Location: /me/stored/courses vào trong Response Headers của Headers có thể view trong Network của Chrome
- https://github.com/nguyendinhnhan/node_blog/commit/c06842c9b83639a4c16815445b61b37b0769b4d8

24. Delete course
- https://github.com/nguyendinhnhan/node_blog/commit/269d535c73d798b08d239063871693131a857119

25. Soft delete
- https://github.com/nguyendinhnhan/node_blog/commit/61bf6e59ba1bce01493ab981fd0e507900e54bd5

26. Sort Middleware
- https://github.com/nguyendinhnhan/node_blog/commit/524baab14ea391105209b97ef7908f4e251ede36
