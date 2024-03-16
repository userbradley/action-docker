# GitHub Action: Docker build and push

A GitHub action to build and push docker images


## Quick Start


```yaml
on: [push]
name: "Docker build: <name>"

jobs:
  docker-build:
    runs-on: ubuntu-latest
    permissions:
      id-token: write
      contents: read
    name: Docker Build
    steps:
      - uses: actions/checkout@vv
      - name: Authenticate to Google
        uses: google-github-actions/auth@v2
        with:
          workload_identity_provider: projects/123456789/locations/global/workloadIdentityPools/my-pool/providers/my-provider
          service_account: my-service-account@my-project.iam.gserviceaccount.com
      - uses: userbradley/action-docker@v4.1.0
        with:
          googleProject: project
          repository: repo
          image: image
          directory: containers/name
```

## Inputs


| Name            | Description                                        | Required | Default Value     |
|-----------------|----------------------------------------------------|----------|-------------------|
| `googleProject` | Name of the google artifact registry project       | `true`   | `Null`            |
| `repository`    | Name of the Artifact Registry Repository           | `true`   | `Null`            |
| `image`         | Name of the Image to build                         | `true`   | `Null`            |
| `directory`     | Name of the Directory that contains the Dockerfile | `false`  | `containers/name` |
| `dockerfile`    | Name of the Dockerfile if not `Dockerfile`         | `false`  | `Dockerfile`      |
