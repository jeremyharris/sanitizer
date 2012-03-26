# Sanitizer

Sanitizer is CakePHP plugin that makes it very easy to automatically sanitize
your data. For example, if you don't want HTML tags in some field and want clean
HTML tags in others, Sanitizer makes it easy to automatically get what you want.

## Usage

Simply add the behavior to your model:

    var $actsAs = array('Sanitizer.Sanitize');

Now just define your sanitization rules. These rules are formatted similar to
CakePHP's validation rules. The Sanitize behavior uses the built-in [Sanitize class][1].
To sanitize a field using a method on the Sanitize class, set the $sanitize var 
with the key as the field name and the value the method. Optionally pass an array 
with the options that you would normally pass to the Sanitize method you want to use.

    // clean the name field using Sanitize::html()
    var $sanitize = array(
        'name' => 'html'
    );

    // or clean the name field using Sanitize::paranoid() and allowing '%'
    var $sanitize = array(
        'name' => array(
            'paranoid => array('%')
        )
    );

Sanitization methods supported:
* clean
* html
* paranoid
* stripAll
* stripImages
* stropScripts
* stripWhitespace

## Advanced

By default, the Sanitize behavior cleans the data before validation. If you want
validate *then* sanitize, use:

    var $actsAs = array(
        'Sanitizer.Sanitize' => array(
            'validate' => 'before'
        )
    );

See the test cases for code samples.

## Notes

* If you upload files, the Sanitize behavior will by default sanitize and escape
  the file path. Make sure to set `'file' => false` in your `$sanitize` var!
* Auto-decoding was removed on the master branch. You can find it in the
  `decode` branch. It didn't work well in a real world application, with find('count')
  and the like generating errors.

## Future plans

* Add ability to customize default method
* Allow using methods outside of Cake's Sanitize class

## License

Licensed under The MIT License
[http://www.opensource.org/licenses/mit-license.php][2]
Redistributions of files must retain the above copyright notice.

[1]: http://api13.cakephp.org/class/sanitize
[2]: http://www.opensource.org/licenses/mit-license.php
