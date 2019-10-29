# App

A sample 12 Factor Application.

## Usage

Generate TLS certificates:

```
$ go run certgen/main.go
```
```
wrote ca.pem
wrote ca-key.pem
wrote server.pem
wrote server-key.pem
```

### Build and Run

```
$ go build -o server ./monolith
```

```
$ ./server
```

```
2016/04/15 06:34:12 Starting server...
2016/04/15 06:34:12 HTTP service listening on 0.0.0.0:80
2016/04/15 06:34:12 Health service listening on 0.0.0.0:81
2016/04/15 06:34:12 Started successfully.
```

### Test with cURL

```
$ curl --cacert ./ca.pem -u user https://127.0.0.1:80/login
```
```
Enter host password for user 'user':
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InVzZXJAZXhhbXBsZS5jb20iLCJleHAiOjE0NjA5ODcxOTcsImlhdCI6MTQ2MDcyNzk5NywiaXNzIjoiYXV0aC5zZXJ2aWNlIiwic3ViIjoidXNlciJ9.x3oFhRhWk5CGYfGcrNctPGWCENEsXpUuKPDQU2ZOLCY
```

> type "password" at the prompt

```
curl --cacert ./ca.pem -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InVzZXJAZXhhbXBsZS5jb20iLCJleHAiOjE0NjA5ODcxOTcsImlhdCI6MTQ2MDcyNzk5NywiaXNzIjoiYXV0aC5zZXJ2aWNlIiwic3ViIjoidXNlciJ9.x3oFhRhWk5CGYfGcrNctPGWCENEsXpUuKPDQU2ZOLCY' https://127.0.0.1:5000/
```
```
<h1>Hello</h1>
```

# Notes
 - https://cloud.google.com/shell/docs/quickstart
 - https://ssh.cloud.google.com/cloudshell/editor
 - `gcloud config set project <project-id>`
 - `gcloud compute ssh ubuntu`

# Docker
 - sudo docker inspect -f '{{.Id}} -  {{.Name}} - {{.NetworkSettings.IPAddress }}' $(sudo docker ps -aq)
 - sudo docker stop $(sudo docker ps -aq)
 - sudo docker inspect <container name or cid>
 - CID=$(sudo docker run -d monolith:1.0.0)
 - CIP=$(sudo docker inspect --format '{{ .NetworkSettings.IPAddress }}' ${CID})
 - sudo docker images
 - sudo docker tag auth:1.0.0 kwiecien/auth:1.0.0
 - sudo docker push kwiecien/auth:1.0.0
