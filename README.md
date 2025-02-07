# About
This project was a part of the [env-decorators](https://github.com/gushi-cookie/env-decorators) that was moved to this repo due to security concerns. Sensitive [dev_containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) and docker files shouldn't be exposed to containers, since they may impact the host machine. There are no robust features that would help to exclude sensitive files from docker volumes.

Projects developed under `dev_containers` usually mount their root directory (aka git repo) to containers. It's a regular practice covered by the extension's docs. To fully use benefits of `dev_containers`, as a sort of an isolated machine, roots of projects should be mounted to workspaces of their containers. Even if a single repo project has modules or services that can be developed independently, it is still needed to mount the whole root of the project. There is no way to "chunk" or mount a part of a git repo. That's why this repo was created.


# How to develop the main project
Requirements: docker, docker-compose, vscode and [dev_containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension should be installed.

Firstly, both [env-decorators](https://github.com/gushi-cookie/env-decorators) and [env-decorators-devcontainer](https://github.com/gushi-cookie/env-decorators-devcontainer) should be cloned in a same directory and environment files be configured:
```
# Cloning
cd ~/my-projects/
git clone https://github.com/gushi-cookie/env-decorators.git
git clone https://github.com/gushi-cookie/env-decorators-devcontainer.git

# Configuring according to preferences
cd .devcontainer/
cp .env.sample .env
nano .env
```

Supposed that both projects are in a same directory and `dev_containers` configs can access the main project through `env-decorators` directory, of the parent directory.

Now to start vscode in a dev container press `F1` in vscode and click on `Dev Containers: Reopen in Container`. It will build necessary docker images if needed. All should work fine and sensitive files are fully isolated.