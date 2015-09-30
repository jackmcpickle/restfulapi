# Restful Api

Restful Api is a plugin for [Craft CMS](http://buildwithcraft.com) that exposes elements as resources via a restful api. While similar to Craft's own [Element Api](https://github.com/pixelandtonic/ElementAPI) plugin, Restful Api offers a few more features such as support for more HTTP verbs, authentication and element type based permissions.

Restful Api utilizes [Fractal] (http://fractal.thephpleague.com/) to transform and serialize responses. Restful Api is also [PSR-7] (http://www.php-fig.org/psr/psr-7/) complaint. Its request and response objects can even be utilized by third party plugins if desired, although this has not been extensively tested yet.

## Installation
[Download] (https://github.com/airtype/RestfulApi/archive/master.zip) the latest version of the zip file. Place the `RestfulApi` directory within the `plugins` directory. In the Craft control panel, install the plugin.

## Usage
The url structure for the api endpoints are as follows (with the `?` denoting optional uri components):

    http://example.com/{{apiRoutePrefix}}/{{elementType}}/{{?elementId}}/{{?action}}?{{?elementCriteriaModelParams}}

* `{{apiRoutePrefix}}` is configurable via the plugin config file.
* `{{elementType}}` can be any element type is enabled in the plugin config file. Any element type can be enabled or disabled. Custom element types will need to be added to the config file.
* `{{elementId}}` is the element's id. Hopefully support for uuid will be added down the road.
* `{{action}}` maps to a custom method on a controller. This allows you to do something custom action on a defined resource.
* `{{elementCriteriaModel}}` accepts any criteria that you would normally use to query Elements in Craft with.

Currently, Rest Api supports the following HTTP verbs:

* __GET__
* __POST__
* __PUT__
* __PATCH__
* __DELETE__

Example endpoints include:

* `GET  http://example.com/api/Entry?page=2&limit=10&order=postDate asc`__ returns the second page of a paginated listing of 10 Entry elements, ordered by the `postDate` attribute in ascending order
* `GET http://example.com/api/Entry/2` returns the entry with the element id of 2
* `POST http://example.com/api/Entry` creates a new Entry element
* `PUT http://example.com/api/Entry/2` updates the entry with the element id of 2
* `DELETE http://example.com/api/Entry/2` deletes the entry with the element id of 2


## Configuration
To override any values defined in the default configuration, create a `restfulApi.php` file in the config directory and place the keys to override in a returned array.

### devMode

```php
'devMode' => \Craft\craft()->config->get('devMode'),
```

If`devMode` is enabled, the stack trace for any exception that throws `RestfulApi\Exceptions\RestfulApiExpception` is output in an error response. If `devMode` is disabled, then the error is still displayed with a message, but without the stack trace. By default, `devMode` observes the setting of `devMode` defined in the `general.php` config.

### apiRoutePrefix

```php
'apiRoutePrefix' => 'api',
```

The Api Route Prefix acts as a namespace and is prepended to all routes that the API plugin defines. For example, the endpoint to

## Permissions

## Disclaimer
This plugin is still considered to be in early development. Use with caution. If you see something wrong, please create an issue or feel free to fork and make a pull request.