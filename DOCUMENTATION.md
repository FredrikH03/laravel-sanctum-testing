This is my documentation for my laravel program with sanctum as the authorization api

--- Prerequisites ---

The programs you need installed for the project:
PHP,
Composer,
MySQL (or other Database of choice),
Laravel framework


--- Setup ---

configure your database connection information in the .env
file

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=your_database_name
DB_USERNAME=your_username
DB_PASSWORD=your_password

Next run "composer install"
if you run into version control issues, run the command
with the following flag 
"--ignore-platform-req=<problematic-dependency"


setup the database structure with "php artisan migrate"

now you can run "php artisan serve" and the server will
by default start on "http://127.0.0.1:8000"


Using the API
You can use either use curl commands or postman for this
I will be writing this with postman in mind

! some requests require you to set the following information
Headers: "Accept" : "application/json"

To retrieve all products in the database
[GET] http://127.0.0.1:8000/api/products


To register a new user
[POST] http://127.0.0.1:8000/api/register
with the following extras
Headers: "Accept" : "application/json"

Body:
"name" : "username"
"email" : "user@email.com"
"password" : "userpassword"
"password_confirmation" : "userpassword"

without the accept header, you will get sent to the main 
page

the password_confirmation is also needed, otherwise the 
register will fail

This will spit out a token, which will be needed to access 
protected routes


Now we can try to add a new products
[POST] http://127.0.0.1:8000/api/products
with the following extras

Headers: "Accept" : "application/json"

Body: 
"name" : "Product One"
"slug" : "product-one"
"description" : "Description for Product One"
"price" : "99.90" (needs to be a number)

Authorization: 
Type: "Bearer Token" : "<insert_token>"

You can also try to run the command without any token,
in which case you will get a "Unauthorized" returned


To update a product
[PUT] http://127.0.0.1:8000/api/products/{id}
with the following extras

Headers: "Accept" : "application/json"

Body (here you can input whatever you want changed, even if
that is one parameter or all parameters):
"name" : "New Name"
"slug" : "new-slug"
"description" : "new description"
"price" : "new price" (still needs to be a number)

Authorization:
Type: "Bearer Token" : "<insert_token>"


To delete a product
[DELETE] http://127.0.0.1:8000/api/products/{id}
with the following extras

Headers: "Accept" : "application/json"

Authorization:
Type: "Bearer Token" : "<insert_token>"


To logout your user
[POST] http://127.0.0.1:8000/api/logout
with the following extras

Headers: "Accept" : "application/json"

Authorization:
Type: "Bearer Token" : "<insert_token>"

This will kill the token and make it unusable


To login with an already existing user account
[POST] http://127.0.0.1:8000/api/login
with the following extras

Headers: "Accept" : "application/json"

Body:
"email" : "existing@email.com"
"password" : "matching_password"

This checks if the credentials match and if they do you 
get a new token 




thats about all, first time writing documentation, I hope
it doesn't suck and everything is documented correctly




