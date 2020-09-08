# Web Development

To keep any form of web development consistent please adhere to these guidelines:
- Use [TypeScript](https://www.typescriptlang.org/) - this will promote better maintainability, early bug catching
- Follow common [code style](#Code-Style) 
- Use code linter tools: [ESLint](https://eslint.org/docs/about/), [Prettier](https://prettier.io/docs/en/index.html)
- Preferred package manager is [Yarn](https://yarnpkg.com/) 

## Code Style

Here are configuration snippets.

### Prettier configuration snippet

```json
{
  "semi": false,
  "trailingComma": "all",
  "singleQuote": false,
  "printWidth": 120,
  "tabWidth": 4
}
```

### ESLint configuration snippet

```json
{
  "parser": "@typescript-eslint/parser",
  "extends": [
    "plugin:react/recommended",
    "plugin:@typescript-eslint/recommended",
    "prettier/@typescript-eslint",
    "plugin:prettier/recommended"
  ],
  "parserOptions": {
    "ecmaVersion": 2018,
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "plugins": [
    "import"
  ],
  "rules": {
    "react/prop-types": "off",
    "import/order": ["error", {
      "newlines-between": "always"
    }],
    "no-restricted-imports": ["error", {
      "patterns": [
        "*-main"
      ]
    }]
  },
  "settings": {
    "react": {
      "version": "detect"
    }
  }
}

```
