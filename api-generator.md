---
layout: default
title: Api Generator
nav_order: 5
has_children: false
permalink: api-generator
---

## **API Generator**
The API Generator simplifies the process of creating API-related files for a model, making it quick and easy to set up the required components. It offers the ability to generate files such as controllers, requests, resources, migrations, factories, seeders, filters, tests, and even API routes.
#### Usage :
To generate API-related files for a specific model, use the following command:

```
php artisan api:generate ModelName
```
Upon running the command, you will be prompted with options to customize the generation process.

- If you choose to proceed with the default options, the generator will create files for all available options specified in the config/api-tool-kit configuration.
Alternatively, you can choose to customize the generation by selecting specific files to create.
- when you type the command it will ask you whether you want default options :
#### Default Options:
By default, the API Generator creates the following files for the specified ModelName:

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

#### Customization
The API Generator allows you to customize the files you want to generate. You can opt to create specific components as per your project requirements. The available customization options are:

| Customization Options | Description |
|-----------------------|-------------|
| `--controller` | Generate a controller file. |
| `--request` | Generate request files for model creation and updating. |
| `--resource` | Generate a resource file for the model. |
| `--migration` | Generate a migration file. |
| `--factory` | Generate a factory file. |
| `--seeder` | Generate a seeder file. |
| `--filter` | Generate a filter file. |
| `--test` | Generate a test file. |
| `--routes` | Add API routes to `routes/api.php`. |
| `--soft-delete` | Enable soft delete for the model. |

----
