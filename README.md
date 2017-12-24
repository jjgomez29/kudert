# Test Kudert

Esta app ordena horarios para Certificación de Kudert tomando en consideracion el tiempo en minutos, se tomo como lenguaje de programacion para el modelo y logica javascript.

* [Instalación](#instalación)
    * [Agregar Repositorio](#agregar-repositorio)
    * [Requerir los Package](#requerir-los-package)
    * [Autor](#Autor)

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

### Autor

Ing. Jhonny Gomez

```Contacto
    Correo: jelvyc15@gmail.com
    Telefono:  096 8961840
```
