# Description [![Build Status](https://secure.travis-ci.org/jeresig/jquery.hotkeys.png)](http://travis-ci.org/jeresig/jquery.hotkeys)

**Laravel Filesaver** is a media saver package, that can help you to stored any kind of media file. And it is very easy to use and install.

This is a small package to easy and simplify your code.

**Speciality** it will automatically save file/image name with actual path into your database


## Installation Process

```
composer require skycoder/laravel-filesaver
```


## Uses
Open your controller from where you want to store your media file and use this piece of line code into the method.

```
  $fileSaver = new Filesaver();

  $fileSaver->upload_file($request->form_variable, $modelName, 'database_fieldname', 'base-path');
```

or 

```
  (new Filesaver())->upload_file($request->file_variable, $modelName, 'database_fieldname', 'base-path');
```

In both case you shoud import class `use Skycoder\LaravelFilesaver\Filesaver;` top of the class


## Example Code
```
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



## More Packages

- <a href="https://github.com/skycoder026/user-log" target="_blank">User Log</a>


