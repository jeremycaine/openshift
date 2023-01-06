# Podman on MacBook Pro M1
The basic installation intstruction are [here](https://podman.io/getting-started/installation)

## Test Podman
```
podman machine init --cpus 2
podman machine start
podman images
git clone http://github.com/baude/alpine_nginx && cd alpine_nginx
podman build -t alpine_nginx .
podman run -dt -p 9999:80 alpine_nginx
curl http://localhost:9999
```



