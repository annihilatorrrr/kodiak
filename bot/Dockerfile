FROM python:3.7-slim@sha256:e720c669cd7188d6a7e36e567be6bde9feb931d66219f1e4ba2caeb30e35d2cd

RUN apt update && \
  apt-get install --no-install-recommends -y \
    supervisor \
    git && \
  pip install \
    --no-cache-dir \
    poetry===1.1.8 && \
  poetry config virtualenvs.in-project true && \
  groupadd kodiak && \
  useradd --uid 1000 --gid kodiak kodiak && \
  mkdir -p /var/app && \
  chown -R kodiak:kodiak /var/app

WORKDIR /var/app

COPY --chown=kodiak pyproject.toml poetry.lock .

# install deps
RUN poetry install

COPY --chown=kodiak . .

USER kodiak

CMD ["/usr/bin/supervisord"]
