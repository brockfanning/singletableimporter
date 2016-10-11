# SingleTableImporter

This class is intended as a simple importer for moving source data into a single MySQL table. It provides a few automations, such as text alterations, and date alterations, which is why it might be better than simply importing the file with phpMyAdmin or something similar. It supports currently supports CSV files and single-worksheet Excel spreadsheets, and assumes that the first row of data corresponds exactly to the column names in the MySQL database.

## Dependencies

* PHP 5.3.2 or higher
* MySQL 5.5 or higher

## Dev dependencies

* Composer

## Installation

Use composer to bring this into your PHP project. The composer.json should look like this:

```
{
    "require": {
        "usdoj/singletableimporter": "dev-master"
    },
    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/usdoj/singletableimporter.git"
        }
    ]
}
```

After creating a composer.json similar to the above, do a "composer install".

## Usage

To use the library you need to include the autoloader, and then instantiate the object referencing your configuration and source data file. The configuration must be an object of the \Noodlehaus\Config class. Then you simply call the run() method. For example:

```
require_once '/path/to/my/libraries/csvtomysql/vendor/autoload.php';
$config = new \Noodlehaus\Config('/path/to/my/configFile.yml');
$sourceFile = '/path/to/my/sourceFile.csv';
$importer = new \USDOJ\CsvToMysql\Importer($config, $sourceFile);
$importer->run();
```

## Configuration

The library depends on configuration in an \Noodlehaus\Config object. Here are examples (in YAML) of the settings that should exist in that config object:
```
# Database credentials: this is the only required section.
database name: myDatabase
database user: myUser
database password: myPassword
database host: localhost
database table: myTable

# If there are any special characters or phrases that need to be altered when
# importing the data from the CSV file, indicate those here. For example, to
# change all occurences of § with &#167; uncomment the lines below.
#text alterations:
#    "§": "&#167;"

# If the environment needs to use a proxy, uncomment and fill out this section.
# proxy: 192.168.1.1:8080

# To prevent the use of the proxy for certain URLs, enter partial patterns here.
# proxy exceptions:
#    - .example.com

# To use a certain user agent for remote requests, uncomment and indicate here.
# user agent: Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2228.0 Safari/537.36
```
