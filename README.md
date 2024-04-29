# drat

The INWTLab drat repository.

## To install from this repository

```r
options(repos = c(getOption("repos"), INWTLab = "https://inwtlab.github.io/drat/"))
```

## Autodeploy R packages to this repo

Add a `drat.yaml` to `.github/workflows`:

We are using the following gh-action: https://github.com/mikemahoney218/upload-to-drat-repo


```yml
on:
  push:
    branches:
      - 'main'
    paths:
      - 'DESCRIPTION'
  workflow_dispatch:

jobs:
  drat-upload:
    runs-on: ubuntu-20.04
    name: Drat Upload
    steps:
      - uses: mikemahoney218/upload-to-drat-repo@v0.3
        with:
          drat_repo: 'INWTlab/drat'
          token: "${{ secrets.GH_ACTION_DRAT }}"
          commit_message: "deploy to drat - update <YOURPACKAGENAME> via gh actions"
          commit_email: "brother-mfc@inwt-statistics.de"
          archive: true
```

* edit `commit_message`: enter the correct name of your R-Package
* add the Personal Access Token to your Repository
   * under Setting > Secrets and Variables > Actions - *New Repository secret*
   * Name: `GH_ACTION_DRAT`
