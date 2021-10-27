build:
	docker build --no-cache -t python-exp .

rebuild:
	sudo docker build --no-cache -t python-exp .

run:
	sudo docker run -it --rm -p 127.0.0.0:8888:8888 -v ${PWD}:/workspace python-exp /bin/bash
