# Laravel Loocalization With Php File

## Create a New Laravel 8 Application
`composer create-project laravel/laravel laravel-language-php`

After successfully create a project We Will create some folders inside the resources / lang folder.
The Folder Name For Spanish And French Language

resources -> lang -> es
resources -> lang -> fr

## Create php File In The en, bn and fr folder Named message.php

resources -> lang -> en -> message.php
resources -> lang -> es -> message.php
resources -> lang -> fr -> message.php
## Add This Code In All message.php File 

<b>For en -> message.php</b>
```
<?php
return [
    'title'    => 'Account',    
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
