For automatic linting and formatting, we will be using:
(test)[vf]

- [ESLint](https://eslint.org/)
- Prettier[https://prettier.io/]
- Husky[https://typicode.github.io/husky/#/]
- lint-staged[https://github.com/okonet/lint-staged#why]

There’s many code quality tools out there for TypeScript, but ESLint and Prettier are two of the most popular and well supported ones

[What’s the difference between Prettier and ESLint?](https://prettier.io/docs/en/comparison.html)

```
Linters have two categories of rules:

Formatting rules: eg: max-len, no-mixed-spaces-and-tabs, keyword-spacing, comma-style…

Prettier alleviates the need for this whole category of rules! Prettier is going to reprint the entire program from scratch in a consistent way, so it’s not possible for the programmer to make a mistake there anymore :)

Code-quality rules: eg no-unused-vars, no-extra-bind, no-implicit-globals, prefer-promise-reject-errors…

Prettier does nothing to help with those kind of rules. They are also the most important ones provided by linters as they are likely to catch real bugs with your code!

In other words, use Prettier for formatting and linters for catching bugs!
```

When you start, your package.json file’s scripts and devDependencies blocks may look like this.
```json
{
  "scripts": {
    "clean": "rm -rf dist && rm -rf cdk.out",
    "build": "tsc",
    "watch": "tsc -w",
    "prepare": "npm run-script build",
    "test": "echo OK"
  },
  "devDependencies": {
    "@types/node": "^12.12.0",
    "typescript": "~4.0.0"
  }
}
```

Steps
Add prettier, husky, lint-staged, and all of the eslint-related packages as dev dependencies. You should look up each package in npmpm to figure out its latest version and use that.
To add dependencies, use the following command
Amazon:
```bash
 brazil-build app install --save-dev <package>
```

For this example we will be pulling in the following:
```json
{
  "devDependencies": {
    "@types/node": "^12.12.0",
    "@typescript-eslint/eslint-plugin": "^4.4.0",
    "@typescript-eslint/parser": "^4.4.0",
    "eslint": "^7.11.0",
    "eslint-config-airbnb-typescript": "^11.0.0",
    "eslint-config-prettier": "^6.12.0",
    "eslint-plugin-import": "^2.22.0",
    "eslint-plugin-prettier": "^3.1.0",
    "husky": "^4.3.0",
    "lint-staged": "^10.4.0",
    "prettier": "^2.1.0",
    "typescript": "~4.0.0"
  }
}
```

There’s a lot of ESLint packages, so here’s why each one is important: 

- @typescript-eslint/parser enables ESLint’s new TypeScript parser,  
- @typescript-eslint/eslint-plugin enables ESLint plugins which allows ESLint to run prettier formatting with eslint-plugin-prettier,  
- eslint-config-airbnb-typescript is the one of the most popular ESLint rules package around which we use as a base
- eslint-config-prettier overrides all ESLint formatting rules that would interfere with prettier making them no-ops
- eslint-plugin-import is required to be installed by the Airbnb package.

```
brazil-build app install --save-dev @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint eslint-config-airbnb-typescript eslint-config-prettier eslint-plugin-import eslint-plugin-prettier husky lint-staged prettier

```

NPM
TODO

--- 

Setup the eslintrc file in root directory:
- Checkout the sample

--- 

Update your package.json’s scripts. You’ll need to add new scripts and modify the prepare script.

```json
{
  "scripts": {
    "clean": "rm -rf dist && rm -rf cdk.out",
    "build": "tsc",
    "watch": "tsc -w",
    "lint-fix": "eslint --fix lib/",
    "prepare": "npm run lint-fix && npm run build",
    "test": "echo OK"
  }
}
```

---

- Configure Husky to add a git pre-commit hook which triggers lint-staged. 
- Configure lint-staged to run eslint --fix on all staged files when you run git commit command. You can do this by adding the following to the top-level of your package.json file.

```json
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "lib/**/*.ts": [
      "eslint --fix",
      "git add"
    ]
  }
}
```

On git commit, lint-staged will look through git’s staged files, match that against lib/**/*.ts , then runs eslint --fix <list of matched files> . If that passes, then it runs git add <list of matched files> and proceeds with the commit. If it fails, then the commit fails and your staged files will be unaffected.

--- 

Checkpoint: 

In the end your package.json file from above would have its scripts, devDependencies, husky, and lint-staged blocks looking like this:

```json
{
  "scripts": {
    "clean": "rm -rf dist && rm -rf cdk.out",
    "build": "tsc",
    "watch": "tsc -w",
    "lint-fix": "eslint --fix lib/",
    "prepare": "npm run lint-fix && npm run build",
    "test": "echo OK"
  },
  "devDependencies": {
    "@types/node": "^12.12.0",
    "@typescript-eslint/eslint-plugin": "^4.4.0",
    "@typescript-eslint/parser": "^4.4.0",
    "eslint": "^7.11.0",
    "eslint-config-airbnb-typescript": "^11.0.0",
    "eslint-config-prettier": "^6.12.0",
    "eslint-plugin-import": "^2.22.0",
    "eslint-plugin-prettier": "^3.1.0",
    "husky": "^4.3.0",
    "lint-staged": "^10.4.0",
    "prettier": "^2.1.0",
    "typescript": "~4.0.0"
  },
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "lib/**/*.ts": [
      "eslint --fix",
      "git add"
    ]
  }
}
```

---

Setup intelliJ
- see picture

---

Override prettier config
- [many ways](https://prettier.io/docs/en/configuration.html)
- One way is using a base prettier object in your package.json file. For example, to increase the max line length of your code to 120 characters, add the following JSON object to your package.json file:
```json
{
  "prettier": {
    "printWidth": 120
  }
}
```

- A full list of configuration options can be found in Prettier’s documentation: https://prettier.io/docs/en/options.html


--- 

TODO: 
Differennce between dependencies and devDependencies

ref: https://w.amazon.com/bin/view/Users/skkrail/CDKTypeScriptPackageBestPractices/#MXd9CA6PNH0