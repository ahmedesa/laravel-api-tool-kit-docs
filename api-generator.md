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
php artisan api:generate Customer "username:string|age:integer:nullable|company_id:foreignId|status:enum(new,old)" --all
```

In the above example, we define three columns: username, and age, company_id, each with its respective data type and options.

### Generated Files and Their Content

When using the schema option, the API Generator will generate various files tailored to the specified schema. Here's how the schema affects different files:

#### Model File
The generated model file will include the fillable attributes and relationships based on the schema. Here's an example:

```php
protected $fillable = ['username', 'company_id', 'age', 'status'];

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
$table->enum('status', ['old', 'new']);
```

#### Factory File 
The factory file will use the schema to generate sample data for testing. Each defined attribute will be assigned a corresponding Faker method. For example:
```php
'username' => $this->faker->firstName(),
'age' => $this->faker->randomNumber(),
'company_id' => createOrRandomFactory(Company::class),
'status' => $this->faker->randomElement(['old', 'new']),
```
> **Note**
> `createOrRandomFactory()` function creates a new instance or fetches a random record from a class using a factory.

#### Request Files
The generated request files will include the validation rules based on the schema.
```php
'username' => ['required', 'string'],
'age' => ['nullable', 'integer'],
'company_id' => ['required'],
'status' => ['sometimes', 'in:old,new'],
```
#### Resource File
The resource file will define the structure of the API response using the schema attributes.
```php
'username' => $this->username,
'age' => $this->age,
'status' => $this->status,
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

## Creating a New Group with Custom File Locations (upcoming feature)
When creating a new group using the API Generator, you can specify custom locations for different types of files, such as models, controllers, factories, and more. Customizing file locations within a group allows you to maintain a well-structured codebase tailored to your project's needs. 
Example :
```
php artisan api:generate ModelName --all --group=v1
```

Here's how to create a new group with custom file locations:

### Step 1: Configure Custom File Locations

To customize the file locations within your group, you need to create a path resolver class for each file type you want to customize (e.g., model, controller, factory). Each path resolver class should implement the `HasClassAndNamespace` interface and define the `folderPath()`, `fileName()`, and `getNameSpace()` methods.

Here's an example of creating custom path resolver classes for a "v1" group:

Resource Path Resolver:

```php
namespace App\CustomGroups\V1;

use Essa\APIToolKit\Generator\Contracts\HasClassAndNamespace;

class V1ResourcePathResolver implements HasClassAndNamespace
{
    public function folderPath(): string
    {
        return app_path("Http/Resources/v1/{$this->model}");
    }

    public function fileName(): string
    {
        return "{$this->model}Resource.php";
    }

    public function getNameSpace(): string
    {
        return "App\Http\Resources\v1\\{$this->model}";
    }
}
```
Controller Path Resolver:
```php
namespace App\CustomGroups\v1;

use Essa\APIToolKit\Generator\Contracts\HasClassAndNamespace;

class V1ControllerPathResolver implements HasClassAndNamespace
{
    public function folderPath(): string
    {
        return app_path('CustomGroups/v1/Controllers');
    }

    public function fileName(): string
    {
        return "{$this->model}Controller.php";
    }

    public function getNameSpace(): string
    {
        return 'App\CustomGroups\v1\Controllers';
    }
}
```
You can create similar path resolver classes for other file types such as factories, requests, resources, and more, as needed.

{: .note }
When creating custom groups, it's essential to provide path resolver classes for all types within the group, even if you only intend to customize some of them. For types you don't wish to customize, you can use the default classes from the default group.

### Step 2: Configure the Generator for the New Group
In your `config/api-tool-kit.php` configuration file, define the path resolver classes for each file type within the new group under the "generator_path_groups" section. Use the group name as the key and the path resolver classes as the values for each file type.

For example, to configure the `"v1"` group with custom path resolver classes for models and controllers, update your configuration like this:
```php
'generator_path_groups' => [
    // ...other groups...
    'v1' => [
        'model' => App\CustomGroups\v1\V1ResourcePathResolver::class,
        'resource' => App\CustomGroups\v1\V1ControllerPathResolver::class,
        // Add path resolver classes for other file types here
    ],
],
```
### Step 3: Generate Files for the New Group

Now that you've defined the group, configured the path resolver classes, and updated the configuration, you can generate API-related files for the new group using the `--group` option.

For example, to generate files for the "v1" group:
```
php artisan api:generate ModelName --all --group=v1
```
The API Generator will use the specified group's path resolver classes to organize the generated files according to the custom folder structure and namespace you defined for each file type.

Customizing file locations within a group provides flexibility in organizing your API codebase to meet specific project requirements. You can create and configure multiple groups, each with its own set of custom file locations, to maintain a modular and structured API implementation.

## Conclusion:
The API Generator feature offers a streamlined and convenient way to generate essential API-related files for your models. Whether you're working with default options or customizing the generation process, this tool enables you to quickly set up controllers, resources, requests, and more. Experiment with the customization options to efficiently create API components that align with your project's architecture and requirements.

----
