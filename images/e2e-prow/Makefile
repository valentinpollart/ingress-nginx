TAG ?=v$(shell date +%m%d%Y)-$(shell git rev-parse --short HEAD)
REGISTRY ?= quay.io/kubernetes-ingress-controller
DOCKER ?= docker

IMAGE = $(REGISTRY)/e2e-prow

all: docker-build docker-push

docker-build:
	$(DOCKER) buildx build \
		--pull \
		--load \
		--build-arg K8S_RELEASE=v1.17.0 \
		--build-arg ETCD_VERSION=v3.3.18 \
		--build-arg KIND_VERSION=v0.7.0 \
		-t $(IMAGE):$(TAG) .

docker-push:
	$(DOCKER) push $(IMAGE):$(TAG)
	$(DOCKER) tag $(IMAGE):$(TAG) $(IMAGE):latest
	$(DOCKER) push $(IMAGE):latest
