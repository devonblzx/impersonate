# Laravel Impersonation

Impersonate as other users temporarily while maintaining your existing authentication.

This is an updated fork of bizhub/impersonate and has only been tested on Laravel 5.0

## How it works

Maintains two session variable `impersonate` of the user ID you are impersonating and `impersonator` of your actual user ID.  The middleware checks for the session variable and overwrites your existing authenticated user with the impersonated user ID.  For that execution, your application will see you as the impersonated user, however, your authenticated session remains in tact, so once the session variables are removed, you'll be, once again, recognized as your original user.

## Updates in this Fork

* Tracks impersonator, you can call Auth::user()->impersonator() to get the impersonator model.
* Allows compatibility with Auth::id() in Laravel 5.  In the parent package, Auth::id() != Auth::user()->id because of a session variable.

## Installation

1. Add CanImpersonate trait to User model.
2. Add CheckIfImpersonating to $middleware in app/Http/Kernel.php

## Usage

1. Retrieve a User model and call $user->impersonate() to set the session variables.
2. Reload the page or go to new pages to view them as the other user.
3. Call Auth::user()->stopImpersonating() to remove the session variables.