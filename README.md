<p align="center">
    <img src="https://user-images.githubusercontent.com/41773797/104140339-f54ce300-53a8-11eb-8049-8d0994a6cd36.png" alt="Squire banner" style="width: 100%; max-width: 800px;" />
</p>

<p align="center">
    <a href="https://github.com/squirephp/squire/actions"><img alt="Tests passing" src="https://img.shields.io/badge/Tests-passing-green?style=for-the-badge&logo=github"></a>
    <a href="https://laravel.com"><img alt="Laravel 8.x" src="https://img.shields.io/badge/Laravel-v8.x-FF2D20?style=for-the-badge&logo=laravel"></a>
    <a href="https://laravel.com"><img alt="PHP 8" src="https://img.shields.io/badge/PHP-8-777BB4?style=for-the-badge&logo=php"></a>
    <a href="https://github.com/squirephp/squire"><img alt="Squire 2.x" src="https://img.shields.io/badge/stable-v2.x-1F2223?style=for-the-badge"></a>
</p>

Squire is a library of static Eloquent models for fixture data that is commonly needed in web applications, such as countries, currencies and airports. It's based on the concepts of [Caleb Porzio's Sushi package](https://github.com/calebporzio/sushi).

Common use cases for Squire include:
- Populating dropdown options, such as a country selector on an address form.
- Attaching extra data to other models in your app, such as airport information to a `Flight` model. See the section on [model relationships](#model-relationships).
- [Validating user input.](#validation)

## Contents

- [Installing a Model](#installing-a-model)
- [Using a Model](#using-a-model)
- [Available Models](#available-models)
  - [`Squire\Models\Airline`](#squiremodelsairline)
  - [`Squire\Models\Airport`](#squiremodelsairport)
  - [`Squire\Models\Continent`](#squiremodelscontinent)
  - [`Squire\Models\Country`](#squiremodelscountry)
  - [`Squire\Models\Currency`](#squiremodelscurrency)
  - [`Squire\Models\GbCounty`](#squiremodelsgbcounty)
  - [`Squire\Models\Region`](#squiremodelsregion)
- [Model Relationships](#model-relationships)
- [Validation](#validation)
- [Creating your own Models](#creating-your-own-models)
- [Upgrading from 1.x](#upgrading-from-1x)
- [Need Help?](#need-help)

## Installing a Model

You can use Composer to install Squire models into your application. Each model is available in a variety of languages, and you need only install the ones you will use.

As an example, you can install the `Squire\Models\Country` model in English:

```
composer require squirephp/countries-en
```

**A complete list of [available models](#available-models) is below.**

## Using a Model

You can interact with a Squire model just like you would any other Eloquent model, except that it only handles read-only operations.

```php
use Squire\Models\Country;

Country::all(); // Get information about all countries.

Country::find('us'); // Get information about the United States.

Country::where('name', 'like', 'a%')->get(); // Get information about all countries beginning with the letter "a".
```

## Available Models

### `Squire\Models\Airline`

#### Installation

| Locale | Installation Command |
|--|--|
| English | `composer require squirephp/airlines-en` |

#### Schema

| Column Name | Description | Example |
|--|--|--|
| `alias` | Alternative name of the airline. | `EasyJet Airline` |
| `call_sign` | Call sign of the airline. | `EASY` |
| `code_iata` | [IATA code](https://en.wikipedia.org/wiki/List_of_airline_codes) of the airline. | `u2` |
| `code_icao` | [ICAO code](https://en.wikipedia.org/wiki/List_of_airline_codes) of the airline. |`ezy` |
| `country_id` | [ISO 3166-1 alpha-2 country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) of the airline. | `gb` |
| `name` | Name of the airline. | `easyJet` |

#### Relationships

| Relationship name | Model |
|--|--|
| `country` | [`Squire\Models\Country`](#squiremodelscountry) |
| `continent` | [`Squire\Models\Continent`](#squiremodelscontinent) |


### `Squire\Models\Airport`

#### Installation

| Locale | Installation Command |
|--|--|
| English | `composer require squirephp/airports-en` |

#### Schema

| Column Name | Description | Example |
|--|--|--|
| `code_gps` | GPS code of the airport. | `ayse` |
| `code_iata` | [IATA code](https://en.wikipedia.org/wiki/IATA_airport_code) of the airport. | `nis` |
| `code_icao` | Local code of the airport. |`sbi` |
| `municipality` | Municipality of the airport. | `Simberi Island` |
| `name` | Name of the airport. | `Simberi Airport` |
| `region_id` | [ISO 3166-2 region code](https://en.wikipedia.org/wiki/ISO_3166-2) of the airport. | `pg-nik` |
| `type` | Type of airport. | `small_airport` |

#### Relationships

| Relationship name | Model |
|--|--|
| `country` | [`Squire\Models\Country`](#squiremodelscountry) |
| `region` | [`Squire\Models\Region`](#squiremodelsregion) |

### `Squire\Models\Continent`

#### Installation

| Locale | Installation Command |
|--|--|
| English | `composer require squirephp/continents-en` |

#### Schema

| Column Name | Description | Example |
|--|--|--|
| `code` | Two letter continent code. | `na` |
| `name` | Continent name. | `North America` |

#### Relationships

| Relationship name | Model |
|--|--|
| `countries` | [`Squire\Models\Country`](#squiremodelscountry) |
| `regions` | [`Squire\Models\Region`](#squiremodelsregion) |

### `Squire\Models\Country`

#### Installation

| Locale | Installation Command |
|--|--|
| English | `composer require squirephp/airlines-en` |
| French | `composer require squirephp/airlines-fr` |
| German | `composer require squirephp/airlines-de` |
| Spanish | `composer require squirephp/airlines-es` |

#### Schema

| Column Name | Description | Example |
|--|--|--|
| `calling_code` | [E.164](https://en.wikipedia.org/wiki/E.164) country calling code. | `1` |
| `capital_city` | Capital city of the country. | `Washington` |
| `code_2` | [ISO 3166-1 alpha-2 country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). | `us` |
| `code_3` | [ISO 3166-1 alpha-3 country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3). | `usa` |
| `continent_id` | Two letter continent code of the country. | `na` |
| `currency_id` | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) alphabetic currency code of the country. | `usd` |
| `flag` | Unicode flag of the country. | `🇺🇸` |
| `name` | Country name. | `United States` |

#### Relationships

| Relationship name | Model |
|--|--|
| `airlines` | [`Squire\Models\Airline`](#squiremodelsairline) |
| `airports` | [`Squire\Models\Airport`](#squiremodelsairport) |
| `continent` | [`Squire\Models\Continent`](#squiremodelscontinent) |
| `currency` | [`Squire\Models\Currency`](#squiremodelscurrency) |
| `regions` | [`Squire\Models\Region`](#squiremodelsregion) |

### `Squire\Models\Currency`

#### Installation

| Locale | Installation Command |
|--|--|
| English | `composer require squirephp/currencies-en` |

#### Schema

| Column Name | Description | Example |
|--|--|--|
| `code_alphabetic` | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) alphabetic currency code. | `usd` |
| `code_numeric` | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) numeric currency code. | `840` |
| `decimal_digits` | Number of decimal digits to use when formatting this currency. | `2` |
| `name` | Currency name. | `US Dollar` |
| `name_plural` | Plural currency name. | `US Dollars` |
| `rounding` | The formatting precison of this currency. | `0` |
| `symbol` | International currency symbol. | `$` |
| `symbol_native` | Native currency symbol. | `$` |

#### Relationships

| Relationship name | Model |
|--|--|
| `countries` | [`Squire\Models\Country`](#squiremodelscountry) |

### `Squire\Models\GbCounty`

#### Installation

| Locale | Installation Command |
|--|--|
| English | `composer require squirephp/gb-counties-en` |

#### Schema

| Column Name | Description | Example |
|--|--|--|
| `code` | [ISO 3166-2 county code](https://en.wikipedia.org/wiki/ISO_3166-2). | `gb-ess` |
| `name` | County name. | `Essex` |
| `region_id` | [ISO 3166-2 region code](https://en.wikipedia.org/wiki/ISO_3166-2) of the county. | `gb-eng` |

#### Relationships

| Relationship name | Model |
|--|--|
| `region` | [`Squire\Models\Region`](#squiremodelsregion) |

### `Squire\Models\Region`

#### Installation

| Locale | Installation Command |
|--|--|
| English | `composer require squirephp/regions-en` |

#### Schema

| Column Name | Description | Example |
|--|--|--|
| `code` | [ISO 3166-2 region code](https://en.wikipedia.org/wiki/ISO_3166-2). | `us-ny` |
| `country_id` | [ISO 3166-1 alpha-2 country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). | `us` |
| `name` | Region name. | `New York` |

#### Relationships

| Relationship name | Model |
|--|--|
| `airports` | [`Squire\Models\Airport`](#squiremodelsairport) |
| `continent` | [`Squire\Models\Continent`](#squiremodelscontinent) |
| `country` | [`Squire\Models\Country`](#squiremodelscountry) |
| `gbCounties` | [`Squire\Models\GbCounty`](#squiremodelsgbcounty) |

## Model Relationships

Implementing an Eloquent relationship between a model in your app and a Squire model is very simple. There are a couple of approaches you could take.

### Using Inheritance

The simplest option is to create a new model in your app, and let it extend the Squire model. Your new app model will now behave like the original Squire model, except you can register new methods and customise it to your liking:

```php
<?php

namespace App\Models;

use Squire\Models\Country as SquireCountry;

class Country extends SquireCountry
{
    public function users()
    {
        return $this->hasMany(User::class);
    }
}
```

### Using `resolveRelationUsing()`

Another option is the `resolveRelationUsing()` method. This allows you to dynamically register a relationship for a Squire model from anywhere in your app, for example, within a service provider:

```php
use App\Models\User;
use Squire\Models\Country;

Country::resolveRelationUsing('users', function (Country $country) {
    return $country->hasMany(User::class);
});
```

## Validation

Squire includes a validation rule for each model installed in your app. These allow you to easily validate user input to ensure that it matches a record in a specific model.

Rules can be found in the `Squire\Rules` namespace. To use one, simply construct a new rule class and pass in the model column name that you would like to validate against:

```php
use Squire\Rules;

$request->validate([
    'country' => ['required', 'string', new Rules\Country('name')],
]);
```

This code will validate the `country` input against the `name` column on the [`Squire\Models\Country` model](#squiremodelscountry). If the user enters a country that does not exist, a validation error will be thrown.

## Creating your own Models

Squire may not always have a model available for the information you require. In this case, you may want to create your own.

### Creating a Model

Squire models are very simple classes that extend `Squire\Model`. Install it with:

```
composer require squirephp/model
```

Your model class should contain a single static property, `$schema`. This contains the column structure for your model, and should match the format of the source data.

```php
<?php

namespace App\Models;

use Squire\Model;

class Language extends Model
{
    public static $schema = [
        'id' => 'string',
        'name' => 'string',
    ];
}
```

### Attaching a Model Source

Your model will require at least one data source to be registered. Each registered data source is associated with a locale. To register a data source, you will need to interact with `Squire\Repository`. Install it with:

```
composer require squirephp/repository
```

Inside a service provider, register an English source for your model:

```php
<?php

namespace App\Providers;

use App\Models\Language;
use Illuminate\Support\ServiceProvider;
use Squire\Repository;

class ModelServiceProvider extends ServiceProvider
{
    public function boot()
    {
        Repository::registerSource(Language::class, 'en', __DIR__.'/../../resources/squire-data/languages-en.csv');
    }
}
```

In this example, the `/resources/squire-data/languages-en.csv` file should be present in your app, and contain the English data served to the model. The column structure should match the `$schema` defined in your model:

```csv
id,name
de,German
en,English
fr,French
es,Spanish
```

### Creating a Validation Rule

[Rules](#validation) allow you to validate user input to ensure that it matches a record in a specific model. Rule classes extend `Squire\Rule`. Install it with:

```
composer require squirephp/rule
```

Your rule class should contain, at minimum, a `$message` to be served if the validation fails, and a `getQueryBuilder()` method for your model.

```php
<?php

namespace App\Rules;

use App\Models;
use Squire\Rule;

class Language extends Rule
{
    protected $message = 'validation.language';

    protected function getQueryBuilder()
    {
        return Models\Language::query();
    }
}
```

If no column is passed to your rule when it's used, `id` will be used by default. To customise this, override the `$column` property on your rule:

```php
<?php

namespace App\Rules;

use Squire\Rule;

class Language extends Rule
{
    protected $column = 'name';
}
```

### Releasing a Model

Squire models, their sources, and validation rules are all simply releasable in Composer packages. To see an example of this in action, check out the [`squirephp/countries`](https://github.com/squirephp/countries) and [`squirephp/countries-en`](https://github.com/squirephp/countries-en) packages.

## Upgrading from 1.x

First, you must remove the 1.x package with Composer:

```
composer remove danharrin/squire
```

Next, assess which models you are currently using in your application. Install them using the [individual command listed for each](#available-models). If your app requires localisation features offered by Squire, you may install more than one translation of each model.

As an example, we will install the `Squire\Models\Country` and `Squire\Models\Continent` models in English:

```
composer require squirephp/countries-en squirephp/continents-en
```

### Breaking Changes Introduced in 2.x

- The original `Squire\Models\Counties\GbCounty` model has now been moved to `Squire\Models\GbCounty`.

- The [`$map` property](https://github.com/squirephp/legacy#column-customisation) has been deprecated to improve performance of the package with large datasets. Please set up [Eloquent accessors](https://laravel.com/docs/master/eloquent-mutators#defining-an-accessor) if you require a similar feature.

## Need Help?

🐞 If you spot a bug with Squire, please [submit a detailed issue](https://github.com/squirephp/squire/issues/new), and wait for assistance.

🤔 If you have a question or feature request, please [start a new discussion](https://github.com/squirephp/squire/discussions/new).

🔐 If you discover a vulnerability within Squire, please review our [security policy](https://github.com/squirephp/squire/blob/main/SECURITY.md).