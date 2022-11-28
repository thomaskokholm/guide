# Deploy mkdocs to GitHub Pages using GitHub Actions

If you're already hosting your code on GitHub, GitHub Pages is certainly the most convenient way to publish your project documentation. It's free of charge and pretty easy to set up.
with [GitHub Actions](https://github.com/features/actions)

Using GitHub Actions you can automate the deployment of your project documentation. At the root of your repository, create a new GitHub Actions workflow, e.g. .github/workflows/ci.yml, and copy and paste the following contents:

```yaml
name: ci
on:
  push:
    branches:
      - master
      - main
permissions:
  contents: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: 3.x
      - run: pip install mkdocs-material
      - run: mkdocs gh-deploy --force
```
