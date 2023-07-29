# Note: these can be overriden on the command line e.g. `make GRAF_VERSION=9.5.3 PROM_VERSION=v2.44.1`
GRAF_VERSION="10.0.3"
PROM_VERSION="v2.46.0"

.PHONY: image

grafana-image := harricross/template-swarm-monitoring:grafana-$(GRAF_VERSION)
prometheus-image := harricross/template-swarm-monitoring:prometheus-$(PROM_VERSION)

images:
	docker run --privileged --rm tonistiigi/binfmt --install all
	docker buildx create --use --name crossplatform-builder default
	docker buildx build --platform linux/amd64,linux/arm64 --build-arg GRAFANA_VERSION=$(GRAF_VERSION) -t $(grafana-image) -f grafana/Dockerfile --push ./grafana
	docker buildx build --platform linux/amd64,linux/arm64 --build-arg GRAFANA_VERSION=$(PROM_VERSION) -t $(prometheus-image) -f prometheus/Dockerfile --push ./prometheus
