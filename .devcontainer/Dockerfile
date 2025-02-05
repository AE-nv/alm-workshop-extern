# Use the latest dev-bookworm base image
FROM mcr.microsoft.com/devcontainers/base:bookworm

# Set environment variables to avoid interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# Install required dependencies in a single RUN command (reduces layers)
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl git tar ca-certificates bash-completion && \
    rm -rf /var/lib/apt/lists/*

# Install OpenShift CLI (oc), Go, Kubernetes CLI, and Helm in a single RUN command to reduce layers
RUN curl -L https://mirror.openshift.com/pub/openshift-v4/clients/ocp/stable/openshift-client-linux.tar.gz | \
    tar -xz -C /usr/local/bin && chmod +x /usr/local/bin/oc && \
    curl -fsSL https://golang.org/dl/go1.23.6.linux-amd64.tar.gz | \
    tar -C /usr/local -xz && ln -s /usr/local/go/bin/go /usr/local/bin/go && \
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" && \
    chmod +x kubectl && mv kubectl /usr/local/bin/ && \
    curl -fsSL https://get.helm.sh/helm-v3.11.2-linux-amd64.tar.gz | \
    tar -xz -C /usr/local/bin --strip-components=1

# Set up Go path
ENV GOPATH=/go
ENV PATH=$GOPATH/bin:/usr/local/go/bin:$PATH

# Default shell
CMD ["bash"]
