# Copyright 2017 The Kubernetes Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

.DEFAULT_GOAL=help

all: image

.PHONY: image push check-docker-registry

check-docker-registry:
ifndef DOCKER_REGISTRY
	$(error DOCKER_REGISTRY is undefined)
endif

image: check-docker-registry  ## Build the image
	docker build --network host -t $(DOCKER_REGISTRY)/nvidia-device-plugin:0.2.0-cuda10.0 -f image/Dockerfile image/

push: check-docker-registry   ## Push the image
	docker push $(DOCKER_REGISTRY)/nvidia-device-plugin:0.2.0-cuda10.0

help:   ## Print list of Makefile targets
	@# Taken from https://github.com/spf13/hugo/blob/master/Makefile
	@grep -E '^[a-zA-Z0-9_-]+:.*?## .*$$' $(MAKEFILE_LIST) | \
	  cut -d ":" -f1- | \
	  awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'
