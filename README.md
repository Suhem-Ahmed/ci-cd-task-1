# Node.js App CI/CD Pipeline with GitHub Actions

This repository implements a CI/CD pipeline to automate building, testing, and deploying a sample Node.js web app as a Docker image to Docker Hub.

## Pipeline Overview
When code is pushed to the `main` branch, the workflow automatically:
1. Checks out repository code
2. Sets up Node.js and runs tests
3. Builds a Docker image for the app
4. Pushes the image to Docker Hub (using secure secrets)

## Key Files
| File Path                  | Purpose                                                                 |
|----------------------------|-------------------------------------------------------------------------|
| `server.js`                | Minimal Express web app                                                |
| `package.json`             | App dependencies and test scripts                                      |
| `Dockerfile`               | Instructions to build the Docker image                                 |
| `.github/workflows/main.yml` | GitHub Actions workflow definition for the CI/CD pipeline            |

## Setup Instructions
1. Create a Docker Hub account and generate an access token with write permissions.
2. Add `DOCKER_HUB_USERNAME` and `DOCKER_HUB_ACCESS_TOKEN` as secrets in the GitHub repo.
3. Push code to `main` to trigger the pipeline.

## Troubleshooting
- **Docker login failure**: Verify secrets are correctly set in GitHub.
- **Test failure**: Ensure the `npm test` script exits with code 0 (no errors).
- **Build failure**: Check the `Dockerfile` for syntax errors.

TESTING BUILD
