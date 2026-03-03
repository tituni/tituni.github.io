## Installing gitlab-ci-local

For fast testing install gitlab-ci-local for running jobs from the pipeline locally.

1. Use Ubuntu (can be installed in Windows) or use devcontainer (docker-in-docker) in VSCode

2. Install nvm (Node VersionManager)

```cmd
    sudo apt-get update
    sudo apt install curl
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
    export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
    nvm --version
```

- [How to install NVM on Ubuntu 22.04](https://www.geeksforgeeks.org/linux-unix/how-to-install-nvm-on-ubuntu-22-04/)

3. Install LTS versions of nodejs and npm

```cmd
    nvm install --lts
```

3. Install gitlab-ci-local

```cmd
    npm install -g gitlab-ci-local
```

4. Clone your repository 

Add .gitlab-ci-local-env file

```cmd
PRIVILEGED=true
ULIMIT=8000:16000
VOLUME=certs:/certs/client
VARIABLE="DOCKER_TLS_CERTDIR=/certs"
```

Add docker:dind service to your .gitlab-ci.yml -file (see example below)

```cmd
---
# @Description Build alpine
alpine-image:
  services:
    - docker:dind
  needs: []
  image: docker:cli
  stage: build
  script:
    - printenv
    - ls -all /certs/client
    - docker build .
```

- [gitlab-ci-local/examples/docker-in-docker-build](https://github.com/firecow/gitlab-ci-local/tree/master/examples/docker-in-docker-build)


5. Run CI/CD - pipeline locally

Run in the same folder as your .gitlab-ci.yml

```cmd
gitlab-ci-local --cwd .
```

Here are some additional information for further configuration:

6. Configure variables

    Since we are running this pipeline locally, we cannot access the CI/CD variables in gitlab we shall put them in config-files.

A) Using one file for all repos

 Create a file "variables.yml" inside of $HOME/.gitlab-ci-local - folder (NOTE: this is outside of your repo).  See example below.

    ```cmd
    project:
    gitlab_url/your_repo.git:
        # Will be type Variable and only available if remote is exact match
        CI_PROJECT_PATH: your_repo_path
        CI_PROJECT_DIR: .devcontainer/your_project_folder #depends on your setup
        REGISTRY_URL: image_registry_url
        REGISTRY_TOKEN: your_token
        REGISTRY_USER: your_username
        STAGING_HOST: your_host_ip
        MY_SSH_KEY: your_ssh_key
        DB_PASSWORD: your_db_password

    group:
        
    global:
        
    ```

B) Using project specific file inside your repo

    Create ".gitlab-ci-local-variables.yml" - file in the root of your repo, and add it to your .gitignore. See example below.

    ```cmd
    CI_PROJECT_PATH: your_repo_path
    CI_PROJECT_DIR: .devcontainer/your_project_folder #depends on your setup
    REGISTRY_URL: image_registry_url
    REGISTRY_TOKEN: your_token
    REGISTRY_USER: your_username
    STAGING_HOST: your_host_ip
    MY_SSH_KEY: your_ssh_key
    DB_PASSWORD: your_db_password
    ```

