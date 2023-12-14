ARG PYTHON_VERSION
FROM python:${PYTHON_VERSION}



ARG DEFAULT_USERNAME
ARG USERNAME=${DEFAULT_USERNAME}
ARG USER_UID=1000
ARG USER_GID=$USER_UID
ENV TZ=Asia/Seoul
# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    #
    # [Optional] Add sudo support. Omit if you don't need to install software after connecting.
    && apt-get update \
    && apt-get install -y sudo \
    && apt-get install -y tzdata \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
RUN ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && echo ${TZ} > /etc/timezone

# ********************************************************
# * Anything else you want to do like clean up goes here *
# ********************************************************

# [Optional] Set the default user. Omit if you want to keep the default as root.
USER $USERNAME


COPY . /var/www
WORKDIR /var/www/study-coding-test

COPY ./requirements.txt /var/www/study-coding-test

RUN pip install --upgrade pip
RUN pip install -r requirements.txt

EXPOSE 80
## install tzdata package for timezone setting

# ENTRYPOINT ["python3"]
CMD ["tail", "-f", "/dev/null"]
