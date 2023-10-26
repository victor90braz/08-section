````markdown
# Laravel Database Interaction README

## GitHub Repository

-   Find the code and more on GitHub: [06-section Repository](https://github.com/victor90braz/07-section.git)

## Introduction

Welcome to the Laravel Database Interaction README! This guide provides comprehensive instructions for setting up your Laravel project, connecting to a MySQL database, and creating and interacting with users, posts, and categories using the Tinker tool.

## Installation

To create a new Laravel project named "app-example," run the following command:

```bash
composer create-project laravel/laravel app-example
```
````

## Running the Application

To start the development server, use the following command:

```bash
php artisan serve
```

## Connect to the Database

You can connect to your MySQL database using the following command:

```bash
mysql -u root -p
```

## Migrate the Database

To create the necessary database tables, run the migration with:

```bash
php artisan migrate
```

## Creating a New User and Adding It to the Database Using Tinker

To create a new user and add it to the database, you can use Laravel's Tinker. First, run Tinker with the following command:

```bash
php artisan tinker
```

1. Create a migration for the "categories" table:

```bash
php artisan make:migration create_categories_table
```

2. Create a model for the "Category" entity:

```bash
php artisan make:model Category
```

4. Run the migration to create the "categories" table:

```bash
php artisan migrate
```

1. Retrieve a post with its associated category:

```php
$post = \App\Models\Post::with('category')->first();
```

2. Access the post's category name:

```php
$post->category->name;
```

## Working with the Database

Here are some useful commands for working with the database:

-   Refresh and seed the database:

```bash
php artisan migrate:refresh
php artisan db:seed
```

-   Add fake data to the database:

```bash
php artisan tinker
$cat = \App\Models\Category::factory(30)->create();
```

-   Retrieve data with relationships:

```bash
php artisan tinker
\App\Models\Post::with('user', 'category')->first()
```

# search

Route::get('/', function () {

    $posts = Post::latest();

    if (request('search')) {
        $posts
            ->where('title', 'like' , '%'. request('search') . '%')
            ->orWhere('body', 'like' , '%'. request('search') . '%');
    };

    return view('posts', [
        'posts' =>   $posts->get(),
        'categories' => Category::all()
    ]);

});

# php artisan migrate:fresh

# php artisan tinker

# \App\Models\Post::factory(50)->create();
