# Start-Up-List

- Se till att ha Node.js installerat på datorn, om du inte redan har det. Välj LTS (long-time support) när du ska välja version.  checka  med 
  ```
  node -v
- Installera VITE och välj TS eller JS. Notera punkten i slutet för att skapa filerna i den mappen ni befinner er i.

  ```
  npm create vite@latest .
- Lägg in/kontrollera .gitignore-filen så att ni slipper få med genererade filer (t.ex. .DS_Store, *.css.map, style.css).
- Ändra i filen vite.config.ts så att er base motsvarar namnet på ert repo.
  ```
  import { defineConfig } from 'vite';
  
  export default defineConfig({
    'base': '/adressen-till-ert-repo-här/' // TODO: Ändra till ert reponamn här
  });
- Installera ESLint
  ```
  npm init @eslint/config@latest
- Installera Prettier
  ```
  # Installera Prettier med npm (eller pnpm)
  npm install --save-dev --save-exact prettier
  # pnpm add -D -E prettier
  
  # Skapa en tom config-fil som heter .prettierrc
  node --eval "fs.writeFileSync('.prettierrc','{}\n')"
  # Skapa en prettierignore-fil för att ignorera vissa filer
  node --eval "fs.writeFileSync('.prettierignore','# Ignore artifacts:\nbuild\ncoverage\n')"
  
  # VÄLJ EN AV NEDAN! (Formaterar alla filer automatiskt)
  # Formatera med npm
  npx prettier . --write
  # Formatera med pnpm
  pnpm exec prettier . --write
  
  # Installera eslint-config-prettier för att Prettier och ESLint ska lira ihop:
  npm install --save-dev eslint-config-prettier
  # Alternativt med pnpm:
  pnpm add -D eslint-config-prettier
- Öppna sedan eslint.config.mjs-filen och lägg till dessa 2 rader:
  ```
  import globals from "globals";
  import pluginJs from "@eslint/js";
  import tseslint from "typescript-eslint";
  import eslintConfigPrettier from "eslint-config-prettier";
  
  /** @type {import('eslint').Linter.Config[]} */
  export default [
    {files: ["**/*.{js,mjs,cjs,ts}"]},
    {
      languageOptions: { globals: globals.browser },
      rules: {
        camelcase: "error",
        'comma-dangle': ['error', 'always-multiline'], // Enforce trailing commas in multiline
        'curly': ['error', 'all'], // Require curly braces for all control statements
        'no-console': 'warn', // Warn about console.log usage
      },
    },
    pluginJs.configs.recommended,
    ...tseslint.configs.recommended,
    eslintConfigPrettier
  ];
- Installer Prettier tilläget i VSC
- Öppna sedan filen .prettierrc och lägg in era regler i den
-  Starta om  VSC

    Gå in på GitHub i ert repo, gå till fliken Settings --> Pages och aktivera Pages, välj GitHub Actions i dropdown-menyn. Lägg in publicerings-skript för Vite
   https://vite.dev/guide/static-deploy.html#github-pages) i mappen .github/workflows - döp filen till deploy.yml.

  
  
