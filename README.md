#  AI-lab Experimental Software Templates

New candidate AI templates can be added under the `templates` folder. See `templates/sampleapp` for a sample template directory structure. Each template should have its own sub-directory under the templates folder.

## TODO: change instructions to use RHDH directly

## Usage in Red Hat Developer Hub

To import these templates click `Register Existing Component` on the Software Templates page.

![Screenshot](./assets/register.png)

Import `https://github.com/redhat-ai-dev/ai-lab-template/blob/main/all.yaml`

![Screenshot](./assets/register2.png)

## Usage in Backstage 

Add the following to your `app-config.yaml` file in your Backstage configuration:

``` 
    - type: url
      target:  https://github.com/redhat-ai-dev/ai-lab-template/blob/main/all.yaml
      rules:
        - allow: [Location, Template]
```

This will add the samples into a set of Backstage templates.

![Screenshot](./assets/catalog.png)


## On-prem Host Support

You need to ensure the on-prem host is being configured in the `app-config.yaml` file in your Backstage/RHDH configuration.

### Change Default Host for Git or Quay

The [properties](./properties) file holds the default host for GitHub, GitLab and Quay.

Modifying the value and running `./generate.sh` will generate new templates with the customized default value.

### Providing On-prem Host Value When Creating a Component

On the `Application Repository Information` page provide your Git host under the `Repository Server` input.

**Note:** Please ensure the correct `Host Type` is selected.

![Screenshot](./assets/on-prem-git.png)

On the `Deployment Information` page provide your Quay host under the `Image Registry` input.

![Screenshot](./assets/on-prem-quay.png)
 
## Contributing

The templates are found in [./templates](./templates) and reference reusable content in [./skeleton](./skeleton).  

The templates are maintained by importing external samples into the software template format. This allows the external samples to be used standalone, developed, and evolved and then imported.

The pipelines are also maintained externally to allow standalone use outside of software templates, as well as evolution of the pipelines in one or more software templates.

To update the templates from these or any new samples you update the list of imported repos and run the following: 


 [`./generate.sh`](./generate.sh) to generate all the templates before committing to this repository.

 [`import-ai-lab-samples`](./scripts/import-ai-lab-samples), [`import-gitops-template`](./scripts/import-gitops-template) and [`update-tekton-definition`](./scripts/import-gitops-template) take `repourl` and `branch` name as environment variables when running the scripts.
 
 The following can be set respectively:
 
 `SAMPLE_REPO`/`GITOPS_REPO`/`PIPELINE_REPO` and `SAMPLE_BRANCH`/`GITOPS_BRANCH`/`PIPELINE_BRANCH`


## Adding Custom Models

For information regarding adding custom models that are not pre-packaged as part of the Podman Desktop AI Lab extension see [adding-custom-models.md](./adding-custom-models.md)


### MacOS 

Due to differences between Linux and MacOS, the GNU version of `sed` is required to be installed.

```
brew install gnu-sed
```
After this, alter PATH. For example, add the following line to your `~/.bash_profile`:
```
export PATH="/opt/homebrew/opt/gnu-sed/libexec/gnubin:$PATH"
```