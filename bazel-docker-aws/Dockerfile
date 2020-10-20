FROM dzag/bazel-docker:2004.1.0

ARG AWSCLI_VERSION=2.0.57
ARG AWSCLI_SHA256=6cdfdeefc173ca3e260d0deb80e3151fad5df6e115355fdafdcf955b42f1666c

RUN wget -O awscliv2.zip "https://awscli.amazonaws.com/awscli-exe-linux-x86_64-${AWSCLI_VERSION}.zip" \
  && echo "$AWSCLI_SHA256 awscliv2.zip" | sha256sum -c - \
  && unzip awscliv2.zip \
  && ./aws/install

RUN apt-get update \
  && apt-get install apt-utils amazon-ecr-credential-helper

 RUN mkdir -p ~/.docker \
  && echo "{ \"credsStore\": \"ecr-login\" }" > ~/.docker/config.json