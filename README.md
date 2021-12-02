# drat

The INWTLab drat repository.

## To install from this repository

```r
options(repos = c(getOption("repos"), INWTLab = "https://inwtlab.github.io/drat/"))
```

## Autodeploy R packages to this repo

Add the following to your .travis.yml file:

```yml
after_success:
    - test $TRAVIS_PULL_REQUEST == "false" &&
      test $TRAVIS_BRANCH == "master" &&
      curl https://raw.githubusercontent.com/INWTlab/drat/main/deploy.sh > deploy.sh &&
      bash deploy.sh
```

Add a deploy key to your .travis.yml:

1. Generate a new personal access token. Needs read access to public repos
2. Follow these steps on the command line:

```sh
# Install travis cli
brew install travis
# Login to travis -- easiest with another deploy-key
travis login --com --deploy-key $GH_TOKEN
# Generate secret and add to your .travis.yml
cd <to your r package repository>
travis encrypt GH_TOKEN=$GH_TOKEN --com --add env.global
```

3. Alternatively go to the settings of your project on travis-ci.com and add the env variable there.
