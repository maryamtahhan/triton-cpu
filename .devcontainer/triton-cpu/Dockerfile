
ARG USERNAME=1001
ARG USER_UID=1000
ARG USER_GID=$USER_UID

FROM registry.access.redhat.com/ubi9/python-312 AS base
USER 0

FROM base AS triton-1001
RUN chown -R 1001:0 ./
ENV XDG_RUNTIME_DIR=/run/user/$USER_GID
ENV _CONTAINERS_USERNS_CONFIGURED=""
USER 1001

FROM base AS triton-0
USER 0

FROM triton-${USERNAME}
ENV PYTHON_VERSION=3.12 \
    PATH=$HOME/.local/bin/:$PATH \
    PYTHONUNBUFFERED=1 \
    TRITON_CPU_BACKEND=1

# install dependencies
RUN pip install --upgrade pip
RUN pip install --upgrade setuptools
RUN pip install ninja cmake wheel pybind11;
RUN echo "export MAX_JOBS=$(nproc --all)" >> "${HOME}"/.bashrc
