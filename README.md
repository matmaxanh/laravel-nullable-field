# Nullable database fields for the Laravel PHP Framework

Often times, database fields that are not assigned values are defaulted to `null`. This is particularly important when creating records with foreign key constraints.

Note, the database field must be configured to allow null.

More recent versions of MySQL will convert the value to an empty string if the field is not configured to allow null. Be aware that older versions may actually return an error.

Laravel (5.1) does not currently support automatically setting nullable database fields as `null` when the value assigned to a given attribute is empty.

# Installation

This trait is installed via [Composer](http://getcomposer.org/). To install, simply add it to your `composer.json` file:

```
{
	"require": {
		"bluecode/laravel-nullable-field": "~0.1"
	}
}
```

Then run composer to update your dependencies:

```
$ composer update
```

In order to use this trait, import it in your Eloquent model, then set the protected `$nullable` property as an array of fields you would like to be saved as `null` when empty.

```php
<?php

use Bluecode\Trait\NullableField;
use Illuminate\Database\Eloquent\Model;

class UserProfile extends Model
{
	use NullableField;
	
	protected $nullable = [
		'tel',
		'address'
	];
}
```

Now, any time you are saving a `UserProfile` profile instance, any empty attributes that are set in the `$nullable` property will be saved as `null`.

```php
<?php

$profile = new UserProfile::find(1);
$profile->tel = ' '; // Empty, saved as null
$profile->address  = '10 A Street';
$profile->save();
```

# Support

If you believe you have found an issue, please report it using the [GitHub issue tracker](https://github.com/matmaxanh/laravel-nullable-field/issues), or better yet, fork the repository and submit a pull request.

If you're using this package, I'd love to hear your thoughts. Thanks!