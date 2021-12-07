# Laravel Loocalization With Php File

## Create a New Laravel 8 Application
```
composer create-project laravel/laravel laravel-language-php
```

After successfully create a project We Will create some folders inside the resources / lang folder.
The Folder Name For Spanish And French Language

resources -> lang -> es\
resources -> lang -> fr

## Create php File In The en, es and fr folder Named message.php

resources -> lang -> en -> message.php\
resources -> lang -> es -> message.php\
resources -> lang -> fr -> message.php
## Add This Code In All message.php File 

<b>For en -> message.php</b>
```
<?php
return [
    'title'     => 'Account',    
     'name'     => 'Name',    
     'email'    => 'E-mail',    
     'password' => 'Password',
];
```
<b>For es -> message.php</b>
```
<?php
return [
    'title'    => 'Cuenta',
    'name'     => 'Nombre',
    'email'    => 'Correo electrónico',
    'password' => 'Contraseña',
];
```

<b>For fr -> message.php</b>
```
<?php
return [
    'title'    => 'Paramètre de compte',
    'name'     => 'nom',
    'email'    => 'Courriel',
    'password' => 'passe',
];
```


## Setup The Blade View In <b>welcome.blade.php</b>
```
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">

  </head>
  <body>
  
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">Navbar</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        @php $locale = session()->get('locale'); @endphp
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false"> Language <span class="caret"></span>
          </a>
          @switch($locale)
              @case('fr')
              <img src="{{asset('flag/fr.png')}}" 
                    width="30px" height="20x"> French
              @break
              @case('es')
              <img src="{{asset('flag/es.png')}}" 
                    width="30px" height="20x"> Spain
              @break
              @default
              <img src="{{asset('flag/en.png')}}" 
                    width="30px" height="20x"> English
          @endswitch
          <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
            <li><a class="dropdown-item" href="lang/en"><img src="{{asset('flag/en.png')}}" width="25px">English</a></li>
            <li><a class="dropdown-item" href="lang/fr"><img src="{{asset('flag/fr.png')}}" width="25px"> Français</a></li>
            <li><a class="dropdown-item" href="lang/es"><img src="{{asset('flag/es.png')}}" width="25px"> Espane</a></li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</nav>
<div class="container">
    <div class="row justify-content-center">
        <div class="col-md-8">
            <div class="card">
                <div class="card-body">
                <p>{{ __("message.title") }}</p>
                <p>{{ __("message.name") }}</p>
                <p>{{ __("message.email") }}</p>
                <p>{{ __("message.password") }}</p>
                  or  @lang('message.title')
                </div>
            </div>
        </div>
    </div>
</div>

    <!-- Optional JavaScript; choose one of the two! -->

    <!-- Option 1: Bootstrap Bundle with Popper -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>

  </body>
</html>
```
## Add Flag
Create a folder name flag in public and add 3 country image for 
```
en.png
es.png
fr.png
```

## Set up route, controller, and middleware
Create Controller

```
php artisan make:controller LanguageController 
```

Add Route in <b>web.php</b>
```
use App\Http\Controllers\LanguageController;
Route::get('lang/{locale}',[LanguageController::class, 'index']);
```
Add Function in <b>LanguageController</b>
```
use Illuminate\Http\Request;
use Illuminate\Support\Facades\App;

public function index(Request $request,  $locale)
    {
        App::setLocale($locale);
        $request->session()->put('locale', $locale);
        return redirect()->back();
    }
```
Create Middleware And Add This Method
```
php artisan make:middleware LanguageMiddleware
```
Add This Code in <b>LanguageMiddleware</b>

```
use Illuminate\Support\Facades\App;
public function handle(Request $request, Closure $next)
    {
        if (session()->has('locale')) {
            App::setLocale(session()->get('locale'));
        }
        return $next($request);
    }
```

## Register The Middleware in <b>kernel.php</b>
```
protected $middlewareGroups = [
        'web' => [
            \App\Http\Middleware\LanguageMiddleware::class,
        ],
```

## Run Application
Run This Application
```
php artisan serve
```

