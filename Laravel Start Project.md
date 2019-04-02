## 1) Create a model with migration file.

Go to the terminal and type the following command to generate the model and migration file.

php artisan make:model Company -m

It will create the model and migration file. Now, update the schema inside <timestamp>create_companies_table.php file.

    public function up()
    {
        Schema::create('companies', function (Blueprint $table) {
            $table->increments('id');
            $table->string('name');
            $table->timestamps();
        });
    }
    
 
