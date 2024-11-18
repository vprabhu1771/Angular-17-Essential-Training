To set up `base_url` in Angular's environment files, follow these steps:

### 1. **Generate Environment Files**
If the environment files are not already created, use the Angular CLI to generate them:

```bash
ng generate environments
```

This will create the following files in the `src/environments` directory:
- `environment.ts` (for development)
- `environment.prod.ts` (for production)

---

### 2. **Add `base_url` to the Environment Files**
Edit the `environment.ts` and `environment.prod.ts` files to include your `base_url`.

#### `environment.ts` (Development):
```typescript
export const environment = {
  production: false,
  base_url: 'http://localhost:3000/api' // Example for local development
};
```

#### `environment.prod.ts` (Production):
```typescript
export const environment = {
  production: true,
  base_url: 'https://your-production-url.com/api' // Example for production
};
```

---

### 3. **Use the `base_url` in Your Angular Services**
To use the `base_url` in your services for making API calls:

#### Example Service (`api.service.ts`):
```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { environment } from '../environments/environment';

@Injectable({
  providedIn: 'root'
})
export class ApiService {
  private baseUrl = environment.base_url;

  constructor(private http: HttpClient) {}

  getData(endpoint: string) {
    return this.http.get(`${this.baseUrl}/${endpoint}`);
  }
}
```

---

### 4. **Switching Environments**
When you build your Angular app, the environment files are swapped automatically based on the build configuration:

#### For Development:
```bash
ng serve
```

#### For Production:
```bash
ng build --prod
```

The `base_url` will point to the respective value in `environment.ts` or `environment.prod.ts`.

---

This setup ensures you can easily manage different `base_url` values for various environments.