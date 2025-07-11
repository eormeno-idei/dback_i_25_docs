# Tutorial: Proyecto Base para Microservicios con Laravel 12 (sin frontend)

**Docente:** Emilio Gustavo Ormeño  
**Nivel:** Principiante  
**Requisitos previos:** PHP, Composer, terminal  
**Tecnologías:** Laravel 12, Jetstream API, SQLite, Pest, Spatie Permission

---

## Objetivos de Aprendizaje

- Crear un proyecto Laravel optimizado para microservicios sin frontend  
- Implementar autenticación segura mediante bearer token  
- Configurar autorización basada en roles con Spatie Permission  
- Desarrollar y probar APIs REST con Pest

---

## 1. Instalación del Proyecto

### 1.1. Requisitos previos

- PHP ≥ 8.2  
- Composer  
- Laravel Installer:  
  ```bash
  composer global require laravel/installer
  ```  
- SQLite (incluido con PHP)  
- Cuenta en [mailtrap.io](https://mailtrap.io)

### 1.2. Crear el proyecto base

```bash
laravel new microservicios-api \
  --jet \
  --api \
  --verification \
  --pest
```

**Idem para Windows**

Este comando genera:

- Proyecto **sin vistas**
- Jetstream API para autenticación
- Verificación por email
- Pruebas preconfiguradas con Pest

---

## 2. Configuración Inicial

### 2.1. Archivo `.env`

```dotenv
APP_NAME="Microservicios API"
DB_CONNECTION=sqlite

MAIL_MAILER=smtp
MAIL_HOST=sandbox.smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=tu_usuario
MAIL_PASSWORD=tu_contraseña
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS=api@example.com
MAIL_FROM_NAME="${APP_NAME}"

ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD=secret123
```

> **Nota:** `MAIL_USERNAME` y `MAIL_PASSWORD` se obtienen de Mailtrap.

### 2.2. Migraciones y base SQLite

```bash
php artisan migrate
```

Si el archivo de base no existe, Laravel preguntará si desea crearlo.

---

## 3. Autenticación con Jetstream API

Jetstream API:

- Usa Laravel Sanctum
- Agrega verificación de email
- Usa `auth:sanctum` como middleware
- Provee endpoints `/register`, `/login`, `/user`, etc.

---

## 4. Autorización con Spatie Permission

### 4.1. Instalar la librería

```bash
composer require spatie/laravel-permission
```

### 4.2. Publicar y migrar

```bash
php artisan vendor:publish --provider="Spatie\\Permission\\PermissionServiceProvider"
php artisan migrate
```

---

## 5. Seeder de Usuario Administrador

### 5.1. Editar `DatabaseSeeder.php`

```php
use App\Models\User;
use Spatie\Permission\Models\Role;

public function run(): void
{
    Role::firstOrCreate(['name' => 'admin']);
    Role::firstOrCreate(['name' => 'user']);

    $admin = User::firstOrCreate(
        ['email' => env('ADMIN_EMAIL')],
        ['name' => 'Administrador', 'password' => bcrypt(env('ADMIN_PASSWORD'))]
    );

    $admin->assignRole('admin');
}
```

### 5.2. Ejecutar

```bash
php artisan db:seed
```

---

## 6. Estructura del Proyecto

| Característica             | Laravel Tradicional | Laravel Jetstream API-only |
|---------------------------|---------------------|-----------------------------|
| Vistas Blade              | Sí                  | No                          |
| Frontend (Inertia/Vue)    | Opcional            | No                          |
| Middleware web            | Sí                  | Parcial                     |
| Autenticación por tokens  | No (por defecto)    | Sí                          |
| Microservicios            | No                  | Sí                          |

---

## 7. Pruebas con Pest

### 7.1. Prueba de Registro y Login

Archivo: `tests/Feature/AuthTest.php`

```php
use Illuminate\Support\Facades\Hash;
use App\Models\User;

it('permite registrar y loguear un usuario', function () {
    $response = $this->postJson('/register', [
        'name' => 'Juan Pérez',
        'email' => 'juan@example.com',
        'password' => 'secret123',
        'password_confirmation' => 'secret123',
    ]);

    $response->assertStatus(201);
    echo "\nRegistro OK";

    $response = $this->postJson('/login', [
        'email' => 'juan@example.com',
        'password' => 'secret123',
    ]);

    $response->assertStatus(200);
    expect($response->json())->toHaveKey('token');
    echo "\nLogin OK con token: " . $response->json('token');
});
```

```bash
php artisan test
```

---

## 8. Microservicio de Ejemplo: Proyectos

### 8.1. Crear modelo y migración

```bash
php artisan make:model Proyecto -m
```

Migración:

```php
Schema::create('proyectos', function (Blueprint $table) {
    $table->id();
    $table->string('nombre');
    $table->timestamps();
});
```

```bash
php artisan migrate
```

### 8.2. Controlador

```bash
php artisan make:controller ProyectoController
```

`ProyectoController.php`:

```php
use App\Models\Proyecto;
use Illuminate\Http\Request;

class ProyectoController extends Controller
{
    public function index(Request $request)
    {
        $this->authorize('admin-only');
        return Proyecto::all();
    }
}
```

### 8.3. Definir política en `AuthServiceProvider`

```php
use Illuminate\Support\Facades\Gate;

Gate::define('admin-only', fn ($user) => $user->hasRole('admin'));
```

### 8.4. Rutas

`routes/api.php`:

```php
Route::middleware(['auth:sanctum', 'verified'])->group(function () {
    Route::get('/proyectos', [ProyectoController::class, 'index']);
});
```

---

## 9. Pruebas con Pest: Autorización

Archivo: `tests/Feature/ProyectoTest.php`

```php
use App\Models\User;
use Spatie\Permission\Models\Role;

it('admin puede acceder a /proyectos', function () {
    $admin = User::factory()->create([
        'email_verified_at' => now()
    ]);
    Role::firstOrCreate(['name' => 'admin']);
    $admin->assignRole('admin');

    $token = $admin->createToken('test')->plainTextToken;

    $response = $this->withToken($token)->getJson('/api/proyectos');
    $response->assertStatus(200);

    echo "\nRespuesta proyectos:\n";
    print_r($response->json());
});

it('usuario sin rol no accede a /proyectos', function () {
    $user = User::factory()->create([
        'email_verified_at' => now()
    ]);
    $token = $user->createToken('test')->plainTextToken;

    $response = $this->withToken($token)->getJson('/api/proyectos');
    $response->assertStatus(403);
});
```

---

## 10. Documentación Manual de la API

```markdown
### GET /api/proyectos

**Autenticación requerida:** Sí (Bearer Token)  
**Roles permitidos:** admin  
**Respuesta esperada:**

[
  {
    "id": 1,
    "nombre": "API de ejemplo",
    "created_at": "...",
    "updated_at": "..."
  }
]
```

---

## 11. Problemas Comunes

| Problema                                       | Solución                                                                 |
|-----------------------------------------------|--------------------------------------------------------------------------|
| Error `email not verified`                    | Asegurarse de que `email_verified_at` esté seteado en el usuario         |
| Seeder no crea usuario admin                  | Verificar que `ADMIN_EMAIL` y `ADMIN_PASSWORD` estén definidos en `.env` |
| Mail no enviado                               | Confirmar credenciales de Mailtrap                                       |
| Token no válido en pruebas                    | Usar `createToken('nombre')->plainTextToken`                             |

---

## Conclusión

Este proyecto sirve como base limpia para desarrollar microservicios REST con Laravel 12. Incluye autenticación con tokens, autorización por roles, pruebas automatizadas y documentación mínima. Es ideal para cursos, talleres y proyectos iniciales sin frontend.

---
