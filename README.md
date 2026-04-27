<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://github.com/laravel/framework/actions"><img src="https://github.com/laravel/framework/workflows/tests/badge.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

## CRUD CON LARAVEL
Este proyecto consiste en la creación de un CRUD básico utilizando Laravel, donde se gestionan productos con los campos: descripción, precio y stock.

## Creación del proyecto
```bash
laravel new crud_rapido
```
Modelo de migración
```bash
php artisan make:model Product -m
```
Estructurta de migración
```bash
$table->id();
$table->string('description');
$table->double('price', 8, 2);
$table->integer('stock');
$table->timestamps();
```
Migraciones
```bash
php artisan migrate
```
## Problemas encontrados
## Error: Key too long
Durante la ejecución de las migraciones, se presentó el error relacionado con la longitud de las claves en MySQL.
Se agregó la siguiente configuración en el archivo AppServiceProvider.php:
```bash
use Illuminate\Support\Facades\Schema;

public function boot(): void
{
    Schema::defaultStringLength(191);
}
```
Y luego ejecutamos:
```bash
php artisan migrate:fresh
```
## Error al insertar productos
Se presentó un error al intentar guardar un producto desde el formulario.
El error estaba en la validación de datos enviada al modelo (Product::create()).
<img width="1115" height="780" alt="image" src="https://github.com/user-attachments/assets/381e883c-9aa0-4e6f-a193-94054c7194d9" />
El problema ocurre en:
```bash
Product::create($request->validated());
```
Solución aplicada:

Se corrigieron las reglas de validación en el archivo:
```bash
app/Http/Requests/ProductRequest.php
```
Dentro de la función rules() para asegurar que los datos enviados coincidan con la estructura de la base de datos.
```bash
public function rules()
{
    return [
        'description' => 'required|string|max:255',
        'price' => 'required|numeric',
        'stock' => 'required|integer',
    ];
}
```
## Generador CRUD
Utilizamos comando como: 
```bash
Instalar generador: 
composer require ibex/crud-generator --dev

Generar CRUD:
php artisan make:crud products

Ejecutar proyecto
php artisan serve

Y accedemos a
http://127.0.0.1:8000/products
```

## Base de datos utilizada
Se utilizó phpMyAdmin para la gestión de base de datos:
```bash
http://localhost/phpmyadmin5.2.3/
```
Y se trabajo en entorno local con WAMP

## Security Vulnerabilities


