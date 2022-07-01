<!-- start title -->

# GitHub Action:Managed Build and Push Image to Registry

<!-- end title -->
<!-- start description -->

Builds and pushes an image to a registry in a managed fashion

<!-- end description -->
<!-- start contents -->
<!-- end contents -->
<!-- start usage -->

```yaml
- uses: atomicfi/action-managed-build-push-image-registry@undefined
  with:
    # Name of the repository to push images to (based on ECR). Defaults to the Git repository's name.
    # Default: ${{ github.repository }}
    repository: ""

    # git tags to push, comma separated string such as `latest,v1.0.0`. Required.
    # Default:
    tag-versions: ""

    # docker context. Passed to [docker build push action context
    # input](https://github.com/docker/build-push-action#inputs). It should be
    # relative to the root of the commit that triggered the action
    # Default: ./
    docker-context: ""

    # path to docker file relative to docker-context. Passed to [docker build push
    # action file input](https://github.com/docker/build-push-action#inputs)
    # Default: Dockerfile
    docker-file: ""
```

<!-- end usage -->
<!-- start inputs -->

| **Input** | **Description** | **Default** | **Required** |
| :-------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------: | :----------: |
| **`repository`** | Name of the repository to push images to (based on ECR). Defaults to the Git repository's name. | `${{ github.repository }}` | **false** |
| **`tag-versions`** | git tags to push, comma separated string such as `latest,v1.0.0` |  | **true** |
| **`docker-context`** | docker context. Passed to [docker build push action context input](https://github.com/docker/build-push-action#inputs). It should be relative to the root of the commit that triggered the action | `./` | **false** |
| **`docker-file`** | path to docker file relative to docker-context. Passed to [docker build push action file input](https://github.com/docker/build-push-action#inputs) | `Dockerfile` |  **false** |

<!-- end inputs -->
<!-- start outputs -->
<!-- end outputs -->
<!-- start examples -->

### Example usage

```yaml
name: Build and push image to registry
on:
  release:
    types: [created]
jobs:
  build-push-image:
    runs-on: ubuntu-latest
    steps:
      - uses: atomicfi/action-managed-build-push-image-registry@v1
        with:
          repository: "repo-name"
          tag-version: ${{ bump-version-job.output.version }}
          docker-context: "sub-folder"
          docker-file: "custom-name"
```

<!-- end examples -->
