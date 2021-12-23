# syntax = docker/dockerfile:1.3-labs
FROM python:3.9.7

WORKDIR /workspace

ENV DEBCONF_NOWARNINGS=yes

RUN apt-get update
RUN apt-get -y install locales && \
    localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
RUN apt-get install -y vim bash-completion jq

COPY pyproject.toml .

RUN pip install -U pip
RUN pip install poetry \
    && poetry config virtualenvs.create false \
    && poetry install \
    && rm pyproject.toml

# Setting jupyter_notebook_config
RUN jupyter notebook --generate-config
RUN echo "c.NotebookApp.ip = '0.0.0.0'" >> /root/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.notebook_dir = '/workspace'" >> /root/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.open_browser = False" >> /root/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.token = ''" >> /root/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.password = ''" >> /root/.jupyter/jupyter_notebook_config.py
# Setting jupyter code formatter
RUN jupyter nbextension install https://github.com/drillan/jupyter-black/archive/master.zip --user
RUN jupyter nbextension enable jupyter-black-master/jupyter-black
RUN mkdir -p /root/.jupyter/lab/user-settings/@jupyterlab/shortcuts-extension
RUN cat <<'EOF' > /root/.jupyter/lab/user-settings/@jupyterlab/shortcuts-extension/shortcuts.jupyterlab-settings
{
    "shortcuts": [
        {
            "command": "jupyterlab_code_formatter:format_all",
            "keys": [
                "Ctrl K",
                "Ctrl M"
            ],
            "selector": ".jp-Notebook.jp-mod-editMode"
        }
    ]
}
EOF
RUN cat <<'EOF' > /root/.jupyter/nbconfig/notebook.json
{
    "codeCellConfig": {
        "lineNumbers": true,
    }
}
EOF



RUN echo "source /etc/bash_completion" >> ~/.bashrc

EXPOSE 10000
