# BuildingContainerOnKubernetes

Tekton Pipeline to build containers without Docker in Docker. 

## BuildKit

To install BuildKit agent on Kubernetes:
https://github.com/moby/buildkit/tree/master/examples/kubernetes

k apply -f deployment+service.rootless.yaml

### Using BuildKit to build container

$ buildctl \
  --addr tcp://[ips]:1234 \
  --tlscacert .certs/client/ca.pem \
  --tlscert .certs/client/cert.pem \
  --tlskey .certs/client/key.pem \
  build --frontend dockerfile.v0 --local context=/tmp/node-docker-example --local dockerfile=/tmp/node-docker-example \
  --output type=image,name=eggboy/node-buildkit:0.0.1,push=true \
  -export-cache type=registry,ref=eggboy/node-buildkit:cache,mode=max
  
## Cloud Native Buildpack
