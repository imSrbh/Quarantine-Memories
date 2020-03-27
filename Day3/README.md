1. Clone this Repo
`git clone https://github.com/imSrbh/<>.git`

2. Build a docker image that has a functional systemd in it.  
```
docker build -t tljh-systemd . -f Dockerfile
```

3. Run a docker container with the image in the background, while bind mounting your TLJH repository under /srv/src.
```
docker run \
  --privileged \
  --detach \
  --name=tljh-dev \
  --publish 12000:80 \
  --mount type=bind,source=$(pwd),target=/srv/src \
  tljh-systemd
  ```
  
4. Get a shell inside the running docker container.
```
docker exec -it tljh-dev /bin/bash
```

5. Run the bootstrapper from inside the container (see step above): The container image is already set up to default to a dev install, so it’ll install from your local repo rather than from github.
```
python3 /srv/src/bootstrap/bootstrap.py --admin admin:password
```

6. You should be able to access the JupyterHub from your browser now at `http://localhost:12000`. Congratulations, you are set up to develop TLJH!
