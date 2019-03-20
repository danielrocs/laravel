Laravel has awesome set of artisan commands, probably the most often used are make:xxx – like make:model or make:migration etc. But do you know all 16 of them? And, moreover, do you know their parameters which may help to make the code even quicker?

First, there is a command php artisan list which gives us all the commands, like this:

```
  make:auth              Scaffold basic login and registration views and routes
  make:command           Create a new Artisan command
  make:controller        Create a new controller class
  make:event             Create a new event class
  make:job               Create a new job class
  make:listener          Create a new event listener class
  make:mail              Create a new email class
  make:middleware        Create a new middleware class
  make:migration         Create a new migration file
  make:model             Create a new Eloquent model class
  make:notification      Create a new notification class
  make:policy            Create a new policy class
  make:provider          Create a new service provider class
  make:request           Create a new form request class
  make:seeder            Create a new seeder class
  make:test              Create a new test class
```
  

But it doesn’t give us any information about the parameters or options for these commands. So I want to make an overview of each of them here, starting with the most often used ones.

For that, we will dive into actual code of the framework, inside /vendor/laravel/framework/src/Illuminate folder, and will check what options and undocumented features we have for each command.
1. make:controller

This command creates a new controller file in app/Http/Controllers folder.

Example usage:
```
php artisan make:controller UserController
```
Parameters:
```
--resource
```
The controller will contain a method for each of the available resource operations – index(), create(), store(), show(), edit(), update(), destroy().
```
--model=Photo
```
If you are using route model binding and would like the resource controller’s methods to type-hint a model instance.
```
--parent=Photo
```
Officially undocumented parameter, in the code it says “Generate a nested resource controller class” but for me it failed to generate a Controller properly. So probably work in progress.
2. make:model

Create a new Eloquent model class.

Example usage:
```
php artisan make:model Photo
```
Parameters:
```
--migration
```
Create a new migration file for the model.
```
--controller
```
Create a new controller for the model.
```
--resource
```
Indicates if the generated controller should be a resource controller.

Yes, you’ve got it right, you can do it like this:

php artisan make:model Project --migration --controller --resource

Or even shorter:

php artisan make:model Project -mcr

3. make:migration

Create a new migration file.

Example usage:
```
php artisan make:migration create_projects_table
```
Parameters:
```
--create=Table
```
The table to be created.
```
--table=Table
```
The table to migrate.
```
--path=Path
```
The location where the migration file should be created.
4. make:seeder

Create a new database seeder class.

Example usage:
```
php artisan make:seeder BooksTableSeeder
```
Parameters: none.
5. make:request

Create a new form request class in app/Http/Requests folder.

Example usage:
```
php artisan make:request StoreBlogPost
```
Parameters: none.
6. make:middleware

Create a new middleware class.

Example usage:
```
php artisan make:middleware CheckAge
```
Parameters: none.
7. make:policy

Create a new policy class.

Example usage:
```
php artisan make:policy PostPolicy
```
Parameters:
```
--model=Photo
```
The model that the policy applies to.
8. make:auth

Example usage:
```
php artisan make:auth
```
Scaffold basic login and registration views and routes.

Parameters:
```
--views
```
Only scaffold the authentication views.
```
--force
```
Overwrite existing views by default.
9. make:command

Create a new Artisan command.

Example usage:
```
php artisan make:command SendEmails
```
Parameters:
```
--command=Command
```
The terminal command that should be assigned.
10. make:event

Create a new event class.

Example usage:
```
php artisan make:event OrderShipped
```
Parameters: none.
11. make:job

Create a new job class.

Example usage:
```
php artisan make:job SendReminderEmail
```
Parameters:
```
--sync
```
Indicates that job should be synchronous.
12. make:listener

Create a new event listener class.

Example usage:
```
php artisan make:listener SendShipmentNotification 
```
Parameters:
```
--event=Event
```
The event class being listened for.
```
--queued
```
Indicates the event listener should be queued.
13. make:mail

Create a new email class.

Example usage:
```
php artisan make:mail OrderShipped
```
Parameters:
```
--markdown
```
Create a new Markdown template for the mailable.
14. make:notification

Create a new notification class.

Example usage:
```
php artisan make:notification InvoicePaid
```
Parameters:
```
--markdown
```
Create a new Markdown template for the notification.
15. make:provider

Create a new service provider class.

Example usage:
```
php artisan make:provider RiakServiceProvider
```
Parameters: none.
16. make:test

Create a new test class.

Example usage:
```
php artisan make:test UserTest
```
Parameters:
```
--unit
```
Create a unit (or, otherwise, feature) test.

So, that’s it – 16 commands covered. Is there anything missing? Or would you like to see some new parameters for your favorite commands? Share in the comments!

P.S. We’re recently released a package that adds a new command in this suite – make:api. 
