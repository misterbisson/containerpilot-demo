FROM ubuntu:16.04

# Install the PHP extensions we need, and other packages
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        jq \
        less \
        unzip \
    && rm -rf /var/lib/apt/lists/*


# Add Containerpilot
# Releases at https://github.com/joyent/containerpilot/releases
ENV CONTAINERPILOT_VER 2.6.0
ENV CONTAINERPILOT file:///etc/containerpilot.json

RUN set -ex \
    && export CONTAINERPILOT_CHECKSUM=c1bcd137fadd26ca2998eec192d04c08f62beb1f \
    && curl -L --retry 7 --fail -vo /tmp/containerpilot.tar.gz \
         "https://github.com/joyent/containerpilot/releases/download/${CONTAINERPILOT_VER}/containerpilot-${CONTAINERPILOT_VER}.tar.gz" \
    && echo "${CONTAINERPILOT_CHECKSUM}  /tmp/containerpilot.tar.gz" | sha1sum -c \
    && tar zxf /tmp/containerpilot.tar.gz -C /usr/local/bin \
    && rm /tmp/containerpilot.tar.gz



# Install Consul
# Releases at https://releases.hashicorp.com/consul
RUN set -ex \
    && export CONSUL_VERSION=0.7.1 \
    && export CONSUL_CHECKSUM=5dbfc555352bded8a39c7a8bf28b5d7cf47dec493bc0496e21603c84dfe41b4b \
    && curl -L --retry 7 --fail -vo /tmp/consul.zip "https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip" \
    && echo "${CONSUL_CHECKSUM}  /tmp/consul.zip" | sha256sum -c \
    && unzip /tmp/consul -d /usr/local/bin \
    && rm /tmp/consul.zip \
    # Create empty directories for Consul config and data \
    && mkdir -p /etc/consul \
    && mkdir -p /var/lib/consul



# Copy our configuration, helper scripts, templates, and top-level content
COPY etc /etc

CMD ["/usr/local/bin/containerpilot", \
    "sleep", "365d"]