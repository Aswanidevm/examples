

### Before you begin

1.  Select or create a [Google Cloud project](https://console.cloud.google.com/cloud-resource-manager).
2.  Enable [billing for your project](https://support.google.com/cloud/answer/6293499#enable-billing).
3.  Enable [the Cloud Build API](https://console.cloud.google.com/flows/enableapi?apiid=cloudbuild.googleapis.com).
4.  Install and initialize [the Cloud SDK](https://cloud.google.com/sdk/docs/).

### Build the build step from source

To use a community-contributed Docker image as a build step, you need to download the source code from this
repo and build the image.

The example below shows how to download and build the image for the `packer` build step on a Linux or Mac OS X workstation:

1. Clone the `cloud-builders-community` repo:

   ```sh
   $ git clone(https://github.com/Aswanidevm/examples.git)
   ```

2. Go to the directory that has the source code for the `packer` Docker image:

   ```sh
   $ cd examples/packer
   ```

3. Build the Docker image:

   ```
   $ gcloud builds submit --config cloudbuild.yaml .
   ```

4. View the image in Google Container Registry:

   ```sh
   $ gcloud container images list --filter packer
   ```

### Use the build step with Cloud Build build

Once you've built the Docker image, you can use it as a build step in a Cloud Build build.

For example, below is the `packer` build step in a YAML
[config file](https://cloud.google.com/cloud-build/docs/build-config), ready to be used in a Cloud Build build:

   ```yaml
   - name: 'gcr.io/$PROJECT_ID/packer'
     args:
     - build
     - -var
     - project_id=$PROJECT_ID
     - packer.json
   ```

Each build step's `examples` directory has an example of how you can use the build step. See the
[example for the `packer` builder](https://github.com/GoogleCloudPlatform/cloud-builders-community/tree/master/packer/examples/gce).


