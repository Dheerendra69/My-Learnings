### Ques - What is Inject and Injectable in nestjs?

In NestJS, `@Injectable()` and `@Inject()` are the building blocks of **Dependency Injection (DI)**. They allow the framework to manage how different parts of your application (like Services, Repositories, and Helpers) are created and shared.

---

## 1. `@Injectable()`

This is a **class decorator**. When you place it above a class, you are telling NestJS: *"This class is a provider that should be managed by the Nest IoC (Inversion of Control) container."*

* **Primary Purpose:** To allow the class to be "injected" into other classes (like Controllers or other Services).
* **Automatic Dependency Resolution:** If an `@Injectable()` class has its own dependencies in its constructor, NestJS will automatically look those up and provide them too.

**Example:**

```typescript
@Injectable()
export class UserService {
  findAll() {
    return ['User 1', 'User 2'];
  }
}

```

---

## 2. `@Inject()`

While NestJS can usually figure out what to inject based on the **Type** (e.g., `private userService: UserService`), there are times when it needs a hint. This is where the `@Inject()` **parameter decorator** comes in.

You use `@Inject()` when:

1. **Using String/Symbol Tokens:** You aren't injecting a class, but a custom provider identified by a string or a symbol (common for configuration or external libraries).
2. **Interface Injection:** Since TypeScript interfaces disappear at runtime, you use a token to tell Nest which implementation to provide.

**Example:**

```typescript
constructor(
  @Inject('CONFIG_OPTIONS') private config: any, // Injecting by string token
  @Inject(USER_REPOSITORY) private users: UserContract // Injecting by constant token
) {}

```

---

## 3. How They Work Together

The "Container" (IoC) acts as a warehouse. `@Injectable()` registers the class in the warehouse, and the constructor (with or without `@Inject()`) is the request form to pull items out of the warehouse.

### Comparison Table

| Feature | `@Injectable()` | `@Inject()` |
| --- | --- | --- |
| **Level** | Class Level | Constructor Parameter Level |
| **Function** | Marks a class as a "provider" available for use. | Explicitly requests a specific dependency. |
| **Requirement** | Required for almost all NestJS services. | Only required for non-class tokens (Strings/Symbols). |
| **Analogy** | A "For Hire" sign on a specialist's shop. | Calling a specific specialist by their name/ID. |

---

## Summary in the Context of Your Code

In the code you shared previously:

* The `ReportService` is marked `@Injectable()`, meaning NestJS will create one instance of it and share it wherever needed.
* The constructor uses `@Inject(USER_REPOSITORY)` because `USER_REPOSITORY` is likely a **constant string or symbol**. Without `@Inject`, Nest wouldn't know which specific object to provide for the `UserContract` interface.
