FROM ros:foxy-ros-base

RUN set -eux; \
    apt-get update; \
	apt-get install -y --no-install-recommends \
        python3-pip \
		ca-certificates \
		curl \
    ; \
	rm -rf /var/lib/apt/lists/*;
