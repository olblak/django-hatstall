.PHONY: build run

VERSION= $(shell grep '_version_' ../_version.py  | awk -F '"' '{print $$2}') 
IMAGE='grimoirelab/hatstall'

build:
	@docker build -t $(IMAGE):$(VERSION) --build-arg HATSTALL_VERSION=$(VERSION) -f Dockerfile ..

publish:
	@docker push $(IMAGE):$(VERSION)

run:
	@docker run \
		-i -t --rm \
		-p 80:80 \
		--name hatstall_run \
		-e "HATSTALL_DEBUG=True" \
		-e "HATSTALL_ALLOWED_HOST=['*']" \
		$(IMAGE):$(VERSION)

shell:
	@docker run \
		-i -t --rm \
		-p 80:80 \
		--name hatstall_shell \
		--entrypoint /bin/bash \
		-e "HATSTALL_DEBUG=True" \
		-e "HATSTALL_ALLOWED_HOST=['*']" \
		$(IMAGE):$(VERSION)
