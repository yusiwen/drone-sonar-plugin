# drone-sonar-plugin
> Forked from aosapps/drone-sonar-plugin, and upgrade sonar-scanner-cli to 5.0.1 to support SonarQube server 10.x

The plugin of Drone CI to integrate with SonarQube (previously called Sonar), which is an open source code quality management platform.

Detail tutorials: [DOCS.md](DOCS.md).

### Build process
build go binary file: 
`GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -o drone-sonar`

build docker image
`docker build -t aosapps/drone-sonar-plugin .`


### Testing the docker image:
```commandline
docker run --rm \
  -e DRONE_REPO=test \
  -e PLUGIN_SOURCES=. \
  -e SONAR_HOST=http://localhost:9000 \
  -e SONAR_TOKEN=60878847cea1a31d817f0deee3daa7868c431433 \
  aosapps/drone-sonar-plugin
```

### Pipeline example
```yaml
steps
- name: code-analysis
  image: aosapps/drone-sonar-plugin
  settings:
      sonar_host:
        from_secret: sonar_host
      sonar_token:
        from_secret: sonar_token
```
