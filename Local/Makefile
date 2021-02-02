
REGISTRY = registry.k8s.asten.maq
VENDOR = system
ARCH = ppc64le

# storage provisioner tag to push changes to
TAG = 1.0.2

# Set the version information for the Kubernetes servers
LDFLAGS := "-X k8s.io/minikube/pkg/storage.version=v4 -s -w -extldflags '-static'"

#.PHONY: clean
#clean: ## Clean build
#	rm -rf out

out/local-provisioner: out/local-provisioner-$(ARCH)
	cp out/local-provisioner-$(ARCH) out/local-provisioner

out/local-provisioner-$(ARCH): cmd/storage-provisioner/main.go pkg/storage/storage_provisioner.go
	CGO_ENABLED=0 GOOS=linux GOARCH=$(ARCH) go build -o out/local-provisioner-$(ARCH) -ldflags=$(PROVISIONER_LDFLAGS) cmd/storage-provisioner/main.go


local-provisioner-image: out/local-provisioner ## Build storage-provisioner docker image
	docker image build -t build/local-provisioner .
	docker image tag build/local-provisioner $(REGISTRY)/$(VENDOR)/local-provisioner\:$(TAG)
	docker image push $(REGISTRY)/$(VENDOR)/local-provisioner\:$(TAG)

.PHONY: all
all:    out/local-provisioner

.PHONY: image
image:  local-provisioner-image





