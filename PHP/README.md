# PHP

> PHP powers ~75% of the web. Modern PHP (8+) is fast, typed, and pleasant.

---

## Purpose

Build web apps with PHP, primarily with Laravel or Symfony.

## Prerequisites

- Programming basics.

## Learning Outcome

You can build, deploy, and maintain a modern PHP app.

## Dependencies

- PHP 8.2+.

## Related Files

- [Laravel/](../Laravel/) · [Backend/](../Backend/) · [Databases/](../Databases/)

## AI Instructions

When using PHP:
1. Use PHP 8.2+.
2. Use Composer for packages.
3. Use Laravel (default) or Symfony.
4. Use PHPStan / Psalm for static analysis.
5. Use Larastan / Pint for Laravel.
6. PHP-FPM + Nginx, or FrankenPHP, or Swoole/RoadRunner.

## Human Notes

### Modern PHP
- Named args.
- Match expressions.
- Readonly properties.
- Enums.
- Fibers (async-ish).
- Property hooks (8.4).
- JIT compiler.

### Frameworks
- **Laravel** — most popular. Eloquent, queues, etc.
- **Symfony** — enterprise. Component-based.
- **CodeIgniter** — lightweight.
- **Slim** — micro.

### Tooling
- **Composer** — package manager.
- **PHPStan / Psalm** — static analysis.
- **PHP CS Fixer / Pint** — formatter.
- **PHPUnit / Pest** — testing.
- **Xdebug** — debugger.

### Install
- macOS: Herd, Homebrew, or XAMPP.
- Linux: package manager.
- Windows: XAMPP, Laragon, or WSL.

### Types
```php
function add(int $a, int $b): int {
    return $a + $b;
}

class User {
    public function __construct(
        public readonly string $name,
        public readonly int $age,
    ) {}
}
```

### Composer
```bash
composer require laravel/framework
composer install
composer update
```

### Performance
- OPcache (built-in).
- Preloading (PHP 7.4+).
- JIT (PHP 8+).
- Swoole / RoadRunner / FrankenPHP for app servers.

## Common Mistakes

- ❌ Using PHP 5 patterns.
- ❌ No types.
- ❌ `echo` from business logic.
- ❌ No Composer.
- ❌ Mixing logic and presentation.

## Tools

- Composer: https://getcomposer.org/
- PHPStan: https://phpstan.org/
- Pest: https://pestphp.com/

## References

- PHP docs: https://www.php.net/manual/
- PHP The Right Way: https://phptherightway.com/

## Further Reading

- *PHP 8 in Action* — Derek Stobbe et al.
- Laracasts: https://laracasts.com/

## Exercises

1. Build a Laravel CRUD app.
2. Add PHPStan level 8.
3. Deploy with FrankenPHP.

## Projects

- Build a SaaS with Laravel + Stripe + MySQL.

---

**Previous:** [FastAPI/](../FastAPI/) · **Next:** [Laravel/](../Laravel/) · **Related:** [Backend/](../Backend/)
