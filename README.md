<!-- start title -->

# GitHub Action:Managed Build and Push Image to Registry

<!-- end title -->
<!-- start description -->

Builds and pushes an image to a registry in a managed fashion for internal use

<!-- end description -->
<!-- start contents -->
<!-- end contents -->
<!-- start usage -->

```yaml
- uses: atomicfi/action-managed-build-push-image-registry@undefined
  with:
    # Name of the registry repository to push images to (based on ECR). Defaults to the Git repository's name.
    # Default: ${{ github.repository }}
    registry-repo-name: ""

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

    # AWS access key id. Required.
    # Default:
    aws-access-key-id:

    # AWS secret access key. Required.
    # Default:
    aws-secret-access-key:
```

<!-- end usage -->
<!-- start inputs -->

| **Input** | **Description** | **Default** | **Required** |
| :-------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------: | :----------: |
| **`registry-repo-name`** | Name of the registry repository to push images to (based on ECR). Defaults to the Git repository's name. | `${{ github.repository }}` | **false** |
| **`tag-versions`** | git tags to push, comma separated string such as `latest,v1.0.0` |  | **true** |
| **`docker-context`** | docker context. Passed to [docker build push action context input](https://github.com/docker/build-push-action#inputs). It should be relative to the root of the commit that triggered the action | `./` | **false** |
| **`docker-file`** | path to docker file relative to docker-context. Passed to [docker build push action file input](https://github.com/docker/build-push-action#inputs) | `Dockerfile` |  **false** |
| **`aws-access-key-id`**     | AWS access key id                   |             |   **true**   |
| **`aws-secret-access-key`** | AWS secret access key               |             |   **true**   |
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
          registry-repo-name: "repo-name"
          tag-version: ${{ bump-version-job.output.version }}
          docker-context: "sub-folder"
          docker-file: "custom-name"
          aws-access-key-id: ${{ secrets.YOUR_AWS_ACCESS_KEY_ID }}
          aws-secret-access-key:  ${{ secrets.YOUR_AWS_SECRET_ACCESS_KEY }}
```

<!-- end examples -->
