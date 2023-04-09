TAG            = ubuntu22.04
IMAGE_NAME     = sshd
TMP_IMAGE_NAME = sshd-ubuntu2204-tmp
CONTAINER_NAME = sshd-ubuntu2204-container
DOCKERFILE     = ./Dockerfile
DOCKER_CONTEXT = .
CMD						 = /bin/bash

$(IMAGE_NAME): Dockerfile
	docker build -f $(DOCKERFILE) -t $(IMAGE_NAME):$(TAG) $(DOCKER_CONTEXT)

.PHONY: run push test clean cleani cleanup
run: 
	docker run -d --name $(CONTAINER_NAME) --net host -v ./sshd_config:/etc/ssh/sshd_config -v ./authorized_keys:/home/docker/.ssh/authorized_keys $(IMAGE_NAME):$(TAG)

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
