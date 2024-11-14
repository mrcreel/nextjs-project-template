I. Setup

&nbsp;&nbsp;A. Init commit

```bash
pnpm create next-app@latest [directory]
```

&nbsp;&nbsp;B. Setup [Commitizen](https://www.npmjs.com/package/commitizen)

  &nbsp;&nbsp;&nbsp;&nbsp;1. Install Commitizen

```bash
        pnpm -i -g commitizen
```

  &nbsp;&nbsp;&nbsp;&nbsp;2. Initizlize Commitizen

```bash
        pnpm dlx commitizen init cz-conventional-changelog --save-dev --save-exact
```

  &nbsp;&nbsp;&nbsp;&nbsp;4. Make a commit: Use the Commitizen command:
```bash
        git add .
        cit cz
```

&nbsp;&nbsp;C. Installing [commit-and-tag-version](https://www.npmjs.com/package/commit-and-tag-version)

&nbsp;&nbsp;&nbsp;&nbsp;1. Install and add to devDependencies:

```bash
        pnpm i -g commit-and-tag-version
```

&nbsp;&nbsp;&nbsp;&nbsp;2. Add an npm run script to your package.json:

```json
    //package.json
    {
        "scripts": {
            "release": "commit-and-tag-version"
        }
    }
```

&nbsp;&nbsp;&nbsp;&nbsp;3. Generate your changelog for your first release

```bash
    pnpm exec commit-and-tag-version --first-release
```

&nbsp;&nbsp;&nbsp;&nbsp;4. To create a new release, do this

```bash
    pnpm release
```

Output:
```bash
    ✔ bumping version in package.json from 0.1.0 to 0.1.1
    ✔ outputting changes to CHANGELOG.md
    ✔ committing package.json and CHANGELOG.md
    ✔ tagging release v0.1.1
    ℹ  Run `git push --follow-tags origin main` to publish
```
 &nbsp;&nbsp;&nbsp;&nbsp;5. Run to push to remote
 ```bash
    git push --follow-tags origin main
 ```

&nbsp;&nbsp;D. Install and setup [Semantic release](https://www.npmjs.com/package/@semantic-release/github)

&nbsp;&nbsp;&nbsp;&nbsp;A. Install dependencies

```bash
    pnpm i -D @semantic-release/github
```

&nbsp;&nbsp;&nbsp;&nbsp;B. Configuration

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;i. Create a .releaserc config file

```ts
// .releaserc
      {
        "branches": ["main", "next"],
        "plugins": [
          "@semantic-release/commit-analyzer",
          "@semantic-release/release-notes-generator",
          [
            "@semantic-release/github",
            {
              "assets": [
                { "path": "dist/asset.min.css", "label": "CSS distribution" },
                { "path": "dist/asset.min.js", "label": "JS distribution" }
              ]
            }
          ]
        ]
      }
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ii. Follow the steps [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-fine-grained-personal-access-token) to create a GitHub Personal Access Token.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;iii. Follow along with [this post](https://dev.to/sahanonp/how-to-setup-semantic-release-with-github-actions-31f3) to set token in repo.

GitHub Actions: Create a .github/workflows/release.yml file with the following content

```yml
    
name: Release

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Install dependencies
        run: npm install

      - name: Run release
        run: npx semantic-release
```




&nbsp;&nbsp;B. Install and Setup [](https://www.npmjs.com/package/)

&nbsp;&nbsp;&nbsp;&nbsp;A. 

```bash
    pnpm i -D 
```