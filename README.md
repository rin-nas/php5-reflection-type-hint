# A PHP class for validating method parameters to allowed types via reflection

## Purpose

1. Used as a more convenient mechanism than a big code for checking types, standing after the declaration of the methods.
1. Requires write correct phpDoc

## Features

1. Very easy to use
1. Ability to turn off on the production server

## Understanding

All built-in PHP functions check the type of input variables and the "swearing", if not given.
ReflectionTypeHint does too.

Previously, I wrote this (the correct way, but a lot of code):

    if (! is_bool($b)) {
        trigger_error('A bool type expected in 1-st parameter, ' . gettype($b)   . ' type given!', E_USER_WARNING);
        return false;
    }
    if (! is_string($s)) {
        trigger_error('A string type expected in 2-nd parameter, ' . gettype($s)   . ' type given!', E_USER_WARNING);
        return false;
    }
Now I'm doing this one line of code:

    if (! ReflectionTypeHint::isValid()) return false;

**WARNING**

On a production server, it is important to disable assert, that would save server resources.
For this, use the `assert_options(ASSERT_ACTIVE, false)` or INI setting `"assert.active 0"`.
In this case `ReflectionTypeHint::isValid()` always immediately returns TRUE!

Project was exported from http://code.google.com/p/php5-reflection-type-hint
