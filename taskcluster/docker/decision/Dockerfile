FROM          ubuntu:20.04
MAINTAINER Release Engineering <release@mozilla.com>

# Add worker user
RUN mkdir /builds && \
    useradd -d /builds/worker -s /bin/bash -m worker && \
    mkdir /builds/worker/artifacts && \
    chown worker:worker /builds/worker/artifacts

# %include-run-task

# %include taskcluster/scripts/external_tools/tooltool.py
ADD topsrcdir/taskcluster/scripts/external_tools/tooltool.py /setup/tooltool.py

# Add taskgraph package.
# %include requirements/base.txt
ADD topsrcdir/requirements/base.txt /setup/requirements.txt

ADD system-setup.sh /setup/system-setup.sh
RUN bash /setup/system-setup.sh

ENV PATH=/builds/worker/bin:$PATH \
    SHELL=/bin/bash \
    HOME=/builds/worker

# Set a default command useful for debugging
CMD ["/bin/bash", "--login"]
