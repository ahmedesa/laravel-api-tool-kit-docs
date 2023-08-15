---
layout: default
title: Filters
nav_order: 4
has_children: false
permalink: filters
---

## **Filters**
Filters allow you to refine API query results based on various attributes.

### Creating a Filter

To create a filter, use the provided Artisan command:
Generate a filter class:
```
php artisan make:filter CarFilters
```
Using Filters in Models
```php
namespace App\Models;

use Essa\APIToolKit\Filters\Filterable;

class Car extends Model
{
    use Filterable;

    protected string $default_filters = CarFilters::class;

    // Other model code...
}

```
### Applying Filters
Filters can be applied to a query using the useFilters scope method:
```php
Car::useFilters()->get();
```
### Available Filter Options
In your filter class (CarFilters in this case), you have several options you can customize:

Allowed Filters
Define the attributes you want to allow filtering by using the $allowedFilters property:
```php
protected array $allowedFilters = ['color', 'model_id'];
```
Allowed Sorts
Specify the attributes that can be used for sorting using the $allowedSorts property:
```php
protected array $allowedSorts = ['created_at'];
```
To sort in descending or descending order. For example, to sort by created_at :
```
// descending : ?sorts=created_at
// ascending  : ?sorts=-created_at
```
Allowed Includes
For eager loading relationships, set the $allowedIncludes property:
```php
protected array $allowedIncludes = ['model'];
```
Column and Relation Search
Specify columns and relationships that can be searched using the $columnSearch and $relationSearch properties:
```php
protected array $columnSearch = ['name', 'description'];
protected array $relationSearch = [
    'user' => ['first_name', 'last_name']
];
```
### Creating Custom Filters
You can create custom filters by adding new methods to your filter class. For example, to filter cars by their manufacturing year:
```php
public function year($term)
{
    $this->builder->whereYear('manufacturing_date', $term);
}
```
### Using Filters in Requests
By default, the filtering, sorting, inclusion, and search parameters are expected to be provided through the query parameters of your API request. The filters are then processed and applied using the provided query parameter, For example, to filter cars by color:
```
GET /cars?color=red
```
### Available Filtering Operations and Keys

## Filtering Operations and Keys

| Operation      | Key            | Description                                                   | Example                                     |
|----------------|----------------|---------------------------------------------------------------|---------------------------------------------|
| Search         | `search`       | Filters results by searching for a keyword across columns.    | `GET /cars?search=red`                      |
| Sorting        | `sorts`        | Sorts results based on specified attributes.                  | `GET /cars?sorts=created_at`                |
| Filtering      | Custom filters | Applies custom filters based on defined attributes.           | `GET /cars?color=red&model_id=1`            |
| Inclusion      | `includes`     | Eager loads specified relationships.                          | `GET /cars?includes=model,otherModel`                  |


### Customizing Filters with FiltersDTO
However, you can also override this default behavior by manually creating a FiltersDTO instance and passing it to the useFilters scope method. This gives you more control over the filter data and allows you to apply filters without relying on the query parameters.

Here's an example of how you can use the FiltersDTO to apply custom filters:
```php
use Essa\APIToolKit\Tests\Mocks\Models\TestModel;
use Essa\APIToolKit\DTO\FiltersDTO;

// Create a FiltersDTO instance manually
$filtersDTO = new FiltersDTO(
    sorts: 'created_at', // Sort by created_at in ascending order
    filters: ['name' => 'Car'], // Filter by name
    includes: ['relation'], // Include sluggableTestModel relation
    search: '2023' // Search for the year 2023
);

// Pass the custom FiltersDTO to the useFilters scope method
$records = TestModel::useFilters(filteredDTO: $filtersDTO)->get();

```
### DateFilter and TimeFilter

The `DateFilter` and `TimeFilter` traits simplify querying records within a specific date or time range.

To use these traits, include them in your filter class:

```php
use Essa\APIToolKit\Traits\DateFilter;
use Essa\APIToolKit\Traits\TimeFilter;

class TestModelFilters extends QueryFilters
{
    use DateFilter;
    use TimeFilter;

    // ...
}
```
Example: Retrieve records created between '2023-08-01' and '2023-08-15' within a time range of '09:00:00' to '12:00:00':
```php 
/api/test-models?from_date=2023-08-01&to_date=2023-08-15&from_time=09:00:00&to_time=12:00:00
```
These traits enhance the flexibility of your API's querying capabilities and allow you to easily retrieve records based on date and time attributes.

----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).
