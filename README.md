## Registry Manager

Laravel 4 Registry Manager for storing application specific settings. A mashup of https://github.com/theelphie/registry and https://github.com/torann/laravel-4-registry. A big thanks to @Torann and @theelphie. 

## Installation

Add the following into your `composer.json` file:

```json
{
	"require": {
		"twosuperior\registry": "1.0.x"
	}
}
```

Add the service provider and alias into your `app/config/app.php`

```php
'providers' => array(
	'Twosuperior\Registry\RegistryServiceProvider',
),

'Registry' => 'Twosuperior\Registry\Facades\Registry',
```

Run `php artisan config:publish "twosuperior\registry"`

Run `php artisan migrate --package="twosuperior\registry"` to install the registry table

## Usage

Retrieve item from registry
```php
Registry::get('foo'); \\will return null if key does not exists
Registry::get('foo.bar'); \\will return null if key does not exists

Registry::get('foo', 'undefine') \\will return undefine if key does not exists
```

Store item into registry
```php
Registry::set('foo', 'bar');
Registry::set('foo', array('bar' => 'foobar'));

Registry::get('foo'); \\bar
Registry::get('foo.bar'); \\foobar
```

Remove item from registry
```php
Registry::forget('foo');
Registry::forget('foo.bar');
```

Flush registry table
```php
Registry::flush();
```

Dump all values from an item
```php
Registry::dump('foo');
```

Mass update

```php
$settings = Input::only('site_name', 'company_address', 'email');

Registry::store($settings);
```