```zsh
bun add -D prettier prettier-plugin-tailwindcss @trivago/prettier-plugin-sort-imports
```

```json
{
  "printWidth": 100,
  "tabWidth": 2,
  "useTabs": true,
  "semi": true,
  "singleQuote": true,
  "jsxSingleQuote": true,
  "trailingComma": "all",
  "bracketSpacing": true,
  "jsxBracketSameLine": false,
  "arrowParens": "always",
  "proseWrap": "always",

  "plugins": [
    "@trivago/prettier-plugin-sort-imports",
    "prettier-plugin-tailwindcss"
  ],

  "importOrder": ["^[react]", "^[a-z]", "^@(?!/)", "^@/", "^[./]"],
  "importOrderSeparation": false,
  "importOrderSortSpecifiers": true
}
```
