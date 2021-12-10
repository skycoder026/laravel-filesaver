# Description [![Build Status](https://secure.travis-ci.org/jeresig/jquery.hotkeys.png)](http://travis-ci.org/jeresig/jquery.hotkeys)

**Laravel Filesaver** is a media saver package, that can help you to stored any kind of media file. And it is very easy to use and install.

This is a small package to easy and simplify your code.

**Speciality** it will automatically save file/image name with actual path into your database


## Installation Process

```bash
composer require skycoder/laravel-filesaver
```


## Uses
Open your controller from where you want to store your media file and use this piece of line code into the method.

```php
  $fileSaver = new Filesaver();

  $fileSaver->upload_file($request->form_variable, $modelName, 'database_fieldname', 'base-path');
```

or 

```php
  (new Filesaver())->upload_file($request->file_variable, $modelName, 'database_fieldname', 'base-path');
```

In both case you shoud import class `use Skycoder\LaravelFilesaver\Filesaver;` top of the class


## Example Code
```php
<?php
namespace App\Http\Controllers\Setup;

use App\Models\User;
use Illuminate\Http\Request;
use App\Http\Controllers\Controller;
use Skycoder\LaravelFilesaver\Filesaver;

class UserController extends Controller
{
    /*
     |--------------------------------------------------------------------------
     | STORE METHOD
     |--------------------------------------------------------------------------
    */
    public function store(Request $request)
    {
        $user = User::create([
            'name'  => $request->name,
            'email' => $request->email
        ]);

        (new Filesaver())->upload_file($request->image, $user, 'profile-pic', 'user-profile-pic');
        return $user->refresh();
    }
}
```


## Configuration for Google Drive
Follow the link to get <a href="https://github.com/ivanvermeyen/laravel-google-drive-demo#create-your-google-drive-api-keys">Google Drive Credential</a> if you don't have
After that you should install a google drive package, 

`composer require nao-pon/flysystem-google-drive`

If need add `App\Providers\GoogleDriveServiceProvider::class,` to providers array into `config/app.php` 
 
 And then add this array into `config/filesystems.php`
 ```php
    'google' => [
        'driver' => 'google',
        'clientId' => env('GOOGLE_CLIENT_ID'),
        'clientSecret' => env('GOOGLE_CLIENT_SECRET'),
        'refreshToken' => env('GOOGLE_REFRESH_TOKEN'),
        'folderId' => env('GOOGLE_DRIVE_FOLDER_ID'),
    ],
  ```
  
  And finally add your google drive credential into `.env` file
  
  ```env
FILESYSTEM_CLOUD=google
GOOGLE_CLIENT_ID="YOUR_GOOGLE_CLIENT_ID"
GOOGLE_CLIENT_SECRET=YOUR_GOOGLE_CLIENT_SECRET"
GOOGLE_REFRESH_TOKEN="YOUR_GOOGLE_REFRESH_TOKEN"
GOOGLE_DRIVE_FOLDER_ID="YOUR_GOOGLE_DRIVE_FOLDER_ID"
  ```

After finish your setup you should add one line of code into your controller

```php 
(new Filesaver())->uploadFileToGoogleDrive($request->form_file_name, $modelName, 'database_file_name');
```

## More Packages

- <a href="https://github.com/skycoder026/user-log" target="_blank">User Log</a>


