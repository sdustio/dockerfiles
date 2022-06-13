FROM nvidia/cuda:11.3.1-runtime-ubuntu20.04

RUN set -eux; \
    apt-get update; \
	apt-get install -y --no-install-recommends \
        python3-dev \
		python3-pip \
		python-is-python3 \
    ; \
	rm -rf /var/lib/apt/lists/*;

RUN pip --disable-pip-version-check --no-cache-dir install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu113
