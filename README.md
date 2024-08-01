# Heroku Review Apps GitHub Action
GitHub Action to create a Heroku Review App from a private repository on pull requests using the [Heroku Source Endpoint API](https://devcenter.heroku.com/articles/build-and-release-using-the-api#sources-endpoint) to upload the code. 
The Review App is automatically removed when the pull request is closed.
In a GitHub Workflow, this action requires to be preceeded by the [actions/checkout](https://github.com/actions/checkout) to work properly.

## Disclaimer
The author of this article makes any warranties about the completeness, reliability and accuracy of this information. **Any action you take upon the information of this website is strictly at your own risk**, and the author will not be liable for any losses and damages in connection with the use of the website and the information provided.