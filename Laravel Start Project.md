## 1) Create a model with migration file.

Go to the terminal and type the following command to generate the model and migration file.

```bash
    $ php artisan make:model Company -m
```

It will create the model and migration file. Now, update the schema inside <timestamp>create_companies_table.php file.

```php
    public function up()
    {
        Schema::create('companies', function (Blueprint $table) {
            $table->increments('id');
            $table->string('name');
            $table->timestamps();
        });
    }
```

Now, add the fillable property inside Company.php file.

```php
    class Company extends Model
    {
        protected $fillable = ['name'];
        protected $guarded = ['id', 'created_at', 'update_at'];
        protected $table = 'companies';
    }
```

## 2) Create routes and controller
 
First, create the CompanyController using the following command.

```bash
    $ php artisan make:controller CompanyController --resource
```

Now, inside the folder routes edit the web.php file, add add the following line of code.

```php
    Route::resource('companies', 'CompanyController');
```

Actually, by adding the following line, we have registered the multiple routes for our application. We can check it using the following command.

```bash
    $ php artisan route:list
``` 
 
 ## 3) Create the views
 
Inside the folder resources -> views folder, create one folder called company.

Inside that folder, create the following three files.

    create.blade.php
    edit.blade.php
    index.blade.php
 
