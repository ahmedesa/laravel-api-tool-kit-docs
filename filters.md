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
To sort in descending or descending order . For example, to sort by created_at :
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
Filters can be applied by including query parameters in the API request. For example, to filter cars by color:
```
GET /cars?color=red
```
### Additional Tips
When searching for a value within a column or relationship, use the search query parameter.
### **DateFilter and TimeFilter**

The `DateFilter` and `TimeFilter` traits simplify querying records within a specific date or time ranges.

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
