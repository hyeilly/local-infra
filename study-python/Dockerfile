ARG PYTHON_VERSION
ARG PYTHON_DEFAULT_PATH
ARG PROJECT_NAME

FROM python:${PYTHON_VERSION}

ARG DEFAULT_USERNAME
ARG USERNAME=${DEFAULT_USERNAME}
ARG USER_UID=1000
ARG USER_GID=$USER_UID
ENV TZ=Asia/Seoul

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && apt-get install -y tzdata \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
RUN ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && echo ${TZ} > /etc/timezone

USER $USERNAME

COPY . $PYTHON_DEFAULT_PATH
WORKDIR $PYTHON_DEFAULT_PATH/$PROJECT_NAME

RUN pip install --upgrade pip

EXPOSE 80

CMD ["tail", "-f", "/dev/null"]
