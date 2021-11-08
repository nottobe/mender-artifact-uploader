# Mender Docker Compose Artifact
This action uploads mender artifacts to a mender server.

Refer [mender](https://mender.io/)


# Usage
See [action.yml](action.yml)


### Create Artifact
```yaml
steps:
  - uses: actions/checkout@v2

  - id: mender
    name: Create mender artifact
    uses: quartx-analytics/mender-docker-compose@v1.1.1
    with:
      compose-file: "docker-compose.yml"
      software-name: "project-name"
      device-types: "raspberrypi3 raspberrypi4"

  - name: Upload mender artifact
    uses: quartx-analytics/mender-artifact-uploader@v1.0.0
    with:
      artifact: ${{ steps.mender.outputs.artifact-file }}
      username: ${{ secrets.MENDER_USER }}
      password: ${{ secrets.MENDER_PASS }}
```
Here we use our other action to create mender artifacts, then use this upload action to upload the artifact to mender.
There are 3 required parameters that need to be passed to the upload action. The path to the artifact file,
the username & password for the mender server. It is recommended to use Github secrets for the username & password parameters.


# License
The scripts and documentation in this project are released under the [Apache License](LICENSE)
