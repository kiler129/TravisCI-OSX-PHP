# Travis CI - PHP on OSX

Some time ago [Travis CI introduced](https://blog.travis-ci.com/2014-05-13-multi-os-feature-available/) support for multiple operating systems adding OS X. Unfortunately, [according to the documentation](https://docs.travis-ci.com/user/osx-ci-environment/) PHP is not an supported language on OS X at this time.
Since I wanted to test my project on both Linux and OS X I spent 2 days doing gazillion of different OS X builds and tests on my local machine to build robust & easy to use dual-os configuration.

## Requirements
This configuration is not specific to any testing framework or code coverage service, however examples assumes [PHPUnit](https://phpunit.de) and [Coveralls](https://coveralls.io).

## What's included?
This repo contains example configuration, which may be treated as base for new project which you want to test on both operating systems.
Repository contains `.travis.yml` file for build configuration & few helper scripts.

##### Included scripts
 * `build/prepare_osx_env.sh` - upgrades package manager & adds PHP-specific repositories
 * `build/handle_brew_pkg.sh` - installs or upgrades given package and than links it
 * `build/custom_php_ini.sh` - adds custom `php.ini`. To use this [set environment variable](https://docs.travis-ci.com/user/environment-variables/#Defining-Variables-in-Repository-Settings) named `ADDITIONAL_PHP_INI` pointing to correct file (e.g. `build/.travis.php.ini`)

## Build process
Build process, in this case, uses so-called "matrix" defined under `matrix -> include` key in `.travis.yml`.
Example configuration file performs following builds:
 * PHP 5.6 on Linux
 * PHP 7.0 on Linux
 * PHP [nightly](https://docs.travis-ci.com/user/languages/php#PHP-nightly-builds) on Linux
 * HHVM on Linux (which is allowed to fail)
 * PHP 5.6 on OS X 10.11
 * PHP 7.0 on OS X 10.11
 * PHP 5.6 on OS X 10.10
 * PHP 7.0 on OS X 10.10
 * PHP 5.6 on OS X 10.9
 * PHP 7.0 on OS X 10.9
