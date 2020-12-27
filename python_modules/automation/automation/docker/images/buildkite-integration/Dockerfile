####################################################################################################
#
# DAGSTER INTEGRATION IMAGE
#
# We use this Dockerfile to build an image for our Buildkite CI/CD pipeline.
#
####################################################################################################

ARG BASE_IMAGE
ARG PYTHON_VERSION
FROM "${BASE_IMAGE}" AS snapshot_builder

# Last git commit in dagster that build the snapshot files
RUN git clone https://github.com/dagster-io/dagster.git dagster \
    && cd dagster \
    && git checkout b1b22e4ec2a1140b64c71531b3b65d9656dbefcd

RUN apt-get update \
    && apt-get install -yqq \
        # Needed for matplotlib
        pkg-config \
        libfreetype6 \
        libfreetype6-dev \
        libpng-dev \
    && cd dagster \
    && make install_dev_python_modules \
    && pip freeze --exclude-editable > /snapshot-reqs.txt


FROM "${BASE_IMAGE}"

COPY --from=snapshot_builder /snapshot-reqs.txt .

RUN pip install -r /snapshot-reqs.txt \
    && rm /snapshot-reqs.txt
