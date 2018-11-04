View

```
docker image ls
docker container ls
```

Build
`docker build -t image-name .`

Run
`docker run -p 4000:80 -v /host/dir/:/container/dir image-name`

Stop
`docker stop container-id`