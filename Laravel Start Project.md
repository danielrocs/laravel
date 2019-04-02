## 1) Create a model with migration file.

Go to the terminal and type the following command to generate the model and migration file.

```bash
php artisan make:model Company -m
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

Now, add the fillable property inside Share.php file.

```php
    class Company extends Model
    {
        protected $fillable = ['name'];
        protected $guarded = ['id', 'created_at', 'update_at'];
        protected $table = 'companies';
    }
```

 ## 2) Create a controller file
 
