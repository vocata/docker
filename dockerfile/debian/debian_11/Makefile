TAG            = 11
IMAGE_NAME     = debian
TMP_IMAGE_NAME = debian-11-tmp
CONTAINER_NAME = debian-11-container
DOCKERFILE     = ./Dockerfile
DOCKER_CONTEXT = .
CMD						 = /bin/bash

$(IMAGE_NAME): $(DOCKERFILE)
	docker build -f $(DOCKERFILE) -t $(IMAGE_NAME):$(TAG) $(DOCKER_CONTEXT)

.PHONY: run push test clean cleani cleanup
run: 
	docker run -it --name $(CONTAINER_NAME) $(IMAGE_NAME):$(TAG) $(CMD)

push:
	docker push $(IMAGE_NAME):$(TAG)

test:
	docker build -f $(DOCKERFILE) -t $(TMP_IMAGE_NAME):$(TAG) $(DOCKER_CONTEXT)
	docker run --rm -it $(TMP_IMAGE_NAME):$(TAG) $(CMD)
	docker rmi -f $(TMP_IMAGE_NAME):$(TAG)

clean:
	docker rm -f $(CONTAINER_NAME)

cleani:
	docker rmi -f $(IMAGE_NAME):$(TAG)

cleanup: clean cleani
