```js
module.exports = {
  // Specifies this is the top-most directory with ESLint configs
  root: true,

  // Use the TypeScript ESLint parser (@typescript-eslint/parser)
  parser: "@typescript-eslint/parser",

  extends: [
    // One of the most popular ESLint rule package
    "airbnb-typescript/base",

    // Allows ESLint to run prettier as if it's just another check
    "plugin:prettier/recommended",
  ],

  // plugins: [
  //   "import",
  // ],

  // Required to be specified by some rules
  parserOptions: {
    project: "./tsconfig.json",
  },

  rules: {
    // Don't enforce use of a default export for files with a single export
    "import/prefer-default-export": "off",

    // Allow console logging
    "no-console": "off",

    // Allow using new for creating CDK constructs
    "no-new": "off",

    // Allow for of syntax
    // Source:
    // https://github.com/airbnb/javascript/blob/3dcc59112308211b6ac8478a4ad997ed3f17d9b1/packages/eslint-config-airbnb-base/rules/style.js#L345-L348
    // Debate: https://github.com/airbnb/javascript/issues/1271
    "no-restricted-syntax": [
      "error",
      {
        selector: "ForInStatement",
        message: "for..in loops iterate over the entire prototype chain, which is virtually never what you want. Use Object.{keys,values,entries}, and iterate over the resulting array.",
      },
      {
        selector: "LabeledStatement",
        message: "Labels are a form of GOTO; using them makes code confusing and hard to maintain and understand.",
      },
      {
        selector: "WithStatement",
        message: "`with` is disallowed in strict mode because it makes code impossible to predict and optimize.",
      },
    ],
  },

  // ESLint doesn't let us specify a path, so instead ignore non-source paths
  ignorePatterns: [
    "/build/**",
    "/dist/**",
    "/node_modules/**",
    ".eslintrc.js",
  ],
};

```