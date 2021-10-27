FROM python:3.9.7

WORKDIR /workspace

RUN apt-get update
RUN apt-get -y install locales && \
    localedef -f UTF-8 -i ja_JP ja_JP.UTF-8

COPY pyproject.toml .

RUN pip install -U pip
RUN pip install poetry \
    && poetry config virtualenvs.create false \
    && poetry install \
    && rm pyproject.toml

CMD [ "poetry" "run" "jupyter" "lab" "--allow-root"]
