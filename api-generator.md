---
layout: default
title: Api Generator
nav_order: 5
has_children: false
permalink: api-generator
---
# API Generator
{: .no_toc }

The API Generator simplifies the process of creating API-related files for a model, making it quick and easy to set up the required components. It offers the ability to generate files such as controllers, requests, resources, migrations, factories, seeders, filters, tests, and even API routes.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Usage 
To generate API-related files for a specific model, use the following command:

```
php artisan api:generate ModelName --all
```
Replace ModelName with the name of the model for which you wish to create API components.

Upon executing the command, you'll be presented with options to tailor the generation process according to your preferences.

- If you use `--all` option it will proceed with all the default options, the generator will create files for all available options specified in the `config/api-tool-kit` configuration.
Alternatively, you can choose to customize the generation by selecting specific files to create.
- When you type the command it will ask you whether you want default options :

## All Options:
By default, the API Generator creates the following files for the specified `ModelName` using the `--all` ,If you don't use `--all`, it will only create the Model class:

| Default Options | Location |
|-----------------|----------|
| Model File | `app/Models/ModelName.php` |
| Controller File | `app/Http/Controllers/API/ModelNameController.php` |
| Resource File | `app/Http/Resources/ModelName/ModelNameResource.php` |
| Create Model Request File | `app/Http/Requests/ModelName/CreateModelNameRequest.php` |
| Update Model Request File | `app/Http/Requests/ModelName/UpdateModelNameRequest.php` |
| Filter File | `app/Filters/ModelNameFilters.php` |
| Seeder File | `database/seeders/ModelNameSeeder.php` |
| Factory File | `database/factories/ModelNameFactory.php` |
| Test File | `tests/Feature/ModelNameTest.php` |
| Migration File | `database/migrations/x_x_x_x_create_model_names_table.php` |
| Routes | Automatically added to `routes/api.php` |

In addition, the generator automatically adds the necessary API routes to the routes/api.php file.

## Folder Structure of Generated Files
```
.
├── app
│   ├── Http
│   │   ├── Controllers
│   │   │   └── API
│   │   │       └── CarController.php
│   │   ├── Requests
│   │   │   └── Car
│   │   │       ├── CreateCarRequest.php
│   │   │       └── UpdateCarRequest.php
│   │   └── Resources
│   │       └── Car
│   │           └── CarResource.php
│   └── Models
│       └── Car.php
├── database
│   ├── factories
│   │   └── CarFactory.php
│   ├── migrations
│   │   └── x_x_x_x_create_cars_table.php
│   └── seeders
│       └── CarSeeder.php
├── tests
│   └── Feature
│       └── CarTest.php
├── app
│   └── Filters
│       └── CarFilters.php
└── routes
    └── api.php
```
## Schema Option
The schema option in the API Generator simplifies the process of generating API-related files for your model by allowing you to define your database columns and their attributes directly in the command. This option lets you specify the schema in a format that closely resembles Laravel's database migrations.
### How to Use Schema
The schema is defined as a comma-separated list of column definitions in the format `COLUMN_NAME:COLUMN_TYPE:OPTIONS`. Here's an example of how to define a schema:

```
php artisan api:generate Customer "username:string|age:integer:nullable|company_id:foreignId" --all
```

In the above example, we define three columns: username, and age, company_id, each with its respective data type and options.

### Generated Files and Their Content

When using the schema option, the API Generator will generate various files tailored to the specified schema. Here's how the schema affects different files:

#### Model File
The generated model file will include the fillable attributes and relationships based on the schema. Here's an example:

```php
protected $fillable = ['username', 'company_id', 'age'];

public function company()
{
    return $this->belongsTo(Company::class);
}

```
#### Migration File 
The migration file will be created with columns and options according to the schema definition. For instance:
```php
$table->string('username');
$table->integer('age')->nullable();
$table->foreignId('company_id')->constrained('companies');
```

#### Factory File 
The factory file will use the schema to generate sample data for testing. Each defined attribute will be assigned a corresponding Faker method. For example:
```php
'username' => $this->faker->firstName(),
'age' => $this->faker->randomNumber(),
'company_id' => createOrRandomFactory(Company::class),
```
> **Note**
> `createOrRandomFactory()` function creates a new instance or fetches a random record from a class using a factory.

#### Request Files
The generated request files will include the validation rules based on the schema.
```php
'username' => ['required', 'string'],
'age' => ['nullable', 'integer'],
'company_id' => ['required'],
```
#### Resource File
The resource file will define the structure of the API response using the schema attributes.
```php
'username' => $this->username,
'age' => $this->age,
'company_id' => $this->company_id,
'created_at' => dateTimeFormat($this->created_at),
'updated_at' => dateTimeFormat($this->updated_at),
```
> **Note**
> `dateTimeFormat()` function used to format datetime formats you can change the format from `api-tool-kit` config file.

## Customization
The API Generator allows you to customize the files you want to generate. You can opt to create specific components as per your project requirements. The available customization options are:

| Customization Options | Shortcuts | Description |
|-----------------------|-----------|-------------|
| `--controller` | `-c` | Generate a controller file. |
| `--request` | `-R` | Generate request files for model creation and updating. |
| `--resource` | `-r` | Generate a resource file for the model. |
| `--migration` | `-m` | Generate a migration file. |
| `--factory` | `-f` | Generate a factory file. |
| `--seeder` | `-s` | Generate a seeder file. |
| `--filter` | `-F` | Generate a filter file. |
| `--test` | `-t` | Generate a test file. |
| `--routes` | | Add API routes to `routes/api.php`. |
| `--soft-delete` | | Enable soft delete for the model. |

### Example: Using Customization Options:
Here's an example of how to generate a Car model with a controller, create and update request files, and enable soft delete :
```php
php artisan api:generate Car -cR --soft-delete
```

## Conclusion:
The API Generator feature offers a streamlined and convenient way to generate essential API-related files for your models. Whether you're working with default options or customizing the generation process, this tool enables you to quickly set up controllers, resources, requests, and more. Experiment with the customization options to efficiently create API components that align with your project's architecture and requirements.

----
