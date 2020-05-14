# Gigalixir for GitLab

This provides a template for deploying review apps in GitLab using Gigalixir. It can also be repurposed for regular deploys since the template should be similar. This assumes that you are using Elixir releases and not other modes of release, and GitLab CI.

## What this does

This generates a review app and uses the branch or `CI_COMMIT_REF_NAME` as an identifier. However, because Gigalixir doesn't clear used names upon deletion, you need a unique identifier. This config file prepends a random 5 character string (a-z only), and shortens the branch's name by getting the first 2 positions delimited by a character. This can be expanded if you find 5 characters too short.

e.g

Branch: `132-add-review-app-to-ci`

App name: `lajsd-132-add`

## Why name it like that?

The reason why is that Gigalixir has an app name limit. If it's too long then it would cause the provisioning of the database to get stuck at `PENDING_CREATE`, and when trying to delete would also be stuck at `PENDING_DELETE`. I had to discover this the hard way! :)

## How to use

Copy the files over to the root directory of the project. In `rel/overlays/Procfile` be sure to change `<APP_NAME>` with your project's app name as a module. `my_app` would be `MyApp`.

## Environment variables

Set these environment variables in the CI/CD.

| Name  | Description  |
|---|---|
| `GIALIXIR_LOGIN_EMAIL`  | Your Gigalixir account's email  |
| `GIGALIXIR_LOGIN_PASSWORD`  | Account password  |
| `SSH_PRIVATE_KEY`   | SSH private key to access your Gigalixir servers  |
