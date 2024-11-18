To generate a model inside a specific folder (e.g., a `models` folder) in Angular, you can specify the folder path when running the `ng generate model` command.

### Command:
```bash
ng generate model models/<model-name>
```

### Example:
To create a model named `user` inside a `models` folder:
```bash
ng generate model models/user
```

### Outcome:
This will generate:
- A `models` folder (if it doesn't already exist).
- A file named `user.model.ts` inside the `models` folder.

The structure will look like:
```
src/
├── app/
│   ├── models/
│   │   └── user.model.ts
```

### Generated Code:
The `user.model.ts` file will contain:
```typescript
export class User {
}
```