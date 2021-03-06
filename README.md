# Repozytorium na potrzeby przedmiotu WIRDS 2021 -- dockerfile

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/DepartmentOfStatisticsPUE/wirds-2021-binder-rocker-przyklad/main?urlpath=rstudio)

Przykład z wykorzystaniem `dockerfile`, który wygląda następująco

```docker
## Use a tag instead of "latest" for reproducibility
FROM rocker/binder:latest

## Declares build arguments
ARG NB_USER
ARG NB_UID

## Copies your repo files into the Docker Container
USER root
COPY . ${HOME}
## Enable this to copy files from the binder subdirectory
## to the home, overriding any existing files.
## Useful to create a setup on binder that is different from a
## clone of your repository
## COPY binder ${HOME}
RUN chown -R ${NB_USER} ${HOME}

## Become normal user again
USER ${NB_USER}

## Run an install.R script, if it exists.
RUN if [ -f install.R ]; then R --quiet -f install.R; fi
```
