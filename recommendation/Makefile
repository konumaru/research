DOCKER_IMAGE_NAME := research-$(lastword $(subst /, ,$(CURDIR)))
DOCKER_CONTAINER_NAME := $(lastword $(subst /, ,$(CURDIR)))-vm

build:
	sudo docker build --no-cache -t $(DOCKER_IMAGE_NAME) .

run:
	sudo docker run --rm \
		--user=root \
		-p 10000:10000 \
		-v ${PWD}:/workspace \
		--name $(DOCKER_CONTAINER_NAME) \
		-it $(DOCKER_IMAGE_NAME) \
		/bin/bash

exec:
	docker exec -it $(DOCKER_CONTAINER_NAME) /bin/bash

jupyter:
	jupyter lab --allow-root --no-browser --port 10000
