
FROM python:3

# Create a non-root user with UID 1000
ARG USERNAME=pydev
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN if id -u $USER_UID ; then userdel `id -un $USER_UID` ; fi

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME -s /bin/bash \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# update the container
RUN apt-get update \
    && apt-get upgrade -y

# add additional dependencies
RUN apt-get install -y \
        build-essential \
        curl \
        git

# clean up a bit
RUN apt-get autoremove --purge -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Set the default user for the container
USER $USERNAME