---
layout: default
title: Api Generator
nav_order: 5
has_children: false
permalink: api-generator
---

## **API Generator**
The API Generator simplifies the process of creating API-related files for a model, making it quick and easy to set up the required components. It offers the ability to generate files such as controllers, requests, resources, migrations, factories, seeders, filters, tests, and even API routes.
### Usage :
To generate API-related files for a specific model, use the following command:

```
php artisan api:generate ModelName --all
```
Replace ModelName with the name of the model for which you wish to create API components.

Upon executing the command, you'll be presented with options to tailor the generation process according to your preferences.

- If you use `--all` option it will proceed with all the default options, the generator will create files for all available options specified in the `config/api-tool-kit` configuration.
Alternatively, you can choose to customize the generation by selecting specific files to create.
- when you type the command it will ask you whether you want default options :

### All Options:
By default, the API Generator creates the following files for the specified `ModelName` using the `--all` ,If you don't use `--all`, it will only create the Model clas:

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

### Customization
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

#### Example: Using Customization Options:
Here's an example of how to generate a Car model with a controller, create and update request files, and enable soft delete :
```php
php artisan api:generate Car -cR --soft-delete
```

### Conclusion:
The API Generator feature offers a streamlined and convenient way to generate essential API-related files for your models. Whether you're working with default options or customizing the generation process, this tool enables you to quickly set up controllers, resources, requests, and more. Experiment with the customization options to efficiently create API components that align with your project's architecture and requirements.

----
