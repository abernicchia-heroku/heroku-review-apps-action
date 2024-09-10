# Heroku Review Apps GitHub Action
GitHub Action to create a Heroku Review App from a private repository on pull requests using the [Heroku Source Endpoint API](https://devcenter.heroku.com/articles/build-and-release-using-the-api#sources-endpoint) to upload the code. 
The Review App is automatically removed when the pull request is closed.
In a GitHub Workflow, this action requires to be preceeded by the [actions/checkout](https://github.com/actions/checkout) to work properly.

## Disclaimer
The author of this article makes any warranties about the completeness, reliability and accuracy of this information. **Any action you take upon the information of this website is strictly at your own risk**, and the author will not be liable for any losses and damages in connection with the use of the website and the information provided. **None of the items included in this repository form a part of the Heroku Services.**

## How to use it
Create the following GitHub workflows under `.github/workflows` directory within your repository and add the following YAML files and configure them. 

This will be executed whenever a PR is [opened, reopened, synchronize, labeled]
```
# pr-opened.yml
name: Deploy PR (create Review App)

on:
  pull_request:
    paths-ignore:
      - '.github/workflows/**'
    types: [opened, reopened, synchronize, labeled]

jobs:
  build-pr:
    runs-on: self-hosted
    steps:
      - uses: actions/checkout@v4
      - uses: abernicchia-heroku/heroku-review-apps-action@v1
        with:
          heroku-api-key: ${{secrets.HEROKU_API_KEY}} # set it on GitHub as secret
          heroku-pipeline-id: ${{vars.HEROKU_REVIEWAPP_PIPELINE}} # set it on GitHub as variable at repository level
          remove-git-folder: false # if you want to override the default (true) - it's usually recommended to avoid exposing the .git folder 
```

This will be executed whenever a PR is [closed ]
```
# pr-closed.yml
name: Close PR (delete Review App)

on:
  pull_request:
    paths-ignore:
      - '.github/workflows/**'
    types: [closed]

jobs:
  close-pr:
    runs-on: self-hosted
    steps:
      - uses: abernicchia-heroku/heroku-review-apps-action@v1
        with:
          heroku-api-key: ${{secrets.HEROKU_API_KEY}} # set it on GitHub as secret
          heroku-pipeline-id: ${{vars.HEROKU_REVIEWAPP_PIPELINE}} # set it on GitHub as variable at repository level
```