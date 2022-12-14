https://www.twilio.com/blog/build-graphql-powered-api-laravel-php

Creating a New Laravel Project
composer create-project --prefer-dist laravel/laravel lara-bookstore

Move into project
$ cd lara-bookstore

Run the application
$ php artisan serve

Install GraphQL Laravel library
$ composer require rebing/graphql-laravel

publish a copy of the configuration file from the vendor folder
$ php artisan vendor:publish --provider="Rebing\GraphQL\GraphQLServiceProvider"

Creating Book Model
$ php artisan make:model Book -m

Modify the newly generated migration file as indicated in database\migrations\create_books_table migration.

Modify the newly generated Book model file as indicated in App\Models\Book.

Create a Seeder File for the Books Table
$ php artisan make:seeder BookSeeder

Make changes as indicated in database\seeders\BookSeeder.php

Update database/seed/DatabaseSeeder.php file as indicated.

Run migrations and seeder after configuring the database.
$ php artisan migrate --seed

Building GraphQL Server
Create GraphQL folder in App

In GraphQL folder create the following folders:

Mutations --  holds classes that will be used to carry out the insert, update, and delete operations.

Queries -- holds classes used to fetch data from the database.

Types -- Types are objects that represent the kind of objects that can be retrieved from the database.

Creating a GraphQL Type for the Application
Create a new file BookType.php within the app/GraphQL/Types folder as indicated.

The $attributes array defines the name, a brief description, and the model linked, with the type defined here and a function that returns the properties of the fields as an array.

The Book Query
Create a file with the name BookQuery.php within the app/GraphQL/Queries folder and change as indicated.

Here, we defined the query name and referenced the type Book that was created earlier as the GraphQL type to be used. The function args() returns the unique identifier that will be used for a particular book, which is an id in this case. Once resolved, the query will search for the book using the identifier and return its details.

The Books Query
Unlike the class defined in the previous section, here we will define a query to retrieve a collection of books. Navigate into the app/GraphQL/Queries folder and create a file with the name BooksQuery.php.

Creating the Mutation
Any query implemented that causes data to be written or altered is often sent through mutation. Mutations can be created to insert, update, and delete a record in the database. Let???s start by defining one to create a new record for a book.

Create a Book
Create a new file within the app/GraphQL/Mutations folder and name it CreateBookMutation.php. 
It is important to note the name of the mutation as it makes it easy to reference this class later. In addition to defining the GraphQL type, we also returned the properties of each field before finally creating an instance of the Book model and filling it with the arguments passed along with the query.

Update a Particular Book
To define a mutation to update the records of a particular book, create a new file within the app/GraphQL/Mutations folder and name it UpdateBookMutation.php. 
Similar to what we had in the previous section, we created an attribute that specified the name of the query and created the field properties for the query arguments. Finally, we used the unique id to retrieve the book of interest and update its details.

Delete a Book
The last mutation to be created is for deleting a specific book. Create a new file within the app/GraphQL/Mutations folder and name it DeleteBookMutation.php.


Registering the Schema and Type
After creating all of the schemas, they need to be registered within the configuration file of the GraphQL library used for this project. To do that, open the config/graphql.php file, locate the schemas, and update as shown here. Do the same for the types property as well:


Run the Application
Start the application with php artisan serve. This will start the local PHP server and run the Laravel application at http://localhost:8000.

Installing GraphiQL IDE
To test the application, we need to install a tool that can be used for testing GraphQL endpoints. One of the popular tools in the tech community created for this purpose isGraphiQL. It is a GUI for editing and testing GraphQL queries and mutations. 

Installing GraphiQL IDE
https://www.electronjs.org/apps/graphiql


Once you are done, open it and use http://localhost:8000/graphql as the GraphQL Endpoint.

Testing the Endpoints

Retrieve the list of books -- GET request
{
  books {
    id
    title,
    author
  }
}

Return a specific book -- GET request
{
  book(id: 6) {
    title,
    author
  }
}

Create a book -- POST request
mutation createBook {
  createBook(title: "John Doe book", author: "johndoe@test.com", 
    language: "secret", year_published: "2020", isbn: "635353353") {
    id
    title
    author
  }
}

Update a Book -- POST request
mutation updateBook {
  updateBook(id: 2, title: "Mine", author: "sample book", language: "secret", year_published: "2020", isbn: "635353353") {
    id
    title
    author
  }
}


Special Thanks to the author of this tutorial:
Olususi Oluyemi

Olususi Oluyemi is a tech enthusiast, programming freak, and a web development junkie who loves to embrace new technology.

Twitter: https://twitter.com/yemiwebby
GitHub: https://github.com/yemiwebby
Website: https://yemiwebby.com.ng/

