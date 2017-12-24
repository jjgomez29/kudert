# Case Bundle

Este es el bundle contenedor de los servicios para los Casos del proyecto commcenter.login

* [Instalación](#instalación)
    * [Agregar Repositorio](#agregar-repositorio)
    * [Requerir los Package](#requerir-los-package)
    * [Registramos el Bundle](#registramos-el-bundle)
    * [Incluimos los Routes del Bundle](#incluimos-los-routes-del-bundle)
    * [Establecemos la configuracion de seguridad del bundle](#establecemos-la-configuracion-de-seguridad-del-bundle)
    * [Creamos las tablas del Bundle (MySQL)](#creamos-las-tablas-del-bundle-(mysql))
    * [Importamos los datos](#importamos-los-datos)

## Instalación

Utilizaremos composer para dicha instalación:

### Agregar Repositorio
Es necesario indicarle a composer donde se encuentra el repositorio de nuestro bundle, esto lo hacemos agregando las siguientes lineas al **composer.json** del proyecto.
```json
...
    "repositories": [
        {
            "type": "vcs",
            "url":  "https://git.smarter.com.ve/jgomez/CaseBundle.git"
        }
    ],
...
```
### Requerir los Package

En un terminal, nos vamos a la carpeta base del proyecto y ejecutamos los siguientes comandos.

```bash
composer require  jgomez/taskbundle "dev-master"
```

### Registramos el Bundle

Con el editor de texto de su preferencia editamos el archivo **app/AppKernel.php**, y agregamos las siguientes lineas.

```php
    public function registerBundles()
    {
        $bundles = array(
            ...
            new CenposCommcenter\CaseBundle\CenposCommcenterCaseBundle(),
        );
        ...
    }
```

### Incluimos los Routes del Bundle

Con el editor de texto de su preferencia editamos el archivo **app/config/routing.yml**, y agregamos las siguientes lineas al final del archivo.

```yaml
cenpos_commcenter_case_cases:
    resource: "@CenposCommcenterCaseBundle/Controller/CaseController.php"
    type:   annotation
```


### Establecemos la configuracion de seguridad del bundle

en **app/config/security.yml** colocamos lo siguiente:

```yaml
security:
    encoders:
        CenposCommcenter\ModelBundle\Entity\UsersProvider:
            algorithm:   sha256
            iterations: 1
            encode_as_base64: false
    providers:
        api_provider:
            entity:
                class: CenposCommcenter\ModelBundle\Entity\UsersProvider
 
    firewalls:
        api_login:
            pattern:  ^/login/$
            anonymous: ~
        api_authenticate:
            pattern:  ^/auth/$
            guard:
                authenticators:
                    - app.jwt_authenticator
        api_theme:
            pattern: ^/theme/(?!token)
            guard:
                authenticators:
                    - app.jwt_authenticator
            
    access_control:
        - { path: ^/login, roles: IS_AUTHENTICATED_ANONYMOUSLY }
        - { path: ^/auth, roles: IS_AUTHENTICATED_FULLY }
        - { path: ^/themes, roles: [OPT_THEME_THEMES] }

```

### Creamos las tablas del Bundle (MySQL)

Ejecutamos desde la consola el comando

```bash
php bin/console doctrine:schema:update --force
```

### Importamos los datos

Este archivo contiene el dump de las tablas maestras de smartme, y debe ejecutarse una sola vez luego de la instalación.

```bash
mysql -h <hostname> -u <ussername> -p

use databasename;

source /direccion-de-la-carpeta-raiz/src/CenposCommcenter/CaseBundle/Resources/sql/casebundle.sql
```
