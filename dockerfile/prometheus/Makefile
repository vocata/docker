TAG            = v2.43.0
IMAGE_NAME     = prometheus
TMP_IMAGE_NAME = prometheus-tmp
CONTAINER_NAME = prometheus-container
DOCKERFILE     = ./Dockerfile
DOCKER_CONTEXT = .
CMD						 = /bin/sh

$(IMAGE_NAME): $(Dockerfile)
	docker build -f $(DOCKERFILE) -t $(IMAGE_NAME):$(TAG) $(DOCKER_CONTEXT)

.PHONY: run push test clean cleani cleanup
run: 
	docker run -d --name $(CONTAINER_NAME) -p 9090:9090 -v ./prometheus.yml:/etc/prometheus/prometheus.yml $(IMAGE_NAME):$(TAG)

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
