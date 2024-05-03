# 📄 Resume – Miguel Pimentel

Hello, I'm Miguel Pimentel and this repository holds the code for my [resume](https://registry.jsonresume.org/semanticdata).

[JSON Resume](https://jsonresume.org/) is an open-source initiative to create a JSON-based standard for resumes. I use their project to host my resume.

## 📦 Hosting your Resume

You can host yours in one of two ways: via GitHub Gist and via a GitHub Repository. Let's explore those.

### Hosting via GitHub Gist

The easy way to host your resume is by making a GitHub Gist name `resume.json` on <https://gist.github.com>.

For example, mine can be found at <https://gist.github.com/semanticdata/a2052f31ac55306c5859777baf2d8e4a> which then automatically gets hosted at <https://registry.jsonresume.org/semanticdata>.

You can then just edit your Gist using the online GUI and it should update within a minute.

### Hosting via GitHub Repository

If you would like to have your `resume.json` in a repository like this one. You can set up a Github Action that automatically updates your `resume.json` gist to match what is in your repository everytime you push. Take a look at the example below:

```yml
name: Update Resume Gist

on: push

jobs:
  update-resume-gist:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Update Resume Gist
        uses: exuanbo/actions-deploy-gist@v1
        with:
          token: ${{ secrets.TOKEN }}
          gist_id: a2052f31ac55306c5859777baf2d8e4a
          file_path: resume.json

```

## 🚩 Repository Resume Setup

1. Create a gist called `resume.json`.
2. Create or fork this repo and commit your updated `resume.json` to it.
3. Create a Personal Github token that has just the `gist` scope.
4. Go to your repository settings, under security, find "Secrets and variables", then open the Actions under it.
5. Add a new secret called `TOKEN` with the value being from the personal token you created in in step 3.
6. Now simply push to your repo, and your `resume.json` from the repo, will update your gist `resume.json` and thus updating the JSON Resume registry to match.

## ✔ Validating your Resume

We use [Resumed](https://www.npmjs.com/package/resumed), a lightweight JSON Resume builder to validate our `resume.json`. This prevents pushing invalid JSON, which will break your resume.

```sh
# Install Resumed
npm i resumed

# Validate resume
npm run validate

# Render resume
npm run render

# Create sample resume
npm run sample
```

## ⏳ Automatic Validation Pre-commit Validation

With the help of [Husky](https://typicode.github.io/husky/), a Git hook manager, we can validate our resume automatically before every commit. Preventing us from pushing invalid code. Here's a quick setup guide:

```sh
# Install Husky
npm install --save-dev husky

# Initiate Husky
npx husky init

# Adding a New Hook
echo "npm run validate" > .husky/pre-commit
```

Done! Now our validate script will run before all commits.

Enjoy!
