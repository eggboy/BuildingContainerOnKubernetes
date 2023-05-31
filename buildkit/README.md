## BuildKit

To install BuildKit agent on Kubernetes:
https://github.com/moby/buildkit/tree/master/examples/kubernetes

Steps
1. Create certs for BuildKit
$ ./create-certs.sh buildkitd.default.svc.cluster.local
$ kubectl apply -f .certs/buildkit-daemon-certs.yaml

2. Create a service 
$ kubectl apply -f service.yml

3. 
kubectl apply -f deployment-rootless.yml





### Using BuildKit to build container

$ buildctl \
--addr tcp://[ips]:1234 \
--tlscacert .certs/client/ca.pem \
--tlscert .certs/client/cert.pem \
--tlskey .certs/client/key.pem \
build --frontend dockerfile.v0 --local context=/tmp/node-docker-example --local dockerfile=/tmp/node-docker-example \
--output type=image,name=eggboy/node-buildkit:0.0.1,push=true \
-export-cache type=registry,ref=eggboy/node-buildkit:cache,mode=max
  