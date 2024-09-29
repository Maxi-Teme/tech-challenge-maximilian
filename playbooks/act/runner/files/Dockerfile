FROM ghcr.io/catthehacker/ubuntu:act-latest

RUN curl -LO https://go.dev/dl/go1.23.1.linux-amd64.tar.gz
RUN tar -C /usr/local -xzf go1.23.1.linux-amd64.tar.gz
ENV PATH="$PATH:/usr/local/go/bin"

RUN curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/local/bin/
