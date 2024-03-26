Google Cloud Build community images
This repository contains source code for community-contributed Docker images. You can use these images as build steps for Google Cloud Build.

These are not official Google products.

How to use a community-contributed build step
Google Cloud Build executes a build as a series of build steps. Each build step is run in a Docker container. See the Cloud Build documentation for more details about builds and build steps.

Before you begin
Select or create a Google Cloud project.
Enable billing for your project.
Enable the Cloud Build API.
Install and initialize the Cloud SDK.
Build the build step from source
To use a community-contributed Docker image as a build step, you need to download the source code from this repo and build the image.

The example below shows how to download and build the image for the packer build step on a Linux or Mac OS X workstation:

Clone the cloud-builders-community repo:

$ git clone https://github.com/GoogleCloudPlatform/cloud-builders-community
Go to the directory that has the source code for the packer Docker image:

$ cd cloud-builders-community/packer
Build the Docker image:

$ gcloud builds submit --config cloudbuild.yaml .
View the image in Google Container Registry:

$ gcloud container images list --filter packer
Use the build step with Cloud Build build
Once you've built the Docker image, you can use it as a build step in a Cloud Build build.

For example, below is the packer build step in a YAML config file, ready to be used in a Cloud Build build:

- name: 'gcr.io/$PROJECT_ID/packer'
  args:
  - build
  - -var
  - project_id=$PROJECT_ID
  - packer.json
Each build step's examples directory has an example of how you can use the build step. See the example for the packer builder.

Contributing
We welcome contributions! See CONTRIBUTING for more information on how to get started. Please include a cloudbuild.yaml and at least one working example in your pull request.

Contribution Requirements
In order to accept your contribution, it must:

make clear that the builder image is pushed to the builder's project's registry. E.g., it specifies images: ['gcr.io/$PROJECT_ID/the-tool']. The builder will not be pushed to the gcr.io/cloud-builders registry.
include a simple sanity test in the cloudbuild.yaml config that builds and pushes the image. This can be as simple as invoking the tool with --help, and it ensures the tool is installed correctly and in the expected location within the image.
include some basic example describing how to use it. This helps new users get acquainted with the builder, and helps us ensure the builder continues to work as intended.
License
This source code is licensed under Apache 2.0. Full license text is available in LICENSE.

Support
To file issues and feature requests against these builder images, the usage of these build steps or the Cloud Build API in general, create an issue in this repo.

If you are experiencing an issue with the Cloud Build service or have a feature request, e-mail google-cloud-dev@googlegroups.com or see our Getting support documentation.
