# Sample Pytorch Project with Docker

## Install
Clone repositry
```bash
git clone git@github.com:sh1027/docker_pytorch.git
```

Modify `docker/.env`
```bash
COMPOSE_PROJECT_NAME=$USER
UID=1000  # <- replace with your UID
GID=1000  # <- replace with your GID
WORKDIR_LOCAL=PATH_TO_WORKDIR  # <- replace with your WORKDIR
HOST_PORT=8888  # <- replace with your HOST_PORT if necessary
CONTAINER_PORT=8888  # <- replace with your CONTAINER_PORT if necessary
```
You can check your UID and GID from the command below.
```bash
id -u # UID
id -g # GID
```

Docker compose up
```bash
cd docker
docker-compose up -d
```

Execute command in Docker
```bash
docker exec -it -w /workspace {USER_NAME} bash
```

## Using JupyterLab (Optional)
```bash
python -m jupyterlab --ip 0.0.0.0 --port {CONTAINER_PORT} --allow-root
```