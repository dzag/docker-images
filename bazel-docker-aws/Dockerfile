FROM dzag/bazel-docker:2004.3.0

ARG AWSCLI_VERSION=2.2.5
ARG AWSCLI_SHA256=cc6b0541600d9d76458a107fcf2c7f7d68438e9b994f0a90ac8d6900a7b02d89

RUN wget -O awscliv2.zip "https://awscli.amazonaws.com/awscli-exe-linux-x86_64-${AWSCLI_VERSION}.zip" \
  && echo "$AWSCLI_SHA256 awscliv2.zip" | sha256sum -c - \
  && unzip awscliv2.zip \
  && ./aws/install

RUN apt-get update \
  && apt-get install -y apt-utils amazon-ecr-credential-helper

RUN mkdir -p ~/.docker \
  && echo "{ \"credsStore\": \"ecr-login\" }" > ~/.docker/config.json