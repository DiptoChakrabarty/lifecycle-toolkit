DOCREPO := github.com/keptn-sandbox/lifecycle-toolkit-docs
TMPDIR := $(CURDIR)/tmp
VOLUMES := -v $(TMPDIR)/lifecycle-toolkit-docs:/src -v $(CURDIR)/content/en/docs:/src/content/en/docs-dev
# renovate: datasource=docker depName=klakegg/hugo
HUGO_VERSION := 0.105.0-ext
IMAGE := klakegg/hugo:$(HUGO_VERSION)
PORT := 1314

.PHONY: build server clean htmltest

clone:
	@rm -rf $(TMPDIR)/lifecycle-toolkit-docs | true
	@mkdir -p $(TMPDIR)/lifecycle-toolkit-docs
	@git clone https://$(DOCREPO) $(TMPDIR)/lifecycle-toolkit-docs

build:
	docker run --rm -it $(VOLUMES) $(IMAGE) -D -v

server:
	docker run --rm -it $(VOLUMES) -p  $(PORT):$(PORT) $(IMAGE) server -D -p $(PORT)

clean:
	docker run --rm -it $(VOLUMES) $(IMAGE) --cleanDestinationDir

htmltest: clone build
	docker run -v $(CURDIR):/test --rm wjdp/htmltest -s /test/tmp/lifecycle-toolkit-docs/public
