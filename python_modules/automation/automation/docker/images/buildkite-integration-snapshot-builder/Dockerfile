ARG BASE_IMAGE
FROM "${BASE_IMAGE}"

# Last git commit in dagster that build the snapshot files
RUN git clone https://github.com/dagster-io/dagster.git dagster \
    && cd dagster \
    && git checkout 51c13f7c2a82267739c2c44dd674ba8ae8d2c94f

# for some reason this is only failing in the 3.8 image
# RUN cd dagster && git checkout "${SNAPSHOT_GIT_HASH}"

RUN cd dagster && make install_dev_python_modules_verbose
