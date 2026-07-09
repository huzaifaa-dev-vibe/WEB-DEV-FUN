# NestJS

> Angular-inspired, batteries-included Node.js framework. TypeScript-first, enterprise-grade.

---

## Purpose

Build structured, maintainable, enterprise-grade Node apps with NestJS.

## Prerequisites

- [NodeJS/](../NodeJS/), [TypeScript/](../TypeScript/), [Express/](../Express/) (concepts).

## Learning Outcome

You can build a NestJS app with modules, controllers, providers, DI, and pipes.

## Dependencies

- Node.js.

## Related Files

- [Express/](../Express/) · [Fastify/](../Fastify/) · [NodeJS/](../NodeJS/) · [Architecture/](../Architecture/)

## AI Instructions

When using NestJS:
1. Use modules for organization.
2. Use DI (providers, services).
3. Use pipes for validation (ValidationPipe + class-validator / Zod).
4. Use guards for auth.
5. Use interceptors for logging, transform.
6. Use filters for error handling.

## Human Notes

### Structure
```
src/
  app.module.ts
  main.ts
  users/
    users.module.ts
    users.controller.ts
    users.service.ts
    dto/
      create-user.dto.ts
    entities/
      user.entity.ts
```

### Module
```ts
@Module({
  imports: [DatabaseModule],
  controllers: [UsersController],
  providers: [UsersService],
  exports: [UsersService],
})
export class UsersModule {}
```

### Controller
```ts
@Controller('users')
export class UsersController {
  constructor(private readonly users: UsersService) {}

  @Get()
  list() { return this.users.list(); }

  @Post()
  @UsePipes(new ValidationPipe())
  create(@Body() dto: CreateUserDto) { return this.users.create(dto); }

  @Get(':id')
  get(@Param('id') id: string) { return this.users.get(id); }
}
```

### Service (provider)
```ts
@Injectable()
export class UsersService {
  constructor(@InjectRepository(User) private repo: Repository<User>) {}
  list() { return this.repo.find(); }
  create(dto: CreateUserDto) { return this.repo.save(dto); }
}
```

### DTO + validation
```ts
import { IsString, IsEmail } from 'class-validator';

export class CreateUserDto {
  @IsString() name: string;
  @IsEmail() email: string;
}
```
Or use Zod via `nestjs-zod`.

### Guards (auth)
```ts
@Injectable()
export class AuthGuard implements CanActivate {
  canActivate(context: ExecutionContext): boolean {
    const req = context.switchToHttp().getRequest();
    return !!req.user;
  }
}

@UseGuards(AuthGuard)
@Controller('admin')
export class AdminController {}
```

### Pipes (validation/transform)
```ts
@Injectable()
export class ParseIntPipe implements PipeTransform {
  transform(value: string) {
    const n = parseInt(value, 10);
    if (isNaN(n)) throw new BadRequestException();
    return n;
  }
}
```

### Interceptors
Wrap handlers — logging, transform, cache.
```ts
@Injectable()
export class LoggingInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler) {
    console.log('Before...');
    return next.handle().pipe(tap(() => console.log('After...')));
  }
}
```

### Filters (error handling)
```ts
@Catch(HttpException)
export class HttpExceptionFilter implements ExceptionFilter {
  catch(exception: HttpException, host: ArgumentsHost) {
    const ctx = host.switchToHttp();
    const res = ctx.getResponse();
    res.status(exception.getStatus()).json({
      error: { code: 'HTTP_ERROR', message: exception.message },
    });
  }
}
```

### Dependency Injection
- Constructor injection (default).
- Property injection (rare).
- Tokens for non-class providers.

### Databases
- TypeORM (legacy, popular).
- Prisma (modern).
- Drizzle (modern, lightweight).
- Mongoose (MongoDB).

### Microservices
NestJS supports microservices (TCP, Redis, NATS, gRPC, Kafka).

### When to use NestJS
- Enterprise apps.
- Large teams.
- Want opinions and structure.
- Angular-style architecture.

### When NOT to use
- Small APIs (Express/Fastify simpler).
- Want minimal abstraction.

## Common Mistakes

- ❌ Not using modules (god module).
- ❌ Tight coupling between services.
- ❌ Business logic in controllers.
- ❌ Not using DI properly.

## Tools

- NestJS CLI: `npm i -g @nestjs/cli`
- NestJS docs: https://docs.nestjs.com/

## References

- NestJS: https://nestjs.com/

## Further Reading

- *NestJS in Action* — Gregor Woiwode

## Exercises

1. Build a CRUD API with modules, services, DTOs.
2. Add auth via guards.
3. Add validation via ValidationPipe.

## Projects

- Build an enterprise API with NestJS + Prisma + auth + tests.

---

**Previous:** [Fastify/](../Fastify/) · **Next:** [Python/](../Python/) · **Related:** [NodeJS/](../NodeJS/)
