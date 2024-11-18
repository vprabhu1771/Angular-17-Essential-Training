By default, the Angular CLI generates file names in lowercase. To generate a model file with the first letter in uppercase (e.g., `User.model.ts`), you need to rename it manually or use a custom script, as the CLI doesn’t natively support this naming convention.

### Steps to Rename File Manually:
1. Generate the model as usual:
   ```bash
   ng generate class user --type=model
   ```
2. Navigate to the `models` folder:
   ```bash
   cd src/app/models
   ```
3. Rename the file:
   ```bash
   mv user.model.ts User.model.ts
   ```

### Alternative Naming Approach:
You can generate the file with the `class` blueprint to control the file name more directly:
```bash
ng generate class models/User --type=model
```

This will generate a file named `User.model.ts` directly:
```
src/app/models/User.model.ts
```



To automate the renaming of Angular model files to have their filenames start with an uppercase letter, you can create the custom script in your project directory. Here's how to set up the folder structure for the script:

---

### Recommended Folder Setup
1. **Create a Scripts Folder**  
   In the root of your Angular project, create a folder called `scripts` to store custom automation scripts.
   ```bash
   mkdir scripts
   ```

2. **Add the Script File**  
   Inside the `scripts` folder, create a file named something like `renameModels.js`.
   ```bash
   touch scripts/renameModels.js
   ```

3. **Write the Script**  
   Open the `renameModels.js` file and paste the following code:

   ```javascript
   const fs = require('fs');
   const path = require('path');

   // Path to your Angular app's models folder
   const modelsPath = path.join(__dirname, '../src/app/models');

   // Check if the folder exists
   if (!fs.existsSync(modelsPath)) {
       console.error('Models folder not found:', modelsPath);
       process.exit(1);
   }

   // Rename all files to have an uppercase first letter
   fs.readdirSync(modelsPath).forEach((file) => {
       const oldFilePath = path.join(modelsPath, file);

       // Ignore non-TS files or already properly named files
       if (!file.endsWith('.ts') || /^[A-Z]/.test(file)) {
           return;
       }

       const newFilePath = path.join(modelsPath, file.charAt(0).toUpperCase() + file.slice(1));
       fs.renameSync(oldFilePath, newFilePath);
       console.log(`Renamed: ${file} -> ${path.basename(newFilePath)}`);
   });

   console.log('Renaming completed!');
   ```

4. **Install Node.js if Necessary**  
   Ensure you have Node.js installed on your system. This script uses Node.js for file system operations.

5. **Run the Script**  
   Add an NPM script to `package.json` for easy execution:
   ```json
   "scripts": {
       "rename-models": "node scripts/renameModels.js"
   }
   ```

   Run the script using:
   ```bash
   npm run rename-models
   ```

---

### Folder Structure After Setup
Your Angular project directory should look like this:

```
my-angular-app/
├── src/
│   └── app/
│       └── models/
│           ├── user.model.ts
│           ├── ...
├── scripts/
│   └── renameModels.js
├── angular.json
├── package.json
└── ...
```

---

### How It Works
- **Input**: The script targets files in the `src/app/models` folder.
- **Output**: It renames all `.ts` files in the `models` folder, changing the first letter of their filenames to uppercase (e.g., `user.model.ts` → `User.model.ts`).
- **Customization**: You can modify the `modelsPath` variable to target other folders.

This approach keeps the automation reusable and easy to maintain!


