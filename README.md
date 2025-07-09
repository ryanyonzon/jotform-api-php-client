# JotForm API Client Library for PHP

## Description

A simple [JotForm API](http://api.jotform.com/docs/) library for PHP.

## Requirements

- [PHP >= 5.4](http://php.net/)
- [Guzzle 6](https://github.com/guzzle/guzzle)

## Installation

The recommended way to install jotform-api-php-client is through [Composer](https://getcomposer.org/).

    curl -sS https://getcomposer.org/installer | php

Next, run the Composer command to install jotform-api-php-client library:

    php composer.phar require ryanyonzon/jotform-api-php-client:dev-master

After installing, simply include the Composer's autoloader (inside your script):

    require 'vendor/autoload.php';

## Examples

A simple example to get user's information:

```php
<?php
require 'vendor/autoload.php';

$key = 'your-jotform-api-key-here';

$client = new JotForm\JotFormClient();
$client->setAPIKey($key);

$user = new JotForm\Resource\User($client);

try {
    $info = $user->getUser();
    print_r($info);
} catch (\JotForm\Exception\ClientException $e) {
    echo $e->getMessage() . "\n";
}
```

Here's another example for creating a form:

```php
<?php
require 'vendor/autoload.php';

$key = 'your-jotform-api-key-here';

$client = new JotForm\JotFormClient();
$client->setAPIKey($key);

$form = new JotForm\Resource\Form($client);

try {
    $myForm = [
        'questions' => [
            [
                'type' => 'control_head',
                'text' => 'Form Title',
                'order' => 1,
                'name' => 'Header'
            ],
            [
                'type' => 'control_textbox',
                'text' => 'Text Box Title',
                'order' => 2,
                'name' => 'TextBox',
                'validation' => 'None',
                'required' => 'No',
                'readonly' => 'No',
                'size' => 30,
                'labelAlign' => 'Auto',
                'hint' => 'Hint: Lorem Ipsum'
            ],
        ],
        'properties' => [
            'title' => 'My Form',
            'height' => 600
        ],
        'emails' => [
            'type' => 'notification',
            'name' => 'notification',
            'from' => 'default',
            'to' => 'noreply@mywebsite.com',
            'subject' => 'New Submission',
            'html' => 'false'
        ]
    ];
    $response = $form->createForm($myForm);
    print_r($response);
} catch (\JotForm\Exception\ClientException $e) {
    echo $e->getMessage() . "\n";
}
```

See [examples](https://github.com/ryanyonzon/jotform-api-php-client/tree/master/examples) folder for more sample scripts.

## License

Licensed under the [MIT license](http://www.opensource.org/licenses/mit-license.php)
