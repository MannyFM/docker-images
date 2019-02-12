#include make_env

NS ?= mannyfm
VERSION ?= latest

IMAGE_NAME ?= tx2-opencv-dev
CONTAINER_NAME ?= tx2-opencv-dev
CONTAINER_INSTANCE ?= default
DOCKER ?= tx2-docker

.PHONY: build push shell run start stop rm release 

build: Dockerfile
	$(DOCKER) build -t $(NS)/$(IMAGE_NAME):$(VERSION) -f Dockerfile .

push:
	$(DOCKER) push $(NS)/$(IMAGE_NAME):$(VERSION)
 
shell:
	$(DOCKER) run --rm --name $(CONTAINER_NAME)-$(CONTAINER_INSTANCE) -i -t $(PORTS) $(VOLUMES) $(ENV) $(NS)/$(IMAGE_NAME):$(VERSION) /bin/bash

run:
	$(DOCKER) run --rm --name $(CONTAINER_NAME)-$(CONTAINER_INSTANCE) $(PORTS) $(VOLUMES) $(ENV) $(NS)/$(IMAGE_NAME):$(VERSION)

start:
	$(DOCKER) run -d --name $(CONTAINER_NAME)-$(CONTAINER_INSTANCE) $(PORTS) $(VOLUMES) $(ENV) $(NS)/$(IMAGE_NAME):$(VERSION)

stop:
	$(DOCKER) stop $(CONTAINER_NAME)-$(CONTAINER_INSTANCE)

rm:
	$(DOCKER) rm $(CONTAINER_NAME)-$(CONTAINER_INSTANCE)

release: build
	make push -e VERSION=$(VERSION)

default: build

