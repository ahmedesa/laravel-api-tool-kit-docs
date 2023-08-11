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

- A model file:
   - Location: app/Models/ModelName.php 
- A controller file:
   - Location: app/Http/Controllers/API/ModelNameController.php
- A resource file:
   - Location: app/Http/Resources/ModelName/ModelNameResource.php
- A request file for creating the model:
   - Location: app/Http/Requests/ModelName/CreateModelNameRequest.php
- A request file for updating the model:
   - Location: app/Http/Requests/ModelName/UpdateModelNameRequest.php
- A filter file:
   - Location: app/Filters/ModelNameFilters.php
- A seeder file:
   - Location: database/seeders/ModelNameSeeder.php
- A factory file:
   - Location: database/factories/ModelNameFactory.php
- A test file:
    - Location: tests/Feature/ModelNameTest.php
- A migration file (created using make:migration):
    - Location: database/migrations/x_x_x_x_create_model_names_table.php

In addition, the generator automatically adds the necessary API routes to the routes/api.php file.

#### Customization
The API Generator allows you to customize the files you want to generate. You can opt to create specific components as per your project requirements. The available customization options are:

- --controller: Generate a controller file.
- --request: Generate request files for creating and updating the model.
- --resource: Generate a resource file for the model.
- --migration: Generate a migration file.
- --factory: Generate a factory file.
- --seeder: Generate a seeder file.
- --filter: Generate a filter file.
- --test: Generate a test file.
- --routes: Add the API routes to the routes/api.php file.
- --soft-delete: Enable soft delete for the model.


----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).
