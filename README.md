Twig Gettext Extractor
======================

This Twig Gettext Extractor is a fork with some love put in; things I needed to develop an alternative to Poedit that
on OS X is a major pain with all of the temp folder issues.

This tool, gives you what you need to extract *.po files from your Twig files, and additionally:

* supports text domains
* supports command-line stubs for functions
* supports command-line stubs for filters

## Installation

Install this through composer [composer](http://getcomposer.org).

```json
{
    "require": {
        "saeven/circlical-twig-extractor": "*"
    }
}
```
## Web-Based Editing for Zend Framework 2

You can skip this setup though, and use my web-based editor for ZF2.
[Click here for more info](https://packagist.org/packages/saeven/zf2-poeditor)

When the time comes, I'll PSR-7 it to make it framework-agnostic.

## PoEdit Setup

By default, Poedit does not have the ability to parse Twig templates.
This can be resolved by adding an additional parser (Edit > Preferences > Parsers)
with the following options:

- Language: `Twig`
- List of extensions: `*.twig`
- Invocation:
    - Parser command: `<project>/vendor/bin/twig-gettext-extractor --sort-output --force-po -o %o %C %K -L PHP --files %F`
    - An item in keyword list: `-k%k`
    - An item in input file list: `%f`
    - Source code charset: `--from-code=%c`

<img src="http://i.imgur.com/f9px2.png" />

Now you can update your catalog and Poedit will synchronize it with your twig templates.

## Custom extensions

Twig-Gettext-Extractor registers some default twig extensions. However, if you are using custom extensions, you need to register them first before you can extract the data. In order to achieve that, copy the binfile into some custom place. A common practice would be: `cp vendor/bin/twig-gettext-extractor bin/twig-gettext-extractor`

Now you may add your custom extensions [here](https://github.com/umpirsky/Twig-Gettext-Extractor/blob/master/twig-gettext-extractor#L41):

```php
$twig->addFunction(new \Twig_SimpleFunction('myCustomExtension', true));
$twig->addFunction(new \Twig_SimpleFunction('myCustomExtension2', true));
```

## Tests

To run the test suite, you need [composer](http://getcomposer.org) and
[PHPUnit](https://github.com/sebastianbergmann/phpunit).

    $ composer install --dev
    $ phpunit

## License

Twig Gettext Extractor is licensed under the MIT license, like its parent fork.
