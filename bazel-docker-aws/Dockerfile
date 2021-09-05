FROM dzag/bazel-docker:2004.5.0

ARG AWSCLI_VERSION=2.2.35
ARG AWSCLI_SHA256=bfdd14ffaa5237a90949ca24a1f8556fa54a47db893546e83b6a45925c9c1be3

RUN wget -O awscliv2.zip "https://awscli.amazonaws.com/awscli-exe-linux-x86_64-${AWSCLI_VERSION}.zip" \
  && echo "$AWSCLI_SHA256 awscliv2.zip" | sha256sum -c - \
  && unzip awscliv2.zip \
  && ./aws/install

RUN apt-get update \
  && apt-get install -y apt-utils amazon-ecr-credential-helper

RUN mkdir -p ~/.docker \
  && echo "{ \"credsStore\": \"ecr-login\" }" > ~/.docker/config.json