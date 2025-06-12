<p align="center">
  <h1 align="center">🚀 Dokploy Deploy GitHub Action</h1>
  <p align="center">
    Trigger deployments on your <a href="https://dokploy.com" target="_blank">Dokploy</a> instance — whether it’s an application or a Docker Compose project — directly from your GitHub Actions workflows.
  </p>
</p>

## 📦 Features

- Deploy a Dokploy application or compose project.
- Automatically fetch application/compose ID if not provided.
- Built-in error handling for deployment failures.
- Secure integration using API keys.

## 🧰 Inputs

| Input            | Description                                                                                                                                         | Required | Default Value |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------------- |
| `dokploy_url`    | Dokploy base URL, e.g. https://dokploy.example.com                                                                                                  | ✅       |               |
| `api_key`        | Dokploy API key.                                                                                                                                    | ✅       |               |
| `type`           | Dokploy deployment type. Valid values – `application`, `compose`.                                                                                   |          | "application" |
| `compose_id`     | Optional. Dokploy compose ID to deploy. If not provided, it will be fetched from Dokploy based on `project_name` and `app_name`.                    |          |               |
| `application_id` | Optional. Dokploy application ID to deploy. If not provided, it will be fetched from Dokploy based on `project_name` and `app_name`.                |          |               |
| `project_name`   | Optional. Dokploy project name, if `compose_id` or `application_id` is not provided, it will be used to get from dokploy.                           |          |               |
| `app_name`       | Optional. Dokploy app name (within your Dokploy project), if `compose_id` or `application_id` is not provided, it will be used to get from dokploy. |          |               |

## 🚦 Usage

Deploy a Dokploy application by App Name and Project Name:

```yaml
name: Deploy to Dokploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Deploy App to Dokploy
        uses: qbix-tech/dokploy-deploy-action@v1
        with:
          dokploy_url: https://dokploy.example.com
          api_key: ${{ secrets.DOKPLOY_API_KEY }}
          project_name: My Project
          app_name: my-app
```

Deploy a Dokploy compose by Project Name and App Name:

```yaml
name: Deploy to Dokploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Deploy App to Dokploy
        uses: qbix-tech/dokploy-deploy-action@v1
        with:
          dokploy_url: https://dokploy.example.com
          api_key: ${{ secrets.DOKPLOY_API_KEY }}
          type: compose
          project_name: My Project
          app_name: my-app
```

Deploy a Dokploy application by Application ID:

```yaml
name: Deploy to Dokploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Deploy App to Dokploy
        uses: qbix-tech/dokploy-deploy-action@v1
        with:
          dokploy_url: https://dokploy.example.com
          api_key: ${{ secrets.DOKPLOY_API_KEY }}
          application_id: g9whzep25kjx044oqq55g8q7
```

Deploy a Dokploy compose by Compose ID:

```yaml
name: Deploy to Dokploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Deploy App to Dokploy
        uses: qbix-tech/dokploy-deploy-action@v1
        with:
          dokploy_url: https://dokploy.example.com
          api_key: ${{ secrets.DOKPLOY_API_KEY }}
          type: compose
          compose_id: jddl377m0cfrtzy604n5fzi4
```
