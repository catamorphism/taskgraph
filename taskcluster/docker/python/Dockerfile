# This Source Code Form is subject to the terms of the Mozilla Public
# License, v. 2.0. If a copy of the MPL was not distributed with this
# file, You can obtain one at http://mozilla.org/MPL/2.0/.

# %ARG PYTHON_VERSION
FROM python:$PYTHON_VERSION
MAINTAINER Andrew Halberstadt <ahal@mozilla.com>

# Add worker user
RUN mkdir /builds && \
    useradd -d /builds/worker -s /bin/bash -m worker && \
    mkdir /builds/worker/artifacts && \
    chown worker:worker /builds/worker/artifacts

# %include-run-task

RUN apt-get update && apt-get install -y --force-yes --no-install-recommends \
    mercurial build-essential zlib1g-dev libssl-dev

ENV SHELL=/bin/bash \
    HOME=/builds/worker \
    PATH=/builds/worker/.local/bin:$PATH

VOLUME /builds/worker/checkouts
VOLUME /builds/worker/.cache

# pyenv
# %ARG PYENV_VERSIONS
ENV PYENV_ROOT=/builds/worker/.pyenv \
    PATH=/builds/worker/.pyenv/bin:/builds/worker/.pyenv/shims:$PATH
# %include taskcluster/scripts/pyenv-setup
ADD topsrcdir/taskcluster/scripts/pyenv-setup /builds/worker/pyenv-setup
RUN chmod +x /builds/worker/pyenv-setup && /builds/worker/pyenv-setup "$PYENV_VERSIONS"

# Set a default command useful for debugging
CMD ["/bin/bash", "--login"]
