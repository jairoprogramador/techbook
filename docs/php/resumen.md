# Introducción a PHP y Slim

Si ya vienes de Java y Spring, una forma sencilla de entender PHP y Slim es pensar en **PHP como el lenguaje** y **Slim como un microframework equivalente a Spring Boot pero mucho más ligero**.

# 1. ¿Qué es PHP?

PHP es un lenguaje interpretado orientado principalmente al desarrollo web.

Un archivo PHP puede generar HTML, responder APIs REST, conectarse a bases de datos, procesar formularios, etc.

```php
<?php

echo "Hola Mundo";
```

Ejecutar:

```bash
php index.php
```

Salida:

```text
Hola Mundo
```

# 2. Variables

En PHP todas las variables comienzan con `$`.

```php
<?php

$nombre = "Jairo";
$edad = 34;

echo $nombre;
```

# 3. Arrays

PHP tiene arrays asociativos (similares a un Map en Java).

```php
<?php

$persona = [
    "nombre" => "Jairo",
    "edad" => 34
];

echo $persona["nombre"];
```

Resultado:

```text
Jairo
```

# 4. Funciones

```php
<?php

function saludar($nombre) {
    return "Hola " . $nombre;
}

echo saludar("Jairo");
```

# 5. Clases

```php
<?php

class Persona {

    private string $nombre;

    public function __construct(string $nombre) {
        $this->nombre = $nombre;
    }

    public function saludar(): string {
        return "Hola " . $this->nombre;
    }
}

$persona = new Persona("Jairo");

echo $persona->saludar();
```

Observa que:

```php
$this->nombre
```

es equivalente a:

```java
this.nombre
```

# 6. Composer (el Maven de PHP)

Composer es el gestor de dependencias más usado en PHP.

Instalar una librería:

```bash
composer require slim/slim
```

# 7. ¿Qué es Slim?

Slim Framework es un microframework para construir APIs REST y aplicaciones web.

# 8. Crear un proyecto Slim

```bash
composer create-project slim/slim-skeleton mi-api
cd mi-api
composer start
```

# 9. Primera ruta

```php
$app->get('/hola', function ($request, $response) {

    $response->getBody()->write("Hola Mundo");

    return $response;
});
```

# 10. Endpoint REST JSON

```php
$app->get('/usuario', function ($request, $response) {

    $data = [
        'id' => 1,
        'nombre' => 'Jairo'
    ];

    $response->getBody()->write(
        json_encode($data)
    );

    return $response
        ->withHeader('Content-Type', 'application/json');
});
```

# 11. Parámetros de ruta

```php
$app->get('/usuarios/{id}', function ($request, $response, $args) {

    $id = $args['id'];

    $response->getBody()->write("Usuario: $id");

    return $response;
});
```

# 12. Recibir JSON

```php
$app->post('/usuarios', function ($request, $response) {

    $body = $request->getParsedBody();

    $nombre = $body['nombre'];

    return $response;
});
```

# 13. Middleware

```php
$app->add(function ($request, $handler) {

    error_log("Petición recibida");

    return $handler->handle($request);
});
```

# 14. Conexión a Base de Datos

```php
$pdo = new PDO(
    "mysql:host=localhost;dbname=test",
    "root",
    "password"
);
```

Consulta:

```php
$stmt = $pdo->prepare(
    "SELECT * FROM usuarios WHERE id = ?"
);

$stmt->execute([1]);

$resultado = $stmt->fetch();
```

# 15. Arquitectura recomendada

```text
src/
├── Controllers
├── Services
├── Repositories
├── Domain
├── Infrastructure
└── Routes
```

Flujo:

```text
Controller
    ↓
Service
    ↓
Repository
    ↓
MySQL
```

# Equivalencias Java/Spring ↔ PHP/Slim

| Java/Spring | PHP/Slim |
|------------|----------|
| Spring Boot | Slim |
| Maven | Composer |
| Controller | Route Handler / Controller |
| Service | Service |
| Repository | Repository |
| JPA/Hibernate | Doctrine ORM o PDO |
| Filter | Middleware |
| @GetMapping | $app->get() |
| @PostMapping | $app->post() |
| application.yml | .env |

Para alguien con experiencia en Java, lo más importante es entender que Slim no impone una arquitectura fuerte como Spring. Tú decides cómo organizar controladores, servicios, repositorios y dependencias.
