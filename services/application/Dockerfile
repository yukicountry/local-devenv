FROM python:3.8-slim-buster

SHELL [ "/bin/bash", "-oeux", "pipefail", "-c" ]

WORKDIR /application

ARG USERNAME=developer
ARG USER_UID=1000
ARG PASSWD=password
ARG MAIN_MODULE=example:app

ENV MAIN_MODULE=${MAIN_MODULE}

# TODO: aptの最適化（キャッシュの削除など）
RUN apt -y update && \
    apt clean && \
    rm -rf /var/lib/apt/lists/* && \
    pip install uvicorn && \
    useradd -m -s /bin/bash -u ${USER_UID} ${USERNAME} && \
    gpasswd -a ${USERNAME} sudo && \
    chown -R ${USERNAME}:${USERNAME} /application

USER ${USERNAME}

COPY ./example.py .

EXPOSE 8000

CMD uvicorn ${MAIN_MODULE} --host 0.0.0.0 --reload
