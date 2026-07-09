# Laravel

> The PHP framework for web artisans. Eloquent, queues, Horizon, Spark, the works.

---

## Purpose

Build full-stack apps with Laravel: ORM, auth, queues, broadcasting, testing.

## Prerequisites

- [PHP/](../PHP/).

## Learning Outcome

You can build, deploy, and scale a Laravel app.

## Dependencies

- PHP 8.2+, Composer.

## Related Files

- [PHP/](../PHP/) · [Backend/](../Backend/) · [MySQL/](../MySQL/) · [PostgreSQL/](../PostgreSQL/)

## AI Instructions

When using Laravel:
1. Use Laravel 11+.
2. Use Eloquent (ORM).
3. Use built-in auth (Breeze / Jetstream / Sanctum).
4. Use queues (Redis + Horizon).
5. Use scheduled jobs (Scheduler).
6. Use `php artisan` for everything.
7. Use Pest for tests.

## Human Notes

### Install
```bash
composer create-project laravel/laravel myapp
cd myapp
php artisan serve
```

### Structure
```
app/
  Models/
  Http/Controllers/
  Services/
database/
  migrations/
  seeders/
routes/
  web.php
  api.php
resources/
  views/
config/
```

### Models (Eloquent)
```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\HasMany;

class User extends Model {
    protected $fillable = ['name', 'email'];

    public function posts(): HasMany {
        return $this->hasMany(Post::class);
    }
}

// Query
$users = User::where('active', true)->orderBy('name')->get();
$user = User::find(1);
$user->posts; // relation loaded
```

### Migrations
```php
// create_users_table.php
Schema::create('users', function (Blueprint $table) {
    $table->id();
    $table->string('name');
    $table->string('email')->unique();
    $table->timestamps();
});
```
```bash
php artisan migrate
php artisan migrate:rollback
php artisan make:migration add_age_to_users
```

### Controllers
```php
class UserController extends Controller {
    public function index() {
        return User::with('posts')->paginate(20);
    }

    public function store(Request $request) {
        $data = $request->validate([
            'name' => 'required|string|max:100',
            'email' => 'required|email|unique:users',
        ]);
        return User::create($data);
    }
}
```

### Routes
```php
// routes/api.php
Route::get('/users', [UserController::class, 'index']);
Route::post('/users', [UserController::class, 'store']);
Route::get('/users/{user}', [UserController::class, 'show']);

// Resource routes
Route::apiResource('posts', PostController::class);
```

### Auth
- **Breeze** — simple starter.
- **Jetstream** — teams, 2FA.
- **Sanctum** — API tokens.
- **Fortify** — headless auth.

### Queues
```php
ProcessPodcast::dispatch($podcast);
```
```bash
php artisan queue:work
php artisan horizon  # with Horizon package
```

### Scheduling
```php
// app/Console/Kernel.php
protected function schedule(Schedule $schedule) {
    $schedule->command('emails:send')->dailyAt('08:00');
}
```
```bash
php artisan schedule:run
```

### Events / Broadcasting
```php
event(new UserRegistered($user));
broadcast(new MessageSent($message))->toOthers();
```

### Testing (Pest)
```php
test('user can register', function () {
    $response = $this->post('/register', [
        'name' => 'Alice',
        'email' => 'a@b.com',
        'password' => 'password',
    ]);
    $response->assertRedirect('/dashboard');
});
```

### Blade templates
```blade
@extends('layouts.app')
@section('content')
  <h1>{{ $title }}</h1>
  @foreach ($posts as $post)
    <p>{{ $post->title }}</p>
  @endforeach
@endsection
```

### Or: Inertia + Vue/React
Laravel + Inertia = SPA-like with backend routing.

### Performance
- OPcache + JIT.
- Redis for cache/queue/sessions.
- Horizon for queue monitoring.
- Telescope for debugging.
- Octane (Swoole/RoadRunner) for app server.

## Common Mistakes

- ❌ N+1 queries (use `with()` for eager loading).
- ❌ Fat controllers.
- ❌ Business logic in routes.
- ❌ Not using queues for slow work.
- ❌ Not using env vars for config.

## Tools

- Laravel docs: https://laravel.com/docs
- Laravel News: https://laravel-news.com/
- Laracasts: https://laracasts.com/
- Nova (admin): https://nova.laravel.com/
- Horizon (queues): https://laravel.com/docs/horizon
- Telescope (debug): https://laravel.com/docs/telescope

## Further Reading

- *Laravel: Up and Running* — Matt Stauffer
- *Laravel Beyond CRUD* — Brent Roose

## Exercises

1. Build a CRUD app with auth.
2. Add queues for email.
3. Add tests with Pest.

## Projects

- Build a SaaS with Laravel + Stripe + Vue (Inertia) + MySQL.

---

**Previous:** [PHP/](../PHP/) · **Next:** [Ruby/](../Ruby/) · **Related:** [Backend/](../Backend/)
